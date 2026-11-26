# Roteiro de reprodução no console do Eclipse

Abra `aplicacao.Main` com **Run As > Java Application**. Use uma execução nova quando indicado e copie os comandos, uma linha por vez. Os caminhos abaixo são relativos à pasta raiz `JogoDamas`; confira **Run Configurations > Arguments > Working directory** se o Eclipse usar outro diretório. Após cada tentativa inválida, use `ESTADO` para comparar tabuleiro e turno com o estado anterior.

Os arquivos em `cenarios/` foram preparados exclusivamente para os testes, mantendo vazias as casas não indicadas. Alguns contêm uma peça preta extra em H8 ou H6 para que a partida continue após a captura testada. Essas peças não participam da jogada. O cenário TM19 contém uma branca em A7 e uma preta em B8, bloqueando a única saída da branca.

## TM01 a TM08: início e movimentação

| Teste | Comandos, em ordem | Resultado a conferir |
| --- | --- | --- |
| TM01 | `NOVO Ana Pedro`; `ESTADO` | Oito linhas de oito caracteres, 12 peças de cada cor, A1 escura; turno BRANCAS e status EM_ANDAMENTO. |
| TM02 | `NOVO Ana Pedro`; `MOVER A3 B4`; `ESTADO` | A3 vazia, branca em B4, turno PRETAS. |
| TM03 | `NOVO Ana Pedro`; `MOVER A3 C3`; `ESTADO` | Erro de movimento; nenhuma alteração. |
| TM04 | `NOVO Ana Pedro`; `MOVER A3 C1`; `ESTADO` | Destino ocupado; nenhuma alteração. |
| TM05 | `NOVO Ana Pedro`; `MOVER B6 A5`; `ESTADO` | Peça adversária rejeitada; turno BRANCAS. |
| TM06 | `NOVO Ana Pedro`; `MOVER A3 Z9`; `ESTADO` | Coordenada inválida; aplicação continua e estado permanece igual. |
| TM07 | `NOVO Ana Pedro`; `MOVER A3 B4`; `MOVER B6 A5`; `ESTADO` | Branca em B4, preta em A5, turno BRANCAS. |
| TM08 | `NOVO Ana Pedro`; `MOVER A3 B4`; `MOVER C3 D4`; `ESTADO` | Segunda jogada rejeitada; somente B4 foi movimentada; turno PRETAS. |

## TM09 a TM19: cenários preparados

| Teste | Comandos, em ordem | Resultado a conferir |
| --- | --- | --- |
| TM09 | `CARREGAR testes/cenarios/tm09-captura-simples.txt`; `MOVER C3 E5`; `ESTADO` | Branca em E5, D4 vazia, turno PRETAS. |
| TM10 | `CARREGAR testes/cenarios/tm10-captura-obrigatoria.txt`; `MOVER C3 B4`; `ESTADO` | Movimento simples rejeitado porque existe captura; C3 e turno preservados. |
| TM11 | `CARREGAR testes/cenarios/tm11-captura-multipla.txt`; `MOVER C3 E5`; `ESTADO`; `MOVER E5 G7`; `ESTADO` | Após primeiro salto: turno BRANCAS e D4 ainda ocupada, bloqueando a trajetória. Após segundo: D4 e F6 vazias, branca em G7, turno PRETAS. |
| TM12 | `CARREGAR testes/cenarios/tm12-captura-tras.txt`; `MOVER E5 C3`; `ESTADO` | Captura para trás aceita, D4 vazia, turno PRETAS. |
| TM13 | `CARREGAR testes/cenarios/tm13-maior-captura.txt`; `MOVER C3 A5`; `ESTADO`; `MOVER C3 E5`; `MOVER E5 G7`; `ESTADO` | Primeira opção captura só uma e é rejeitada. Sequência de duas aceita; preta de B4 permanece. |
| TM14 | `CARREGAR testes/cenarios/tm14-promocao.txt`; `MOVER A7 B8`; `ESTADO` | B8 contém `B`, dama branca. |
| TM15 | `CARREGAR testes/cenarios/tm15-dama-longa.txt`; `MOVER C3 F6`; `ESTADO` | Dama branca em F6 e C3 vazia. |
| TM16 | `CARREGAR testes/cenarios/tm16-dama-tras.txt`; `MOVER F6 C3`; `ESTADO` | Dama branca em C3 e F6 vazia. |
| TM17 | `CARREGAR testes/cenarios/tm17-dama-bloqueada.txt`; `MOVER C3 F6`; `ESTADO` | Dama não atravessa aliada em E5; estado preservado. |
| TM18 | `CARREGAR testes/cenarios/tm18-eliminacao.txt`; `MOVER C3 E5`; `ESTADO`; `MOVER E5 F6` | VITORIA_BRANCAS e movimento posterior rejeitado. |
| TM19 | `CARREGAR testes/cenarios/tm19-sem-movimentos.txt`; `ESTADO`; `MOVER A7 B8` | Vitória PRETAS já no carregamento; movimento rejeitado. |

## TM20 a TM23: arquivos

| Teste | Comandos, em ordem | Resultado a conferir |
| --- | --- | --- |
| TM20 | `NOVO Ana Pedro`; `MOVER A3 B4`; `SALVAR partidas/teste-manual.txt` | Arquivo criado com Ana, Pedro, turno PRETAS e branca em B4. |
| TM21 | `SAIR`; execute Main novamente; `CARREGAR partidas/teste-manual.txt`; `ESTADO`; `MOVER B6 A5`; `ESTADO` | Recuperação em outra execução; nomes e estado preservados; preta consegue jogar e turno passa a BRANCAS. |
| TM22 | `NOVO Ana Pedro`; `CARREGAR testes/cenarios/arquivo-inexistente.txt`; `ESTADO` | Erro de leitura, partida inicial preservada; aplicação continua. Não crie esse arquivo. |
| TM23 | `NOVO Ana Pedro`; `MOVER A3 B4`; `CARREGAR testes/cenarios/tm23-invalido.txt`; `ESTADO` | Arquivo inválido rejeitado; branca permanece em B4 e turno PRETAS. |

## TA01 a TA10: robustez

| Teste | Comandos, em ordem | Resultado a conferir |
| --- | --- | --- |
| TA01 | `NOVO Ana Pedro`; `ABRACADABRA`; `ESTADO` | Comando desconhecido rejeitado; aplicação continua. |
| TA02 | `NOVO Ana Pedro`; `MOVER`; `ESTADO` | Faltam coordenadas; estado preservado. |
| TA03 | `NOVO Ana Pedro`; `MOVER A3 A4`; `ESTADO` | Casa clara rejeitada. |
| TA04 | `NOVO Ana Pedro`; `MOVER C5 D6`; `ESTADO` | Origem vazia rejeitada. |
| TA05 | `CARREGAR testes/cenarios/ta05-comum-tras.txt`; `MOVER C3 B2`; `ESTADO` | Comum não anda para trás sem captura. |
| TA06 | Repita TM18 e tente `MOVER E5 F6`; `ESTADO` | Movimento após vitória rejeitado, estado terminal preservado. |
| TA07 | `NOVO Ana Pedro`; `CARREGAR testes/cenarios/ta07-vazio.txt`; `ESTADO` | Arquivo vazio rejeitado; partida preservada. |
| TA08 | `novo Ana Pedro`; `mover a3 b4`; `estado` | Comandos e coordenadas minúsculos reconhecidos. |
| TA09 | `CARREGAR testes/cenarios/tm11-captura-multipla.txt`; `MOVER C3 E5`; `SALVAR partidas/meio-sequencia.txt`; `ESTADO`; `MOVER E5 G7`; `ESTADO` | Salvamento rejeitado durante sequência, sem alteração da partida nem criação/substituição do arquivo. Segunda captura continua normalmente. |
| TA10 | Repita TM18; `NOVO Clara Beto`; `ESTADO` | Novo tabuleiro, 24 peças, turno BRANCAS, status EM_ANDAMENTO. |

## Demonstrações adicionais das regras difíceis

- **Maioria global:** carregue `extra-maioria-global.txt`. `MOVER A5 C7` é rejeitado; `MOVER C3 E5` seguido de `MOVER E5 G7` é aceito. Uma peça não pode ignorar a sequência maior disponível em outra.
- **Capturados bloqueiam:** carregue `extra-bloqueio-capturadas.txt`. Faça `MOVER C3 E5`; tente `MOVER E5 A1` (rejeitado porque D4 permanece bloqueada); conclua com `MOVER E5 G7`. A preta de B2 permanece.
- **Passagem pela última linha:** carregue `extra-promocao-passagem.txt`. Faça `MOVER B6 D8`, veja `b` em D8; `MOVER D8 G5` é rejeitado; conclua `MOVER D8 F6`. A peça continua comum porque terminou fora da última linha.
- **Aterrissagem da dama:** carregue `extra-dama-aterrissagem.txt`. `MOVER C3 F6` é rejeitado; `MOVER C3 E5` seguido de `MOVER E5 G3` captura duas peças.
- **Retorno à origem durante circuito:** carregue `extra-circuito.txt`. Faça `MOVER C3 E5`, `MOVER E5 G3`, `MOVER G3 E1` e `MOVER E1 C3`. Quatro peças são capturadas; retornar a uma casa desocupada anteriormente é permitido.

## Registro

Preencha as colunas de execução manual em `relatorio-testes.md` somente após observar cada caso no Eclipse. Em caso de reprovação, registre comando, resultado observado e ambiente; não troque o estado por APROVADO com base apenas nos testes automatizados.
