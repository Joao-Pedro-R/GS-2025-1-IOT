# GS-2025-1-IOT

## Link do projeto no wokwi: https://wokwi.com/projects/432784932341371905

## 👨‍💻 Integrantes do Grupo
| Nome           | RM        |
|----------------|-----------|
| Daniel Akiyama | RM 558263 |
| Danilo Correia | RM 557540 |
| João Pedro R   | RM 558199 |

## 💻 Conceito
O projeto visa a criar um detector de chuvas fortes, enchentes, incêndios, entre outros desastres através de sensores que enviam os dados a um dashboard e avisa pessoas em volta com um buzzer que serve como alarme.

## 🏗️ Estrutura do projeto
### 🧰 Componentes utilizados
|Componente	                                  | Função                                    |
|---------------------------------------------|-------------------------------------------|
|ESP32                                        | Microcontrolador Wi-Fi                    |
|BME280	                                      | Medição de pressão, temperatura, umidade  |
|Sensor ultrassônico HC-SR04 (ou JSN-SR04T)	  | Nível da água (distância até a superfície)|
|Buzzer ou LED	                              | Alarme local                              |
|MQ2                                          | Detecção de fumaças e gases               |
|Conexão Wi-Fi                	              | Para enviar alertas remotos               |

### 🧠 Pinos usados (modificáveis):
|Função	                |Pino ESP32        |
|-----------------------|------------------|
|BME280 (I2C)	          |SDA = 21, SCL = 22|
|Trigger Ultrassônico	  |GPIO 12           |
|Echo Ultrassônico	    |GPIO 14           |
|Buzzer / LED de alarme	|GPIO 27           |

![image](https://github.com/user-attachments/assets/533cbaa6-841b-4fe0-a9eb-21ed49b0098e)

### 📚 Bibliotecas
| Library Name      | Purpose                                                          |
| ----------------- | ---------------------------------------------------------------- |
| `Wire`            | I2C communication (built-in, used for BME280 sensor)             |
| `Adafruit_Sensor` | Adafruit’s unified sensor interface (required for BME280)        |
| `Adafruit_BME280` | For reading temperature, humidity, and pressure from BME280      |
| `WiFi`            | To connect the ESP32 to a Wi-Fi network                          |
| `PubSubClient`    | For connecting to and publishing/subscribing with an MQTT broker |

### 🔁 Fluxo resumido do projeto:

#### Previsão de chuva →
Detectar queda súbita na pressão →
Umidade > 85% →
Temperatura entre 18–30 °C →
→ Mostrar “Alta chance de chuva”

#### Alerta de enchente →
Sensor ultrassônico mede nível da água (altura < X cm) →
Se abaixo do limite → disparar alarme

### ✅ Funções do sistema
#### 📈 Previsão de chuva com BME280:
Mede pressão, umidade e temperatura, alerta se houver alta probabilidade de chuva

#### 🌊 Detecção de enchente com sensor ultrassônico (HC-SR04 ou JSN-SR04T):
Mede distância até a superfície da água, aciona buzzer ou LED se água subir acima do nível crítico

## ✅ Vantagens de incluir o MQ-2 no projeto
- Complementa o sistema de alarme
- Detecta fumaça de incêndios florestais ou urbanos
- Pode funcionar como alarme precoce em áreas remotas

### 🔥 Quando é útil o MQ-2 nesse projeto?
|Situação	                            |Benefício do MQ-2            |  
|-------------------------------------|-----------------------------|
|Queimadas perto de áreas urbanas	    |Alerta precoce de fumaça     |
|Regiões de mata com seca extrema	    |Detecta fumaça/sinais de fogo|
|Ambientes internos (abrigos, caixas)	|Alerta de fumaça por curto   |

## 📋 Resultado no Dashboard MQTT

|Tópico                  |	Mensagem                                       |
|------------------------|-------------------------------------------------|
|esp32/sensores/gas      |	"GAS DETECTADO" ou "Nivel normal"              |
|esp32/sensores/enchente |	"RISCO DE ENCHENTE" ou "Nivel normal"          |
|esp32/sensores/clima    |	Ex: "Temp:24.87 Umid:48.22 Press:1010.12 Niv:17 MQ2:351" |

![image](https://github.com/user-attachments/assets/b1dd16ac-f042-40a5-8020-94d19f46e7d6)

![image](https://github.com/user-attachments/assets/8e2f2239-7c7f-4719-97db-4c92750e65a7)
