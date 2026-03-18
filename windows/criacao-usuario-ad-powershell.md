## Scripts PS criação de usuário AD

## Exemplo de Uso:

```powershell
# Uso básico
New-ADUserWithPermissions -FirstName "João" -LastName "Silva" -SourceUser "usuario.modelo"

# Com nome do meio
New-ADUserWithPermissions -FirstName "Maria" -LastName "Santos" -MiddleNames @("da", "Silva") -SourceUser "usuario.modelo"

# Com informações completas
New-ADUserWithPermissions -FirstName "Pedro" -LastName "Costa" -SourceUser "usuario.modelo" -Department "TI" -JobTitle "Analista" -OrganizationalUnit "OU=Usuarios,DC=empresa,DC=com"
```

## Personalizações Recomendadas:

1. **Altere o domínio de email** na variável `$EmailDomain`
2. **Configure a empresa** na variável `$Company`
3. **Defina uma senha mais segura** no parâmetro `$DefaultPassword`
4. **Configure a OU padrão** se necessário

O script inclui tratamento de erros, feedback visual colorido e validações para garantir que funcione corretamente em seu ambiente. Precisa de alguma modificação específica?



# Script para criar usuários no Active Directory com cópia de permissões
# Autor: Customizável para ambiente corporativo
# Versão: 1.0

# Importar módulo do Active Directory
Import-Module ActiveDirectory

# Função para gerar login único
function Get-UniqueLogin {
    param(
        [string]$FirstName,
        [string]$LastName,
        [string[]]$MiddleNames = @()
    )
    
    # Remove acentos e caracteres especiais
    $FirstName = Remove-Accents $FirstName
    $LastName = Remove-Accents $LastName
    $MiddleNames = $MiddleNames | ForEach-Object { Remove-Accents $_ }
    
    # Primeira tentativa: primeira inicial + último sobrenome
    $login = ($FirstName.Substring(0,1) + $LastName).ToLower()
    
    if (-not (Get-ADUser -Filter "SamAccountName -eq '$login'" -ErrorAction SilentlyContinue)) {
        return $login
    }
    
    Write-Host "Login '$login' já existe. Tentando alternativa..." -ForegroundColor Yellow
    
    # Segunda tentativa: primeira inicial + primeira inicial do segundo nome/sobrenome + último sobrenome
    if ($MiddleNames.Count -gt 0) {
        $login = ($FirstName.Substring(0,1) + $MiddleNames[0].Substring(0,1) + $LastName).ToLower()
    } else {
        # Se não tem nome do meio, usa primeira inicial + duas primeiras letras do sobrenome
        $login = ($FirstName.Substring(0,1) + $LastName.Substring(0,[Math]::Min(2,$LastName.Length))).ToLower()
    }
    
    if (-not (Get-ADUser -Filter "SamAccountName -eq '$login'" -ErrorAction SilentlyContinue)) {
        return $login
    }
    
    # Terceira tentativa: adiciona números sequenciais
    $counter = 1
    $baseLogin = $login
    do {
        $login = $baseLogin + $counter
        $counter++
    } while (Get-ADUser -Filter "SamAccountName -eq '$login'" -ErrorAction SilentlyContinue)
    
    Write-Host "Usando login alternativo: '$login'" -ForegroundColor Green
    return $login
}

# Função para remover acentos
function Remove-Accents {
    param([string]$Text)
    
    $Text = $Text -replace '[àáâãäå]','a'
    $Text = $Text -replace '[èéêë]','e'
    $Text = $Text -replace '[ìíîï]','i'
    $Text = $Text -replace '[òóôõö]','o'
    $Text = $Text -replace '[ùúûü]','u'
    $Text = $Text -replace '[ç]','c'
    $Text = $Text -replace '[ñ]','n'
    $Text = $Text -replace '[ÀÁÂÃÄÅ]','A'
    $Text = $Text -replace '[ÈÉÊË]','E'
    $Text = $Text -replace '[ÌÍÎÏ]','I'
    $Text = $Text -replace '[ÒÓÔÕÖ]','O'
    $Text = $Text -replace '[ÙÚÛÜ]','U'
    $Text = $Text -replace '[Ç]','C'
    $Text = $Text -replace '[Ñ]','N'
    
    return $Text
}

# Função para copiar grupos de um usuário modelo
function Copy-UserGroups {
    param(
        [string]$SourceUser,
        [string]$TargetUser
    )
    
    try {
        $sourceGroups = Get-ADUser -Identity $SourceUser -Properties MemberOf | Select-Object -ExpandProperty MemberOf
        
        foreach ($group in $sourceGroups) {
            try {
                Add-ADGroupMember -Identity $group -Members $TargetUser -ErrorAction Stop
                Write-Host "✓ Adicionado ao grupo: $group" -ForegroundColor Green
            }
            catch {
                Write-Host "✗ Erro ao adicionar ao grupo $group`: $($_.Exception.Message)" -ForegroundColor Red
            }
        }
    }
    catch {
        Write-Host "✗ Erro ao copiar grupos: $($_.Exception.Message)" -ForegroundColor Red
    }
}

# Função principal para criar usuário
function New-ADUserWithPermissions {
    param(
        [Parameter(Mandatory=$true)]
        [string]$FirstName,
        
        [Parameter(Mandatory=$true)]
        [string]$LastName,
        
        [string[]]$MiddleNames = @(),
        
        [Parameter(Mandatory=$true)]
        [string]$SourceUser,
        
        [string]$DefaultPassword = "1234",
        
        [string]$OrganizationalUnit,
        
        [string]$Department,
        
        [string]$JobTitle,
        
        [string]$Company = "Sua Empresa",
        
        [string]$EmailDomain = "@suaempresa.com.br"
    )
    
    try {
        # Gerar login único
        $login = Get-UniqueLogin -FirstName $FirstName -LastName $LastName -MiddleNames $MiddleNames
        
        # Construir nome completo
        $fullName = if ($MiddleNames.Count -gt 0) {
            "$FirstName " + ($MiddleNames -join " ") + " $LastName"
        } else {
            "$FirstName $LastName"
        }
        
        # Definir email
        $email = "$login$EmailDomain"
        
        # Verificar se usuário modelo existe
        $sourceUserObj = Get-ADUser -Identity $SourceUser -ErrorAction Stop
        Write-Host "✓ Usuário modelo '$SourceUser' encontrado" -ForegroundColor Green
        
        # Converter senha para SecureString
        $securePassword = ConvertTo-SecureString -String $DefaultPassword -AsPlainText -Force
        
        # Parâmetros para criação do usuário
        $userParams = @{
            SamAccountName = $login
            Name = $fullName
            DisplayName = $fullName
            GivenName = $FirstName
            Surname = $LastName
            EmailAddress = $email
            UserPrincipalName = $email
            AccountPassword = $securePassword
            Enabled = $true
            ChangePasswordAtLogon = $true
            PasswordNeverExpires = $false
        }
        
        # Adicionar parâmetros opcionais se fornecidos
        if ($OrganizationalUnit) { $userParams.Path = $OrganizationalUnit }
        if ($Department) { $userParams.Department = $Department }
        if ($JobTitle) { $userParams.Title = $JobTitle }
        if ($Company) { $userParams.Company = $Company }
        
        # Criar usuário
        Write-Host "`nCriando usuário..." -ForegroundColor Cyan
        New-ADUser @userParams
        
        Write-Host "✓ Usuário '$fullName' criado com sucesso!" -ForegroundColor Green
        Write-Host "  Login: $login" -ForegroundColor White
        Write-Host "  Email: $email" -ForegroundColor White
        Write-Host "  Senha temporária: $DefaultPassword" -ForegroundColor Yellow
        
        # Aguardar replicação
        Start-Sleep -Seconds 2
        
        # Copiar grupos do usuário modelo
        Write-Host "`nCopiando permissões do usuário modelo..." -ForegroundColor Cyan
        Copy-UserGroups -SourceUser $SourceUser -TargetUser $login
        
        Write-Host "`n🎉 Processo concluído com sucesso!" -ForegroundColor Green
        
        return @{
            Success = $true
            Login = $login
            FullName = $fullName
            Email = $email
        }
    }
    catch {
        Write-Host "✗ Erro ao criar usuário: $($_.Exception.Message)" -ForegroundColor Red
        return @{
            Success = $false
            Error = $_.Exception.Message
        }
    }
}


# EXEMPLOS DE USO


# Exemplo 1: Uso básico
Write-Host "=== EXEMPLO DE USO DO SCRIPT ===" -ForegroundColor Magenta
Write-Host "Para criar um usuário, use o comando:" -ForegroundColor White
Write-Host 'New-ADUserWithPermissions -FirstName "João" -LastName "Silva" -SourceUser "usuario.modelo"' -ForegroundColor Green

Write-Host "`nPara usuário com nome do meio:" -ForegroundColor White
Write-Host 'New-ADUserWithPermissions -FirstName "Maria" -LastName "Santos" -MiddleNames @("da", "Silva") -SourceUser "usuario.modelo"' -ForegroundColor Green

Write-Host "`nCom parâmetros adicionais:" -ForegroundColor White
Write-Host 'New-ADUserWithPermissions -FirstName "Pedro" -LastName "Costa" -SourceUser "usuario.modelo" -Department "TI" -JobTitle "Analista" -OrganizationalUnit "OU=Usuarios,DC=empresa,DC=com"' -ForegroundColor Green


# CONFIGURAÇÕES PERSONALIZÁVEIS


Write-Host "`n=== CONFIGURAÇÕES PERSONALIZÁVEIS ===" -ForegroundColor Magenta
Write-Host "Edite as seguintes variáveis no início da função conforme seu ambiente:" -ForegroundColor Yellow
Write-Host "• EmailDomain: domínio do email da empresa" -ForegroundColor White
Write-Host "• Company: nome da empresa" -ForegroundColor White  
Write-Host "• DefaultPassword: senha padrão (recomenda-se alterar)" -ForegroundColor White
Write-Host "• OrganizationalUnit: OU padrão para novos usuários" -ForegroundColor White

Write-Host "`nPara executar o script:" -ForegroundColor Cyan
Write-Host "1. Certifique-se de ter o módulo ActiveDirectory instalado" -ForegroundColor White
Write-Host "2. Execute como administrador com permissões no AD" -ForegroundColor White
Write-Host "3. Personalize os parâmetros conforme necessário" -ForegroundColor White
