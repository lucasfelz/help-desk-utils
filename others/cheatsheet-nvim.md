# CheatSheet Nvim

## Top 100 Comandos Neovim para Iniciantes

O Neovim se estabeleceu como um editor de texto poderoso e extensível para desenvolvedores e usuários avançados. Construindo sobre a fundação do Vim, o Neovim oferece desempenho melhorado, uma arquitetura de plugin superior e uma comunidade vibrante que constantemente aprimora suas capacidades. Seja você um veterano experiente do Vim ou um novato na edição modal, ter um referencial de comandos abrangente à sua disposição pode melhorar dramaticamente sua eficiência e fluxo de trabalho.

Este guia compila 100 comandos essenciais do Neovim que todo usuário deve conhecer, organizados por categoria para referência rápida. Desde navegação básica até manipulação avançada de texto, esses comandos representam o conjunto de ferramentas que torna o Neovim um ambiente de edição tão formidable. Dominar até mesmo um subconjunto desses comandos aumentará significativamente sua produtividade e ajudará você a aproveitar todo o potencial do Neovim.

## Navegação Básica

1. `h`, `j`, `k`, `l` - Mover o cursor para a esquerda, para baixo, para cima, para a direita (as teclas de movimento principais no Neovim)
2. `w` - Ir para o início da próxima palavra (pontuação considerada como palavras)
3. `W` - Ir para o início da próxima WORD (palavras separadas por espaço)
4. `b` - Ir para o início da palavra anterior
5. `B` - Ir para o início da WORD anterior
6. `e` - Ir para o final da palavra
7. `E` - Ir para o final da WORD
8. `0` - Ir para o início da linha (primeira coluna)
9. `^` - Ir para o primeiro caractere não em branco da linha
10. `$` - Ir para o final da linha
11. `gg` - Ir para a primeira linha do documento
12. `G` - Ir para a última linha do documento
13. `{number}G` - Ir para o número da linha específico
14. `{` - Ir para o parágrafo/bloco de código anterior
15. `}` - Ir para o próximo parágrafo/bloco de código
16. `Ctrl-u` - Mover para cima meio tela
17. `Ctrl-d` - Mover para baixo meio tela
18. `Ctrl-b` - Mover para cima uma tela completa
19. `Ctrl-f` - Mover para baixo uma tela completa
20. `zz` - Centralizar o cursor na tela (a linha atual se torna a linha do meio)
21. `zt` - Posicionar o cursor no topo da tela
22. `zb` - Posicionar o cursor na parte inferior da tela

## Comandos de Edição

1. `i` - Entrar no modo de inserção antes do cursor (para inserir texto)
2. `I` - Entrar no modo de inserção no início da linha
3. `a` - Entrar no modo de inserção após o cursor (anexar)
4. `A` - Entrar no modo de inserção no final da linha
5. `o` - Inserir nova linha abaixo da linha atual e entrar no modo de inserção
6. `O` - Inserir nova linha acima da linha atual e entrar no modo de inserção
7. `r` - Substituir um único caractere sob o cursor (sem entrar no modo de inserção)
8. `R` - Entrar no modo de substituição (sobrescrever texto existente)
9. `x` - Excluir o caractere sob o cursor
10. `X` - Excluir o caractere antes do cursor
11. `dd` - Excluir toda a linha (e armazenar no registro)
12. `{number}dd` - Excluir múltiplas linhas
13. `D` - Excluir do cursor até o final da linha
14. `yy` ou `Y` - Yank (copiar) toda a linha
15. `{number}yy` - Yank múltiplas linhas
16. `y$` - Yank do cursor até o final da linha
17. `p` - Colar após o cursor
18. `P` - Colar antes do cursor
19. `u` - Desfazer a última alteração
20. `Ctrl-r` - Refazer (desfazer o desfazer)
21. `~` - Alternar o caso do caractere sob o cursor
22. `>>` - Indentar a linha
23. `<<` - Desindentar a linha
24. `.` - Repetir o último comando (poderoso para edições repetitivas)
25. `cc` ou `C` - Alterar toda a linha (excluir a linha e entrar no modo de inserção)
26. `cw` - Alterar a palavra (excluir a palavra e entrar no modo de inserção)
27. `c$` ou `C` - Alterar até o final da linha
28. `J` - Juntar a linha atual com a próxima linha

## Buscar e Substituir

1. `/padrão` - Buscar para frente pelo padrão
2. `?padrão` - Buscar para trás pelo padrão
3. `n` - Repetir a busca na mesma direção
4. `N` - Repetir a busca na direção oposta
5. `*` - Buscar para frente pela palavra sob o cursor
6. `#` - Buscar para trás pela palavra sob o cursor
7. `:%s/velho/novo/g` - Substituir todas as ocorrências de 'velho' por 'novo' em todo o arquivo
8. `:%s/velho/novo/gc` - Substituir todas as ocorrências com confirmações
9. `:s/velho/novo/g` - Substituir todas as ocorrências na linha atual
10. `:noh` - Limpar o destaque da busca
11. `gd` - Ir para a definição local da palavra sob o cursor
12. `gD` - Ir para a definição global da palavra sob o cursor

## Modo Visual

1. `v` - Entrar no modo visual caracter a caracter (selecionar caracteres)
2. `V` - Entrar no modo visual linha a linha (selecionar linhas inteiras)
3. `Ctrl-v` - Entrar no modo visual de bloco (selecionar blocos retangulares)
4. `gv` - Re-selecionar a seleção visual anterior
5. `o` - No modo visual: Mover para a outra extremidade da seleção
6. `O` - No modo visual de bloco: Mover para o outro canto do bloco
7. `aw` - Selecionar uma palavra (no modo visual)
8. `ab` - Selecionar um bloco com () (no modo visual)
9. `aB` - Selecionar um bloco com {} (no modo visual)
10. `at` - Selecionar um bloco com tags HTML/XML (no modo visual)

## Operações com Arquivos

1. `:e nome_do_arquivo` - Editar um arquivo (criar se não existir)
2. `:w` - Escrever (salvar) o arquivo
3. `:w nome_do_arquivo` - Escrever no nome do arquivo especificado (salvar como)
4. `:q` - Sair (falha se houver alterações não salvas)
5. `:q!` - Sair sem salvar (descartar alterações)
6. `:wq` ou `:x` - Escrever e sair
7. `:saveas nome_do_arquivo` - Salvar arquivo como nome_do_arquivo
8. `:r nome_do_arquivo` - Inserir o conteúdo do arquivo abaixo do cursor
9. `:r !comando` - Inserir a saída do comando de shell abaixo do cursor

## Trabalhando com Janelas e Abas

1. `:split` ou `:sp` - Dividir a janela horizontalmente
2. `:vsplit` ou `:vs` - Dividir a janela verticalmente
3. `Ctrl-w h/j/k/l` - Navegar entre janelas (esquerda/baixo/cima/direita)
4. `Ctrl-w +/-` - Aumentar/diminuir a altura da janela
5. `Ctrl-w </>`- Aumentar/diminuir a largura da janela
6. `Ctrl-w =` - Tornar todas as janelas de tamanho igual
7. `Ctrl-w o` - Tornar a janela atual a única
8. `:tabnew` - Criar nova aba
9. `gt` - Ir para a próxima aba
10. `gT` - Ir para a aba anterior
11. `:tabclose` - Fechar a aba atual
12. `:tabonly` - Fechar todas as outras abas

## Gerenciamento de Buffers

1. `:ls` - Listar todos os buffers
2. `:b número` - Alternar para o buffer pelo número
3. `:bn` - Próximo buffer
4. `:bp` - Buffer anterior
5. `:bd` - Excluir buffer (fechar arquivo)
6. `:bufdo comando` - Executar comando em todos os buffers
7. `:e #` - Editar o arquivo alternativo (geralmente o arquivo editado anteriormente)

## Marcas e Saltos

1. `m{a-z}` - Definir marca na posição atual (minúsculas para local do arquivo)
2. `m{A-Z}` - Definir marca na posição atual (maiúsculas para global)
3. `'{marca}` - Ir para a linha da marca
4. `` `{marca} `` - Ir para a posição da marca
5. `Ctrl-o` - Ir para a posição mais antiga na lista de saltos
6. `Ctrl-i` - Ir para a posição mais recente na lista de saltos
7. `'.` - Ir para a posição da última alteração
8. `` `. `` - Ir para a posição exata da última alteração

## Objetos de Texto e Movimentos

1. `ci(` - Alterar dentro de parênteses
2. `di"` - Excluir dentro de aspas duplas
3. `yi]` - Yank dentro de colchetes
4. `va{` - Selecionar visualmente em torno de chaves (incluindo as chaves)
5. `dap` - Excluir em torno do parágrafo
6. `cit` - Alterar dentro da tag HTML/XML
7. `diw` - Excluir dentro da palavra
8. `daw` - Excluir em torno da palavra (incluindo espaços)
9. `dab` - Excluir em torno do bloco (parênteses)
10. `daB` - Excluir em torno do bloco (chaves)

## Comandos de Dobra

1. `zf` - Criar dobra (no modo visual)
2. `zo` - Abrir a dobra sob o cursor
3. `zc` - Fechar a dobra sob o cursor
4. `za` - Alternar a dobra sob o cursor
5. `zR` - Abrir todas as dobras
6. `zM` - Fechar todas as dobras
7. `zj` - Mover para a próxima dobra
8. `zk` - Mover para a dobra anterior

## Recursos Específicos do Neovim

1. `:terminal` ou `:term` - Abrir terminal integrado
2. `Ctrl-\ Ctrl-n` - Sair do modo terminal para o modo normal
3. `:checkhealth` - Executar a ferramenta de diagnóstico do Neovim
4. `:lua require('telescope.builtin').find_files()` - Usar o plugin Telescope para encontrar arquivos
5. `:TSInstall linguagem` - Instalar o parser treesitter para uma linguagem
6. `:LspInfo` - Mostrar o status do Protocolo de Servidor de Linguagens
7. `:TSBufToggle highlight` - Alternar o destaque do treesitter
8. `:highlight` - Mostrar os grupos de destaque atuais
9. `:Tutor` - Iniciar o tutorial embutido do Neovim
10. `:help nvim-features` - Ver os recursos específicos do Neovim

## Recursos Avançados

1. `q{a-z}` - Gravar macro no registro
2. `@{a-z}` - Executar macro do registro
3. `@@` - Repetir a última macro executada
4. `g&` - Repetir a última substituição em todas as linhas
5. `:norm cmd` - Executar comando do modo normal nas linhas selecionadas
6. `gf` - Ir para o arquivo sob o cursor
7. `Ctrl-a` - Incrementar número sob o cursor
8. `Ctrl-x` - Decrementar número sob o cursor
9. `:sort` - Classificar linhas selecionadas
10. `!motion comando` - Filtrar texto através de comando externo
