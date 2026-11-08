# Sabença: dados da pesquisa com estudantes

Dados e resultados da pesquisa apresentada no Trabalho de Conclusão de Curso "Desenvolvimento de uma plataforma web para comunidades acadêmicas: a credencial acadêmica validada como sinal de confiança em redes locais de negociação", de Kauan Moreira e Samuel Sampaio Lins (Ciência da Computação, FATECE, 2026).

A pesquisa foi aplicada em 26 e 27 de outubro de 2026 por meio de formulário on-line, em duas versões (A e B) que diferem apenas pela ordem dos anúncios. As respostas são anônimas: o formulário não coletou nome, e-mail ou qualquer dado que permita identificar os participantes.

## Estrutura

```
dados/
  dados_pesquisa.csv          respostas organizadas por condição (31 linhas)
resultados_jasp/
  tabelas4_5_analise_principal.html
  tabela6_primeiro_anuncio_e_efeito_de_ordem.html
  tabela6_sensibilidade_checagem_correta.html
  tabela7_versao_A.html
  tabela7_versao_B.html
  tabela7_ciencia_da_computacao.html
  tabela7_pedagogia.html
  alfa_cronbach_com_credencial.html
  alfa_cronbach_sem_credencial.html
```

Os arquivos da pasta `resultados_jasp` são as saídas exportadas do JASP 0.98.1. O número no nome de cada arquivo indica a tabela do Apêndice A que ele sustenta.

## Colunas do arquivo de dados

| Coluna | Descrição |
|---|---|
| participante | Número sequencial da resposta |
| versao | Versão do formulário: A (primeiro anúncio sem credencial) ou B (primeiro anúncio com credencial) |
| valida | 1 = resposta incluída na análise; 0 = excluída por não atender ao critério de inclusão |
| curso | Curso informado, padronizado |
| semestre | Faixa de semestre informada |
| sem_conhecimento, com_conhecimento | Nota de 1 a 5 para "Esta pessoa tem conhecimento técnico para realizar o serviço bem feito", no anúncio sem e com credencial |
| sem_seguranca, com_seguranca | Nota de 1 a 5 para "Eu me sentiria seguro para negociar com esta pessoa" |
| sem_intencao, com_intencao | Nota de 1 a 5 para "Eu entraria em contato com esta pessoa se precisasse deste serviço" |
| sem_indice, com_indice | Média dos três itens em cada anúncio (arredondada, usada apenas para estatística descritiva) |
| sem_soma, com_soma | Soma dos três itens em cada anúncio (usada nos testes do índice geral) |
| diferenca_soma | com_soma menos sem_soma |
| primeiro_anuncio_soma | Soma dos três itens no primeiro anúncio visto pelo participante |
| checagem_correta | 1 = acertou em qual anúncio aparecia a formação do anunciante; 0 = errou |
| comprou_de_colega | Frequência com que já comprou ou contratou de um colega |
| precisou_sem_saber | Frequência com que já precisou de um serviço sem saber a quem recorrer |
| oferece | Se oferece ou já ofereceu produtos ou serviços por conta própria |

## Como reproduzir no JASP

1. Abra `dados/dados_pesquisa.csv` no JASP 0.98.1 e filtre `valida` = 1 (30 respostas).
2. Análise principal: T-Tests > Paired Samples T-Test, com os pares `com_` × `sem_` de cada item e `com_soma` × `sem_soma`, testes Student e Wilcoxon signed-rank, bilaterais, com tamanho de efeito.
3. Primeiro anúncio e efeito de ordem: T-Tests > Independent Samples T-Test, com `primeiro_anuncio_soma` e `diferenca_soma` agrupados por `versao`, teste de Mann-Whitney.
4. Sensibilidade: repetir o par `com_soma` × `sem_soma` filtrando também `checagem_correta` = 1.
5. Subgrupos: repetir o par `com_soma` × `sem_soma` filtrando por `versao` ou por `curso`.
6. Consistência interna: Reliability, alfa de Cronbach dos três itens `com_` e dos três itens `sem_`.
