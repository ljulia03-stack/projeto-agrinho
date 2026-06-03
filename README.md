# Tema do meu projeto 

Projeto desenvolvido para o concurso Agrinho. 

1. Introdução e Objetivo
O objetivo deste trabalho é aplicar a tecnologia da Internet das Coisas (IoT) na agricultura familiar para evitar o desperdício de água e monitorar a saúde das plantações. Criamos um sistema automatizado que mede a umidade do solo e avisa o agricultor se a planta precisa de rega.

2. O Circuito (Hardware com Arduino)
Este código simula ou roda em um Arduino real conectado a um sensor de umidade de solo e um display LCD (ou monitor serial) para exibir os dados.

// --- PROTÓTIPO AGRINHO: MONITOR DE UMIDADE DO SOLO ---
// Linguagem: C++ (Arduino)

const int sensorPin = A0;   // Pino analógico conectado ao sensor de umidade
const int ledPin = 13;      // LED interno do Arduino que acende se o solo estiver seco
int valorUmidade = 0;       // Variável para armazenar a leitura bruta
int porcentagemUmidade = 0; // Variável para armazenar a umidade convertida em %

void setup() {
  Serial.begin(9600);       // Inicializa a comunicação serial com o computador
  pinMode(ledPin, OUTPUT);  // Define o pino do LED como saída
}

void loop() {
  // Lê o valor do sensor (varia de 0 a 1023)
  valorUmidade = analogRead(sensorPin);
  
  // Converte o valor para uma escala de 0% (seco) a 100% (totalmente úmido)
  porcentagemUmidade = map(valorUmidade, 1023, 0, 0, 100);
  
  // Envia os dados formatados para o computador (para o sistema em Python)
  Serial.print("Umidade atual: ");
  Serial.print(porcentagemUmidade);
  Serial.println("%");
  
  // Lógica de alerta para o agricultor
  if (porcentagemUmidade < 30) {
    digitalWrite(ledPin, HIGH); // Solo muito seco! Liga alerta de irrigação
  } else {
    digitalWrite(ledPin, LOW);  // Solo ideal ou úmido. Desliga alerta
  }
  
  delay(2000); // Aguarda 2 segundos para a próxima leitura
}
3. O Painel de Controle (Software com Python)
Para que o agricultor possa ver os dados de forma visual e organizada no computador, este código em Python cria uma interface gráfica simples e gera relatórios sobre as condições do solo.

Nota: Para rodar este código, você precisará instalar a biblioteca matplotlib usando o comando pip install matplotlib no seu terminal.**
**
