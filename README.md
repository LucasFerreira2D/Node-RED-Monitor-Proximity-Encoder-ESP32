# Node-RED-Monitor-Proximity-Encoder-ESP32

## 1. Visão Geral
Este projeto utiliza Node-RED para monitorar e visualizar dados de proximidade e giroscópio obtidos de um ESP32. Os dados são recebidos via protocolo MQTT e armazenados em um banco de dados PostgreSQL. Além disso, um dashboard é configurado para visualizar os dados em tempo real.

## 2. Pré-requisitos
1. Node-RED instalado em um ambiente configurado.
2. MQTT Broker (ex.: broker.hivemq.com).
3. Banco de dados PostgreSQL configurado.
4. Conexão com um ESP32 com sensores de proximidade e giroscópio.
5. Node-RED Dashboard configurado para visualizar os dados.

## 3. Descrição do Fluxo
![image](https://github.com/user-attachments/assets/d3b5bbd4-02ef-42f2-8e4f-ddc831c0a632)

## 4. GETs para o Android
1. **GET /proximidade**: Retorna os últimos 10 registros do sensor de proximidade.
2. **GET /giro**: Retorna os últimos 10 registros do sensor de giroscópio.
3. **GET /monitoramento**: Retorna o status do sistema.

## 5. Proximidade
1. Recebe os dados de proximidade do ESP32 via MQTT.
2. Processa os dados e insere no banco de dados PostgreSQL.
3. Exibe os dados em um gauge e em uma tabela no dashboard.

## 6. Giro
1. Recebe os dados do giroscópio do ESP32 via MQTT.
2. Processa os dados e insere no banco de dados PostgreSQL.
3. Exibe os dados em um compass (bússola) e em uma tabela no dashboard.

## 7. Estrutura de Dados
![image](https://github.com/user-attachments/assets/236af385-a9c5-41b0-b4ec-144781682c97)

## 8. Instalação e Configuração
1. Clone o repositório do seu projeto Node-RED.
2. Importe o fluxo no Node-RED através da opção de importação.
3. Certifique-se de que os nós MQTT estão configurados corretamente para se conectar ao seu broker.

## 9. Configuração do MQTT
1. **Broker**: broker.hivemq.com
2. **Porta**: 1883
3. **Tópicos**:
   - **ESP32_PROXIMIDADE_IOT_IFSP**: Tópico para receber dados de proximidade.
   - **ESP32_GIRO_IOT_IFSP**: Tópico para receber dados de giroscópio.

## 10. Configuração do PostgreSQL
Certifique-se de que o PostgreSQL está configurado com as tabelas necessárias:

```sql
CREATE TABLE SENSOR_PROXIMIDADE (
    id SERIAL PRIMARY KEY,
    valor FLOAT NOT NULL,
    data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE SENSOR_GIRO (
    id SERIAL PRIMARY KEY,
    valor FLOAT NOT NULL,
    data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- **Host**: IP_DO_BANCO
- **Porta**: 5432 (Padrão)
- **Usuário**: SEU_USUÁRIO
- **Senha**: SUA_SENHA
- **Banco de dados**: SEU_BANCO

## 11. Dashboard
O projeto inclui um dashboard para visualização em tempo real dos dados de proximidade e giroscópio. Ele está dividido em duas partes principais:
1. **Proximidade**: Gauge e tabela mostrando os valores mais recentes do sensor de proximidade.
2. **Giro**: Compass (bússola) e tabela mostrando os valores mais recentes do sensor de giroscópio.

### 11.1. Acessando o Dashboard
Acesse o dashboard do Node-RED em: `http://<IP_do_Node-RED>:1880/ui`.

## 12. Endpoints HTTP
1. **GET /proximidade**: Retorna os últimos 10 registros de proximidade no formato JSON.
2. **GET /giro**: Retorna os últimos 10 registros de giroscópio no formato JSON.
3. **GET /monitoramento**: Retorna o status do sistema com a mensagem de monitoramento.

## 13. Exemplo de Resposta JSON
### 13.1. GET /proximidade:
![image](https://github.com/user-attachments/assets/2ff873e0-9711-41b3-8ff1-54891d8d10d2)

```json
{
    "proximidade": [
        {
            "id": 1,
            "valor": 12.5,
            "data_hora": "08/10/2024 10:30:45"
        },
        {
            "id": 2,
            "valor": 13.0,
            "data_hora": "08/10/2024 10:31:00"
        }
    ]
}
```

### 13.2. GET /giro:
![image](https://github.com/user-attachments/assets/4398912e-4b3c-4322-881f-24bd134aa956)

```json
{
    "giro": [
        {
            "id": 1,
            "valor": 1,
            "data_hora": "08/10/2024 10:30:45"
        },
        {
            "id": 2,
            "valor": 2,
            "data_hora": "08/10/2024 10:31:00"
        }
    ]
}
```

## 14. Funcionalidades
1. **Monitoramento de Sensores**: Recebe e processa dados de sensores de proximidade e giroscópio.
2. **Armazenamento em Banco de Dados**: Armazena os valores em tabelas do PostgreSQL.
3. **Visualização de Dados**: Exibe os dados em tempo real através do Node-RED Dashboard.
4. **Integração com MQTT**: Conecta-se a um broker MQTT para receber dados dos sensores.
