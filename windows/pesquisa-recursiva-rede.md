## Script para pesquisa recursiva windows## Pesquisa no próprio computador
```powershell
Get-ChildItem -Path C:\ -Recurse -ErrorAction SilentlyContinue -Filter "*file_name"
```




## Obter os compartilhamentos do servidor

```powershell
$server = "srv-arquivos"

# Obter os compartilhamentos do servidor
$shares = Get-SmbShare -CimSession $server | Where-Object { $_.Name -notin @("IPC$", "ADMIN$", "C$") }

foreach ($share in $shares) {
    $path = "\\$server\$($share.Name)"
    Write-Host "`n--- Pesquisando em $path ---" -ForegroundColor Cyan

    Get-ChildItem -Path $path -Recurse -ErrorAction SilentlyContinue -Filter "*Informativo*" |
        Select-Object FullName, LastWriteTime
}

```


### ✅ **2. Se você quer pesquisar apenas dentro de UM compartilhamento**

Exemplo: o compartilhamento seja `\\srv-arquivos\documentos$`


```powershell
Get-ChildItem -Path "\\srv-arquivos\documentos$" -Recurse -Filter "*Informativo*" -ErrorAction SilentlyContinue
```
