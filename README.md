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
### 🧰 Componentes sugeridos
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

![image](https://github.com/user-attachments/assets/b1dd16ac-f042-40a5-8020-94d19f46e7d6)

![image](https://github.com/user-attachments/assets/8e2f2239-7c7f-4719-97db-4c92750e65a7)

🌦️ 1. Previsão de chuvas fortes
Com base em:

Pressão atmosférica e umidade relativa

Com sensor BME280 (ideal para isso)

🌊 2. Detecção de enchente/local alagado
Com:

Sensor de nível d’água (ultrassônico ou boia de nível)

Medição contínua da altura da água

📋 Esquema geral do projeto
ESP32 conectado a:

BME280 via I2C (SDA/SCL)

HC-SR04: Trigger e Echo em dois pinos GPIO

Buzzer/LED: Alerta em caso de nível crítico

Opcional: enviar alerta por Wi-Fi / Telegram / MQTT

💡 Lógica do sistema
Previsão de chuva:

Detectar queda súbita na pressão

Umidade > 85%

Temperatura entre 18–30 °C

→ Mostrar “Alta chance de chuva”

Alerta de enchente:

Sensor ultrassônico mede nível da água (altura < X cm)

Se abaixo do limite → disparar alarme

✅ Funções do sistema
📈 Previsão de chuva com BME280:

Mede pressão, umidade e temperatura

Alerta se houver alta probabilidade de chuva

🌊 Detecção de enchente com sensor ultrassônico (HC-SR04 ou JSN-SR04T):

Mede distância até a superfície da água

Aciona buzzer ou LED se água subir acima do nível crítico



✅ Vantagens de incluir o MQ-2 no projeto
Complementa o sistema de alarme:

Detecta fumaça de incêndios florestais ou urbanos

Pode funcionar como alarme precoce em áreas remotas

Simples de integrar:

Leitura direta com analogRead() ou digitalRead()

Não exige muita energia nem muitos pinos

Baixo custo, fácil de encontrar

🔥 Quando é útil o MQ-2 nesse projeto?
Situação	Benefício do MQ-2
Queimadas perto de áreas urbanas	Alerta precoce de fumaça
Regiões de mata com seca extrema	Detecta fumaça/sinais de fogo
Ambientes internos (abrigos, caixas)	Alerta de fumaça por curto

⚠️ Limitações
Não detecta CO₂ (gás de combustão completa)

Pode ser sensível a outros gases (álcool, GLP), então falsos positivos são possíveis

Requer calibração e um tempo de aquecimento (~24h na primeira vez)

📋 Resultado no Dashboard MQTT
Se você usar um dashboard como o MQTT Explorer, Node-RED, TagoIO, Ubidots, etc., vai ver:

Tópico	Mensagem
esp32/sensores/gas	"GAS DETECTADO" ou "Nivel normal"
esp32/sensores/enchente	"RISCO DE ENCHENTE" ou "Nivel normal"
esp32/sensores/clima	Ex: "Temp: 25.12, Umid: 64.50, Press: 1012.10"

Temp:24.87 Umid:48.22 Press:1010.12 Niv:17 MQ2:351
