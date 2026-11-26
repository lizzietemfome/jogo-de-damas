# Relatório de testes

## Ambiente e evidência

Data das validações: **23/11/2026**. As atividades abaixo são registradas separadamente:

| Forma de validação | Resultado | Evidência |
| --- | --- | --- |
| Automação Java | 57 casos aprovados, zero reprovados: 23 TM, 10 TA e 24 extras. | [Saída integral da suíte](resultado-automatizado.txt). |
| Interface do Eclipse operada por agente | Os 33 casos obrigatórios, TM01 a TM23 e TA01 a TA10, foram executados e aprovados no console. | [Índice das capturas e comandos](evidencias-eclipse/LEIA-ME.md). |
| Execução humana por Júlia ou pela equipe | NÃO EXECUTADO nesta preparação; registro a preencher após a execução pessoal. | [Roteiro para repetir os testes](roteiro-manual.md). |

Na automação Java, o código foi compilado com **OpenJDK 17.0.20**, usando `javac --release 8 -encoding UTF-8`, e executado pela classe `testes.TestesJogo`, sem bibliotecas externas. Esse parâmetro limita a linguagem e as APIs públicas ao Java 8. Iniciar essa suíte no Eclipse também é automação Java; isso não muda sua natureza para teste manual.

Na validação de interface, foi utilizado **Eclipse IDE 2026-09 R, versão 4.41.0, build 4.41.0.20260903-0719, macOS 27.2 arm64**, com o runtime embutido **Eclipse Adoptium 25.0.4.1**. O projeto real foi importado por **General → Existing Projects into Workspace**, compilado automaticamente pelo Eclipse e iniciado em `Main` por **Run As → Java Application**, sem alterar o código-fonte. A operação da interface foi feita pelo agente: os comandos foram enviados em pequenos blocos ao console e os resultados foram observados nas capturas de tela. A [importação](evidencias-eclipse/01-importacao.png) e a [execução inicial](evidencias-eclipse/TM01.png) estão registradas.

Os resultados da interface não são atribuídos a uma execução humana. Para a conferência pessoal exigida da equipe pelo enunciado, use o [roteiro manual](roteiro-manual.md), registre o responsável, a data e os resultados na última coluna. O [roteiro de apresentação](../docs/roteiro-apresentacao.md) oferece uma sequência curta para o ensaio.

## Casos obrigatórios

| Teste | Resultado observado | Automação Java | UI no Eclipse por agente | Execução humana |
| --- | --- | --- | --- | --- |
| TM01 | Tabuleiro exato, 12 peças por cor, brancas iniciam, partida em andamento. | APROVADO | [APROVADO](evidencias-eclipse/TM01.png) | NÃO EXECUTADO |
| TM02 | A3 esvaziada, branca em B4, turno das pretas. | APROVADO | [APROVADO](evidencias-eclipse/TM02.png) | NÃO EXECUTADO |
| TM03 | Movimento horizontal rejeitado sem alterar estado. | APROVADO | [APROVADO](evidencias-eclipse/TM03.png) | NÃO EXECUTADO |
| TM04 | Destino ocupado rejeitado sem alterar estado. | APROVADO | [APROVADO](evidencias-eclipse/TM04.png) | NÃO EXECUTADO |
| TM05 | Peça adversária rejeitada sem alterar turno. | APROVADO | [APROVADO](evidencias-eclipse/TM05.png) | NÃO EXECUTADO |
| TM06 | Coordenada inválida gera erro e console continua. | APROVADO | [APROVADO](evidencias-eclipse/TM06.png) | NÃO EXECUTADO |
| TM07 | Duas jogadas alternadas aceitas; turno retorna às brancas. | APROVADO | [APROVADO](evidencias-eclipse/TM07.png) | NÃO EXECUTADO |
| TM08 | Segunda jogada branca consecutiva rejeitada. | APROVADO | [APROVADO](evidencias-eclipse/TM08.png) | NÃO EXECUTADO |
| TM09 | Captura simples remove D4 e mantém adversário extra para continuidade. | APROVADO | [APROVADO](evidencias-eclipse/TM09.png) | NÃO EXECUTADO |
| TM10 | Movimento simples rejeitado quando existe captura. | APROVADO | [APROVADO](evidencias-eclipse/TM10.png) | NÃO EXECUTADO |
| TM11 | Turno retido na primeira etapa; capturados removidos somente ao final. | APROVADO | APROVADO — [A](evidencias-eclipse/TM11-A.png), [B](evidencias-eclipse/TM11-B.png) | NÃO EXECUTADO |
| TM12 | Captura comum para trás aceita. | APROVADO | [APROVADO](evidencias-eclipse/TM12.png) | NÃO EXECUTADO |
| TM13 | Sequência de uma captura rejeitada; sequência de duas aceita. | APROVADO | APROVADO — [A](evidencias-eclipse/TM13-A.png), [B](evidencias-eclipse/TM13-B.png), [C](evidencias-eclipse/TM13-C.png) | NÃO EXECUTADO |
| TM14 | Peça em B8 promovida a dama branca. | APROVADO | [APROVADO](evidencias-eclipse/TM14.png) | NÃO EXECUTADO |
| TM15 | Dama deslocada de C3 a F6. | APROVADO | [APROVADO](evidencias-eclipse/TM15.png) | NÃO EXECUTADO |
| TM16 | Dama deslocada para trás de F6 a C3. | APROVADO | [APROVADO](evidencias-eclipse/TM16.png) | NÃO EXECUTADO |
| TM17 | Dama não atravessa peça própria em E5. | APROVADO | [APROVADO](evidencias-eclipse/TM17.png) | NÃO EXECUTADO |
| TM18 | Última preta capturada, vitória branca, novo movimento rejeitado. | APROVADO | APROVADO — [A](evidencias-eclipse/TM18-A.png), [B](evidencias-eclipse/TM18-B.png) | NÃO EXECUTADO |
| TM19 | Falta de movimentos detectada ao carregar; vitória preta. | APROVADO | [APROVADO](evidencias-eclipse/TM19.png) | NÃO EXECUTADO |
| TM20 | Arquivo gravado com nomes, estado e turno preservados. | APROVADO | [APROVADO](evidencias-eclipse/TM20.png) | NÃO EXECUTADO |
| TM21 | Outra instância do console recupera arquivo e permite continuar. | APROVADO | APROVADO — [A](evidencias-eclipse/TM21-A.png), [B](evidencias-eclipse/TM21-B.png), [C](evidencias-eclipse/TM21-C.png) | NÃO EXECUTADO |
| TM22 | Arquivo inexistente não substitui a partida ativa. | APROVADO | [APROVADO](evidencias-eclipse/TM22.png) | NÃO EXECUTADO |
| TM23 | Arquivo inválido não substitui a partida ativa. | APROVADO | [APROVADO](evidencias-eclipse/TM23.png) | NÃO EXECUTADO |
| TA01 | Comando desconhecido gera erro e preserva partida. | APROVADO | [APROVADO](evidencias-eclipse/TA01.png) | NÃO EXECUTADO |
| TA02 | MOVER sem coordenadas gera erro e preserva partida. | APROVADO | [APROVADO](evidencias-eclipse/TA02.png) | NÃO EXECUTADO |
| TA03 | Casa clara rejeitada. | APROVADO | [APROVADO](evidencias-eclipse/TA03.png) | NÃO EXECUTADO |
| TA04 | Origem sem peça rejeitada. | APROVADO | [APROVADO](evidencias-eclipse/TA04.png) | NÃO EXECUTADO |
| TA05 | Movimento comum para trás sem captura rejeitado. | APROVADO | [APROVADO](evidencias-eclipse/TA05.png) | NÃO EXECUTADO |
| TA06 | Console rejeita movimento após vitória. | APROVADO | [APROVADO](evidencias-eclipse/TA06.png) | NÃO EXECUTADO |
| TA07 | Arquivo vazio rejeitado sem substituir a partida. | APROVADO | [APROVADO](evidencias-eclipse/TA07.png) | NÃO EXECUTADO |
| TA08 | Comandos e coordenadas minúsculas reconhecidos. | APROVADO | [APROVADO](evidencias-eclipse/TA08.png) | NÃO EXECUTADO |
| TA09 | Salvar durante sequência rejeitado; conteúdo de arquivo anterior preservado. | APROVADO | APROVADO — [A](evidencias-eclipse/TA09-A.png), [B](evidencias-eclipse/TA09-B.png), [C](evidencias-eclipse/TA09-C.png) | NÃO EXECUTADO |
| TA10 | Nova partida após vitória reinicia peças, turno e status. | APROVADO | APROVADO — [A](evidencias-eclipse/TA10-A.png), [B](evidencias-eclipse/TA10-B.png) | NÃO EXECUTADO |

## Casos adicionais automatizados

| Caso | Verificação |
| --- | --- |
| EX01 | Lei da maioria entre peças diferentes e obrigação de continuar com a mesma peça. |
| EX02 | Escolha livre entre sequências com quantidade máxima empatada. |
| EX03 | Capturados bloqueiam a dama e não podem ser recapturados. |
| EX04 | Todas as casas de aterrissagem empatadas da dama são aceitas. |
| EX05 | Aterrissagem escolhida deve permitir a maior sequência futura. |
| EX06 | Passar pela linha de promoção não promove; a peça ainda não voa. |
| EX07 | Terminar captura na última linha promove. |
| EX08 | Movimento, promoção e passagem pela última linha das pretas. |
| EX09 | Vitória preta por eliminação. |
| EX10 | Dama não atravessa duas adversárias nem aliada. |
| EX11 | Captura em outra peça também torna o movimento simples proibido. |
| EX12 | Persistência preserva damas, nomes com espaços e acentos, turno e vitória. |
| EX13 | Versão, turno, status, nome, símbolo, casa clara, linhas, rodapé e terminal inconsistentes são rejeitados. |
| EX14 | Falha de leitura de diretório e escrita em pasta inexistente não encerra o console. |
| EX15 | Comandos incompletos, excesso de argumentos, operação sem partida e EOF. |
| EX16 | Caminho de arquivo com espaços e letras maiúsculas é preservado. |
| EX17 | Lei da maioria continua obrigatória após uma etapa comum a várias sequências. |
| EX18 | Peça preta também captura para trás. |
| EX19 | Carregamento rejeita comuns em linha de promoção e tabuleiro vazio. |
| EX20 | Sequência em circuito permite retornar à origem, sem recapturar peças. |
| EX21 | Arquivos com UTF-8 inválido ou tamanho acima de 16 KiB são rejeitados, preservando a partida. |
| EX22 | Arquivos com quebras de linha CRLF são carregados corretamente. |
| EX23 | Falha ao salvar sobre diretório preserva sentinela e não deixa arquivos temporários. |
| EX24 | Delimitadores de ESTADO ocupam linhas exatas, com oito linhas de oito símbolos entre eles. |

Resultado desta suíte: **57 casos aprovados, zero reprovados**. Cada caso pode conter várias verificações; a contagem é de casos nomeados, não de asserções.

## Como repetir a automação

No Eclipse, execute `testes.TestesJogo` com **Run As > Java Application**, com diretório de trabalho na raiz de `JogoDamas`.

Pelo terminal, na raiz do projeto (JDK 9 ou superior):

```text
javac --release 8 -encoding UTF-8 -d bin @fontes-producao.txt @fontes-testes.txt
java -cp bin testes.TestesJogo
```

Com JDK 8, troque `--release 8` por `-source 1.8 -target 1.8`. A aplicação principal não precisa da suíte para funcionar.

## Problemas identificados e limites

Durante a preparação, um cenário de teste extra das pretas usava uma casa clara. O próprio validador rejeitou o cenário; as coordenadas foram corrigidas antes da execução final.

Ao final da operação da interface, a ferramenta de automação excedeu seu tempo de espera durante TA09/TA10. As capturas já produzidas foram preservadas e visualizadas; TA10 foi repetido sequencialmente após a retomada da operação, com o Eclipse em foco confirmado por uma captura do ambiente. Os resultados foram confirmados e não foi observado defeito do jogo. O timeout pertence à ferramenta que operava a interface e não é registrado como falha da aplicação.

Durante o encerramento posterior aos testes, o log da IDE registrou `SWTException: Invalid thread access` no plug-in `org.eclipse.ui.console`, às 22:13:30. A ocorrência pertence à notificação do console da IDE; essa evidência não apresenta exceção de `aplicacao.Main`. O [log preservado](evidencias-eclipse/eclipse.log) e a [nota de ambiente](evidencias-eclipse/ambiente.txt) permitem conferir a ocorrência sem atribuí-la ao jogo.

Nenhum defeito funcional ficou conhecido após a suíte e a validação no Eclipse. Isso não prova ausência de todos os defeitos possíveis. Permanecem pendentes a execução humana dos testes, o ensaio da apresentação e o preenchimento da identificação dos integrantes.

## Registro da execução humana

Responsável pela execução pessoal: ____________________

Versão do Eclipse/JDK e sistema operacional utilizados pela pessoa: ____________________

Data da execução pessoal: ____________________

Observações ou divergências: ____________________
