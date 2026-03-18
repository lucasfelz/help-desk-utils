
## 🎫 Documentação de Helpdesk/Troubleshooting

### Formato Base:

```
Ticket: #[número]
Usuário: [nome/setor]
Data/Hora: [timestamp]
Prioridade: [Baixa/Média/Alta/Crítica]

PROBLEMA RELATADO:
"Exatamente o que o usuário disse, entre aspas"

SINTOMAS OBSERVADOS:
- Sistema trava ao abrir Excel
- Mensagem de erro: "0x80070057"
- Afeta apenas arquivos .xlsx acima de 10MB

DIAGNÓSTICO:
Causa raiz: Memória RAM insuficiente + Office 32-bit

SOLUÇÃO APLICADA:
1. Verificado memória disponível (Task Manager)
2. Desinstalado Office 32-bit
3. Instalado Office 64-bit (versão 16.0.xxxxx)
4. Testado com arquivo de 15MB - funcionou normalmente

TEMPO DE RESOLUÇÃO: 45 minutos

STATUS: ✓ Resolvido
```

### Base de Conhecimento (KB):

Transforme tickets recorrentes em artigos:

```
KB-0042: Erro "DNS_PROBE_FINISHED_NXDOMAIN" no Chrome

CENÁRIO:
Usuário não consegue acessar sites, mas internet funciona

DIAGNÓSTICO RÁPIDO:
1. Abrir CMD: ping 8.8.8.8 (funciona?) → Problema é DNS
2. ping google.com (não funciona?) → Confirma DNS

SOLUÇÃO PADRÃO:
1. Configurar DNS manual:
   - Painel de Controle > Rede > Adaptador > Propriedades
   - IPv4 > Propriedades
   - Usar: 8.8.8.8 e 8.8.4.4
2. Limpar cache: ipconfig /flushdns
3. Reiniciar navegador

CASOS ESPECIAIS:
- Se estiver em rede corporativa: use DNS interno (10.0.0.1)
- Se VPN ativa: desconectar e reconectar
```

### ⚠️ Nunca Esqueça em Helpdesk:

- **Sempre registre a causa raiz**, não só a solução
- **Mudanças feitas no sistema** do usuário
- **O que NÃO funcionou** antes da solução final
- **Follow-up**: funcionou 24h depois?

---

## 🎨 Boas Práticas de Formatação

### Use Hierarquia Visual:

```
# Título Principal
## Seção
### Subseção
- Item de lista
  - Sub-item
```

### Destaque o Importante:

- **Negrito** para comandos críticos
- `código inline` para comandos/caminhos
- > Blocos de citação para observações importantes
    
- ⚠️ 🔴 ⚡ Emojis para diferentes níveis de alerta

### Blocos de Código Sempre com Linguagem:

```bash
#!/bin/bash
echo "Fica mais fácil de ler"
```

```python
# E permite syntax highlighting
print("Melhor visualização")
```

---

## 📦 Organização de Arquivos

### Estrutura de Pastas Sugerida:

```
/Documentação/
├── POPs/
│   ├── 001-Backup-Diario.md
│   ├── 002-Deploy-Aplicacao.md
├── Labs/
│   ├── 2024-11-05-Lab-SQLi/
│   │   ├── relatorio.md
│   │   ├── evidencias/
│   │   └── comandos.txt
├── Helpdesk/
│   ├── KB/
│   │   ├── KB-001-Erro-DNS.md
│   ├── Tickets/
│   │   ├── 2024-11/
├── Templates/
│   ├── template-pop.md
│   ├── template-lab.md
```

### Nomenclatura de Arquivos:

- **POPs**: `NNN-Nome-Descritivo.md` (ex: 042-Reiniciar-Servidor.md)
- **Labs**: `YYYY-MM-DD-Alvo-Tipo.md` (ex: 2024-11-05-WebApp-XSS.md)
- **KBs**: `KB-NNNN-Resumo.md` (ex: KB-0123-Erro-Impressao.md)

---

## 🔄 Manutenção e Versionamento

### Controle de Versões:

```
v1.0 - 05/11/2024 - João Silva - Criação inicial
v1.1 - 10/11/2024 - Maria Costa - Adicionado seção troubleshooting
v2.0 - 15/11/2024 - João Silva - Reestruturação completa
```

### Revisão Periódica:

- POPs: revisar a cada 6 meses ou quando mudar processo
- Labs: não mudam, mas adicione notas se ferramentas ficarem obsoletas
- KB Helpdesk: marcar como obsoleto quando não aplicar mais

### Marcação de Status:

```
[ATUAL] - Em uso ativo
[DEPRECATED] - Não usar mais, mas mantido para referência
[RASCUNHO] - Ainda em desenvolvimento
[ARQUIVADO] - Histórico apenas
```

---

## ✅ Checklist Final Antes de Publicar

Pergunte-se:

□ Alguém sem contexto consegue executar isso sozinho?  
□ Todas as ferramentas/versões estão especificadas?  
□ Tem prints/evidências suficientes?  
□ Riscos e avisos estão destacados?  
□ Está em português claro (ou inglês técnico consistente)?  
□ Comandos foram testados e funcionam?  
□ Tem seção de troubleshooting?  
□ Cabeçalho com metadados está preenchido?  
□ Formatação está legível (não é textão corrido)?  
□ Salvei em formato que não vai corromper (Markdown/PDF)?

---

## 💡 Dica de Ouro

**Documente ENQUANTO faz, não depois!**

Mantenha um bloco de notas aberto e vá anotando:

- Cada comando executado (copie do histórico)
- Erros que apareceram
- O que pensou em cada decisão
- Tempo que cada etapa levou

Depois é só organizar. Tentar lembrar depois = documentação incompleta.
