# Predictive-Analytics-N1

## Alunos: Lucas Willian de Souza Serpa e Ryan Gabriel Bromati

### a) Conceitue e apresente exemplos dos tipos de análise de dados.
 Análise Descritiva: “O que aconteceu?”
Exemplo: calcular médias de aceleração, velocidades máximas, pesos de todos os veículos; ver quantos veículos de determinado tipo, quantos têm tração específica. Ex: “a média de velocidade máxima para carros esportivos é X km/h”.

Análise Diagnóstica: “Por que aconteceu?”
Exemplo: investigar por que determinados veículos têm desempenho pior — pode ser pelo peso elevado ou pela tração ruim ou baixa aceleração. Comparar atributos como aceleração vs peso para ver impactos.

Análise Preditiva: “O que pode acontecer?”
Exemplo: construir um modelo para prever a velocidade máxima de um veículo dado atributos como peso, aceleração, torque, tipo de tração, etc. Ou, classificar se um veículo pertence à categoria “alto desempenho” ou “desempenho comum”.

Análise Prescritiva: “O que deve ser feito?”
Exemplo: sugerir ajustes nos atributos de handling (em termos de jogo) para melhorar veículos — por exemplo, se quiser um carro competitivo de corrida, que atributos ajustar (menos peso, mais tração, aceleração etc.). Ou, se fosse um jogo modificado, recomendar configurações de combo de atributos para diferentes tipos (corrida, rally, off-road) para otimizar desempenho.

### b) Apresente um domínio de problema em que é requerido à AP (classificação ou predição); esse domínio 
será utilizado na N3 (atividade integrada com a disciplina Ciência de Dados).
Domínio: Jogos / Veículos de games — desempenho de veículos no ambiente do GTA San Andreas.

Problema de predição: Prever a velocidade máxima (ou outro atributo de desempenho, como aceleração) de um veículo com base em seus outros atributos do handling (peso, tração, freio, torque, aderência, etc.).

Ou problema de classificação: Classificar veículos em categorias de desempenho, por exemplo:

“Alto desempenho”

“Médio desempenho”

“Baixo desempenho”

Essa classificação poderia ser feita com base num limiar de velocidade máxima ou aceleração.

Utilidade: para modders ou desenvolvedores de jogos que queiram balancear os veículos, para jogadores que queiram escolher veículos ótimos para corridas ou missões, para análises comparativas etc.

### c) Justificar a escolha do(s) modelo(s) NoSQL/Relacional como possível(eis) repositório(s) de dados para o
domínio de problema (item b).
Modelo Relacional (SQL):

Os dados do dataset são bastante estruturados: atributos numéricos claros (peso, aceleração, etc.), tipo de veículo, características de tração/freio, etc.

O modelo relacional facilita consultas complexas, junções, agregações, filtros como “todos os veículos com peso menor que X e aceleração maior que Y” — SQL é bom para isso.

Se quisermos manter versões históricas ou versões distintas (por exemplo, ajustes de handling ao longo do tempo), podemos ter tabelas normalizadas: veículos, atributos de handling, categorias, etc.

Modelo NoSQL (Documentos, ex: MongoDB):

Caso você queira flexibilidade para adicionar atributos extras no futuro (por exemplo, atributos novos de modificação, atributos personalizados de modders), um modelo de documento permite que veículos tenham campos diferentes.

Também útil se quiser guardar anotações livres ou comentários de usuários sobre veículos, logs de performance ou resultados de testes que não seguem esquema fixo.

Se tiver, além dos números, imagens, metadados ricos ou dados semiestruturados é vantajoso.

Possível combinação híbrida:

Estruturar os atributos fixos via SQL para desempenho de consultas estruturadas e índices.

Guardar dados variáveis ou extensões no NoSQL.

Por exemplo, manter tabela relacional com características principais de cada veículo; usar MongoDB para armazenar coleções de logs de testes de desempenho, modificações customizadas, comparações de usuários, etc.
