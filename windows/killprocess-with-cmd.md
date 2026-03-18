1. Identificar o processo
Primeiro, você precisa saber o nome do executável (por exemplo, chrome.exe ou msedge.exe) ou o ID do processo (PID) do programa que deseja fechar. 
Abra o CMD (procure por "cmd" no menu Iniciar e execute-o como administrador para ter privilégios totais).
Digite o comando tasklist e pressione Enter.
Uma lista de todos os processos em execução será exibida. Localize o nome da imagem (Image Name) ou o PID (PID) do processo que você quer encerrar. 
2. Matar o processo
Depois de identificar o processo, use o comando taskkill com os parâmetros apropriados. 
Para encerrar pelo nome do executável:
Use a sintaxe taskkill /f /im [nome_do_processo.exe]. O parâmetro /f força o encerramento do processo, o que é útil para programas travados. 
Exemplo: Para fechar o navegador Microsoft Edge, o comando seria:
cmd
taskkill /f /im msedge.exe
Navegadores modernos abrem múltiplos processos para diferentes abas, e esse comando fechará todos eles simultaneamente. 
Para encerrar pelo PID (ID do Processo):
Use a sintaxe taskkill /f /pid [número_do_PID].
Exemplo: Se o PID do processo for 1234, o comando seria:
cmd
taskkill /f /pid 1234
