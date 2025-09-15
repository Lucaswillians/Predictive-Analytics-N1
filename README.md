# Predictive Analytics N1

## Alunos: Lucas Willian de Souza Serpa e Ryan Gabriel Bromati

### Dataset utilizado
**GTA San Andreas Vehicle Stats - Full Handling Data**  
Link: [https://www.kaggle.com/datasets/marcelbiezunski/gta-san-andreas-vehicle-stats-full-handling-data](https://www.kaggle.com/datasets/marcelbiezunski/gta-san-andreas-vehicle-stats-full-handling-data)

**Área de negócio**: Desenvolvimento e Design de Veículos para Games (GTA San Andreas Car Stats)  
- A Rockstar busca ajudar designers a criar novos carros que se encaixem em categorias específicas, como sedã de luxo, esportivo ou off-road.  
- O objetivo é identificar os atributos essenciais que definem o comportamento típico de cada categoria, garantindo que o novo veículo tenha a “receita” correta para seu tipo.

---

### a) Conceitue e apresente exemplos dos tipos de análise de dados

**Análise Descritiva**:
- Calcular médias de aceleração, velocidade máxima, peso e torque por categoria de veículo (sedã, esportivo, off-road) para entender padrões típicos.

**Análise Diagnóstica**:
- Investigar por que determinados veículos apresentam desempenho inferior, analisando a relação entre peso, tração e aceleração.

**Análise Preditiva**:  
- Construir um modelo para prever a categoria de um novo veículo ou sua velocidade máxima com base em atributos como peso, aceleração, torque e tração.

**Análise Prescritiva**: 
- Sugerir ajustes nos atributos de handling para que um novo veículo se encaixe corretamente em uma categoria específica, otimizando desempenho e gameplay.

---

### b) Domínio de problema (classificação ou predição)

**Domínio**: Desenvolvimento e Design de Veículos em Games – GTA San Andreas.  

**Problema de predição/classificação**:  
- **Predição**: prever a velocidade máxima de um veículo com base nos atributos de handling (peso, aceleração, torque, tração, freio, aderência, etc.).  
- **Classificação**: classificar veículos em categorias de desempenho, por exemplo:  
  1. Alto desempenho  
  2. Médio desempenho  
  3. Baixo desempenho  

**Utilidade**: auxilia designers e modders a criar veículos equilibrados e consistentes, permitindo decisões informadas sobre ajustes de atributos e garantindo experiência de gameplay adequada.

---

### c) Justificar a escolha do(s) modelo(s) NoSQL/Relacional como repositório(s) de dados

**Modelo Relacional (SQL)**:  
- Ideal para armazenar atributos estruturados, como peso, aceleração, torque, tração e categoria.  
- Facilita consultas, agregações e filtragens, por exemplo: “todos os veículos esportivos com aceleração acima de X e peso menor que Y”.  
- Permite normalizar tabelas: veículos, atributos de handling e categorias, garantindo consistência.

**Modelo NoSQL (Documentos, ex.: MongoDB)**:  
- Permite flexibilidade para armazenar atributos adicionais ou variáveis, como comentários de designers, logs de testes ou imagens de protótipos.  
- Útil para dados semiestruturados e extensões futuras sem alterar o esquema principal.

**Combinação híbrida**:  
- Usar SQL para os atributos estruturados principais e consultas rápidas.  
- Usar NoSQL para dados variáveis, logs de testes, modificações personalizadas e anotações de designers.
