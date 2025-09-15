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

---

### d) Apresentar um modelo simples passivo de ser instanciado no banco NoSQL/Relacional escolhido(s)

**Modelo NoSQL (MongoDB)**:

```javascript
// Coleção de veículos com estrutura flexível
{
  "_id": ObjectId("..."),
  "identifier": "INFERNUS",
  "basic_stats": {
    "mass_kg": 1400.0,
    "turn_mass_kg": 2725.3,
    "drag_multiplier": 1.5,
    "max_velocity_kmh": 240.0,
    "acceleration_ms2": 30.0
  },
  "handling_attributes": {
    "center_of_mass": {
      "x": 0.0,
      "y": 0.0,
      "z": -0.25,
      "submerged_percent": 70
    },
    "traction": {
      "multiplier": 0.7,
      "loss": 0.8,
      "bias_percent": 0.5
    },
    "suspension": {
      "force_level": 1.2,
      "damping_level": 0.19,
      "high_speed_com_damping": 0.0,
      "lines_upper_limit": 0.25,
      "lines_lower_limit": -0.1,
      "lines_bias_between_front_and_rear": 0.5,
      "anti_dive_multiplier": 0.4
    }
  },
  "performance_classification": {
    "predicted_category": "high_performance",
    "confidence": 0.92,
    "model_version": "v1.0"
  },
  "designer_notes": [
    {
      "author": "designer_001",
      "note": "Excellent for racing circuits",
      "timestamp": "2024-01-15T10:30:00Z"
    }
  ],
  "test_results": [
    {
      "test_type": "lap_time",
      "circuit": "downtown_race",
      "time_seconds": 120.5,
      "date": "2024-01-10"
    }
  ],
  "metadata": {
    "created_at": "2024-01-01T00:00:00Z",
    "updated_at": "2024-01-15T10:30:00Z",
    "version": 1
  }
}
```

---

### e) Mostrar exemplos de manipulação de dados no banco escolhido

**Exemplos MongoDB**:

```javascript
// 1. Inserir um novo veículo
db.vehicles.insertOne({
  "identifier": "CUSTOM_CAR",
  "basic_stats": {
    "mass_kg": 1500.0,
    "max_velocity_kmh": 200.0,
    "acceleration_ms2": 25.0
  },
  "handling_attributes": {
    "drive_type": "Rear",
    "engine_type": "Petrol"
  },
  "performance_classification": {
    "predicted_category": "medium_performance",
    "confidence": 0.85
  }
});

// 2. Consultar veículos de alto desempenho
db.vehicles.find({
  "basic_stats.max_velocity_kmh": { $gt: 200 },
  "basic_stats.acceleration_ms2": { $gt: 25 }
}).sort({ "basic_stats.max_velocity_kmh": -1 });

// 3. Agregação por tipo de tração
db.vehicles.aggregate([
  {
    $group: {
      _id: "$handling_attributes.drive_type",
      total_vehicles: { $sum: 1 },
      avg_max_velocity: { $avg: "$basic_stats.max_velocity_kmh" },
      avg_acceleration: { $avg: "$basic_stats.acceleration_ms2" }
    }
  }
]);

// 4. Atualizar classificação de desempenho
db.vehicles.updateMany(
  {
    "basic_stats.max_velocity_kmh": { $gt: 220 },
    "basic_stats.acceleration_ms2": { $gt: 28 }
  },
  {
    $set: {
      "performance_classification.predicted_category": "high_performance",
      "performance_classification.confidence": 0.95
    }
  }
);

// 5. Consulta com projeção e filtros complexos
db.vehicles.find(
  {
    "basic_stats.mass_kg": { $lt: 2000 },
    "performance_classification.confidence": { $gt: 0.8 }
  },
  {
    "identifier": 1,
    "basic_stats.max_velocity_kmh": 1,
    "performance_classification.predicted_category": 1
  }
);
```

---

### f) Escolher e justificar o ambiente que abrigará dados brutos e/ou pré-processados para alimentar os modelos de AP

**Escolha: Data Lake (MongoDB + Python)**

**Justificativa**:

1. **Simplicidade de Implementação**:
   - MongoDB é fácil de instalar e configurar
   - Ferramentas gratuitas e amplamente utilizadas
   - Documentação extensa e comunidade ativa

2. **Adequação ao Escopo**:
   - Suficiente para o dataset GTA (164 registros)
   - Flexibilidade para dados semiestruturados
   - Integração direta com Python para ML

3. **Estrutura Flexível**:
   - Dados brutos e processados em coleções separadas
   - Suporte a documentos aninhados
   - Fácil adição de novos campos sem alterar esquema

4. **Integração com ML**:
   - Bibliotecas Python (pymongo, pandas) conectam facilmente
   - Exportação direta para DataFrames
   - Ambiente Jupyter para experimentação

**Arquitetura Simplificada**:

```
Data Lake (MongoDB):
├── vehicles_raw (dados originais do CSV)
├── vehicles_cleaned (dados limpos e normalizados)
├── training_set (dados preparados para ML)
├── validation_set (dados de validação)
└── test_set (dados de teste)

Ambiente Python:
├── data_processing.py (scripts de limpeza)
├── feature_engineering.py (criação de features)
├── model_training.py (treinamento dos modelos)
└── notebooks/ (análise exploratória)
```

**Exemplo de Implementação**:

```python
# 1. Conexão com MongoDB
import pandas as pd
from pymongo import MongoClient
import json

# Conexão com banco
client = MongoClient('mongodb://localhost:27017/')
db = client['gta_analytics']

# 2. Carregar dados brutos
raw_data = pd.read_csv('gta_sa_vehicle_stats.csv')
raw_records = raw_data.to_dict('records')
db.vehicles_raw.insert_many(raw_records)

# 3. Processar e limpar dados
cleaned_data = raw_data.dropna()
cleaned_data['performance_category'] = cleaned_data['max_velocity_kmh'].apply(
    lambda x: 'high' if x > 200 else 'medium' if x > 160 else 'low'
)

# Converter para documentos MongoDB
cleaned_records = []
for _, row in cleaned_data.iterrows():
    doc = {
        'identifier': row['identifier'],
        'basic_stats': {
            'mass_kg': row['mass_(kg)'],
            'max_velocity_kmh': row['max_velocity(km/h)'],
            'acceleration_ms2': row['acceleration(ms^2)'],
            'traction_multiplier': row['traction_multiplier']
        },
        'performance_category': row['performance_category'],
        'metadata': {
            'created_at': '2024-01-01T00:00:00Z',
            'version': 1
        }
    }
    cleaned_records.append(doc)

db.vehicles_cleaned.insert_many(cleaned_records)

# 4. Preparar dados para ML
from sklearn.model_selection import train_test_split

# Extrair features do MongoDB
features_data = []
for doc in db.vehicles_cleaned.find():
    features_data.append({
        'mass_kg': doc['basic_stats']['mass_kg'],
        'acceleration_ms2': doc['basic_stats']['acceleration_ms2'],
        'traction_multiplier': doc['basic_stats']['traction_multiplier'],
        'max_velocity_kmh': doc['basic_stats']['max_velocity_kmh']
    })

ml_df = pd.DataFrame(features_data)
features = ['mass_kg', 'acceleration_ms2', 'traction_multiplier']
X = ml_df[features]
y = ml_df['max_velocity_kmh']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 5. Salvar conjuntos de treino/teste no MongoDB
train_data = pd.concat([X_train, y_train], axis=1)
test_data = pd.concat([X_test, y_test], axis=1)

train_records = train_data.to_dict('records')
test_records = test_data.to_dict('records')

db.training_set.insert_many(train_records)
db.test_set.insert_many(test_records)
```

**Vantagens desta Abordagem**:
- **Simplicidade**: Fácil de implementar e manter
- **Custo**: Ferramentas gratuitas (MongoDB + Python)
- **Flexibilidade**: Esquema flexível para diferentes tipos de dados
- **Escalabilidade**: Pode crescer conforme necessário
- **Integração**: Excelente integração com Python e Jupyter

**Desvantagens**:
- Menos otimizado para consultas analíticas complexas que SQL
- Requer mais processamento para agregações
- Curva de aprendizado para consultas MongoDB
