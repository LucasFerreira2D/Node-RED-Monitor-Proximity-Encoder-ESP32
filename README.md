# Node-RED-Monitor-Proximity-Encoder-ESP32
Node-RED Monitor Proximity Encoder ESP32 

**Visão Geral**
Este projeto utiliza Node-RED para monitorar e visualizar dados de proximidade e giroscópio obtidos de um ESP32. Os dados são recebidos via protocolo MQTT e armazenados em um banco de dados PostgreSQL. Além disso, um dashboard é configurado para visualizar os dados em tempo real.

Pré-requisitos
* Node-RED instalado em um ambiente configurado.
* MQTT Broker (ex.: broker.hivemq.com).
* Banco de dados PostgreSQL configurado.
* Conexão com um ESP32 com sensores de proximidade e giroscópio.
* Node-RED Dashboard configurado para visualizar os dados.

**Descrição do Fluxo**

![image](https://github.com/user-attachments/assets/d3b5bbd4-02ef-42f2-8e4f-ddc831c0a632)

**GETS para o android:**

* GET /proximidade: Retorna os últimos 10 registros do sensor de proximidade.
* GET /giro: Retorna os últimos 10 registros do sensor de giroscópio.
* GET /monitoramento: Retorna o status do sistema.

**Proximidade:**

* Recebe os dados de proximidade do ESP32 via MQTT.
* Processa os dados e insere no banco de dados PostgreSQL.
* Exibe os dados em um gauge e em uma tabela no dashboard.
  
**Giro:**

* Recebe os dados do giroscópio do ESP32 via MQTT.
* Processa os dados e insere no banco de dados PostgreSQL.
* Exibe os dados em um compass (bússola) e em uma tabela no dashboard.

**Estrutura de Dados**

![image](https://github.com/user-attachments/assets/236af385-a9c5-41b0-b4ec-144781682c97)


**Instalação e Configuração**

* Clone o repositório do seu projeto Node-RED.
* Importe o fluxo no Node-RED através da opção de importação.
* Certifique-se de que os nós MQTT estão configurados corretamente para se conectar ao seu broker.

**Configuração do MQTT**

* Broker: broker.hivemq.com
* Porta: 1883
* Tópicos:
    * ESP32_PROXIMIDADE_IOT_IFSP: Tópico para receber dados de proximidade.
    * ESP32_GIRO_IOT_IFSP: Tópico para receber dados de giroscópio.


**Configuração do PostgreSQL**

Certifique-se de que o PostgreSQL está configurado com as tabelas necessárias:

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

* Host: IP_DO_BANCO
* Porta: 5432 (Padrão)
* Usuário: SEU_USUÁRIO
* Senha: SUA_SENHA
* Banco de dados: SEU_BANCO

**Dashboard**

O projeto inclui um dashboard para visualização em tempo real dos dados de proximidade e giroscópio. Ele está dividido em duas partes principais:

* Proximidade: Gauge e tabela mostrando os valores mais recentes do sensor de proximidade.
* Giro: Compass (bússola) e tabela mostrando os valores mais recentes do sensor de giroscópio.

Acessando o Dashboard
Acesse o dashboard do Node-RED em: http://<IP_do_Node-RED>:1880/ui.

Endpoints HTTP
* GET /proximidade: Retorna os últimos 10 registros de proximidade no formato JSON.
* GET /giro: Retorna os últimos 10 registros de giroscópio no formato JSON.
* GET /monitoramento: Retorna o status do sistema com a mensagem de monitoramento.

**Exemplo de Resposta JSON**

GET /proximidade:


![image](https://github.com/user-attachments/assets/2ff873e0-9711-41b3-8ff1-54891d8d10d2)


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

GET /giro:

![image](https://github.com/user-attachments/assets/4398912e-4b3c-4322-881f-24bd134aa956)

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

**Funcionalidades**

* Monitoramento de Sensores: Recebe e processa dados de sensores de proximidade e giroscópio.
* Armazenamento em Banco de Dados: Armazena os valores em tabelas do PostgreSQL.
* Visualização de Dados: Exibe os dados em tempo real através do Node-RED Dashboard.
* Integração com MQTT: Conecta-se a um broker MQTT para receber dados dos sensores.

