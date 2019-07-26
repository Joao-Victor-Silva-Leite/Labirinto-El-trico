# Labirinto-Elétrico

Um labirinto elétrico clássico, mas com adições de funções utilizando um Arduíno uno. O principal objetivo é lógicamente a diversão de quem for utilizar o Labirinto, mas também é importante ver que com esse projeto é possível ver o potencial que o Arduíno tem de criar variedade e diversificação mesmo para coisas simples como um labirinto elétrico.

# Sumário:
(para adicionar)

# 1- Lista de materiais:
(1X) Arduino UNO R3;
(1X) Módulo relé 5V;
(1X) Chave alavanca;
(1X) Buzzer 5V;
(1X) Sirene 9V ou 12V;
(2X) Borne preto para plug banana;
(1X) Borne vermelho para plug banana;
(2X) Plug banana preto;
(1X) Plug banana vermelho;
(1X) Resistor 1k (1/4W);
(1X) Resistor 220R (1/4W);
(1X) LED verde difuso 3mm;
(1X) Adaptador de clip de bateria 9V para plug P4 macho;
(1X) Bateria de 9V;
(1X - Opcional) Caixa de MDF (25cmX17cmX8cm).

# 2- Código do Arduino:
// Declaração dos pinos utilizados do Arduino
int pinoLED = 2;
int pinoLabirinto = 3;
int pinoBuzzer = 9;
int pinoSirene = 10;

// Declaração das variáveis auxiliares
int nivel = 0;
long int tempoAnterior = 0;
int deltaT = 200;
int tomBuzzer = 3000;
int estadoBotao = LOW;
int estadoBuzzer = LOW;

// A função setup é apenas executada uma vez ao se iniciar o Arduino, aqui configuramos nossa placa Arduino
void setup() {
  // Pinos configurados como entrada:
  pinMode(pinoLabirinto, INPUT_PULLUP); // Configurando a entrada como INPUT_PULLUP, utilizamos o resistor interno pull-up do Arduino
//=======  
  pinMode(pinoBotao, INPUT);

  // Pinos configurados como saída:
  pinMode(pinoBuzzer, OUTPUT);
  pinMode(pinoSirene, OUTPUT);
  digitalWrite(pinoLED, HIGH);
  digitalWrite(pinoSirene, HIGH); //noTone(pinoSirene);
  Serial.begin(9600);
}
// A função loop é executada repetitivamente até se desligar o Arduino
void loop() {

  Serial.println(nivel);
  estadoBotao = digitalRead(pinoLabirinto);
  if (estadoBotao == LOW) {
    delay(50);
    estadoBotao = digitalRead(pinoLabirinto);
    while (!digitalRead(pinoLabirinto)) {
      delay(1);
    }
    if (estadoBotao == LOW) {
      nivel = nivel + 1;
    }
  }
  if (nivel == 2) {
    deltaT = 100;
    tomBuzzer = 3500;
  }
  if (nivel == 3) {
    deltaT = 50;
    tomBuzzer = 4000;
  }
  if (nivel == 4) {
    noTone(pinoBuzzer);//digitalWrite(pinoBuzzer, LOW);
    while (1) {
      digitalWrite(pinoSirene, LOW); //tone(pinoSirene, 4000);
    }
  }
  if (((millis() - tempoAnterior) > deltaT) && (nivel >= 1)) { 
    if (estadoBuzzer) {
      tone(pinoBuzzer, tomBuzzer);
    }
    else {
      noTone(pinoBuzzer);
    }
    estadoBuzzer = !estadoBuzzer;
    tempoAnterior = millis();
  }
}

# 3- Montando o projeto:
(será adicionado posteriormente)

# 4- Usando o labirinto eletrico:
Após ligar a chave on/off o o jogo começa.
O objetivo é pegar o arame com a argola e passar pelo circuito sem tocar as partes metálicas do circuito com a argola.
O arduino foi programado para soar um alarme após 3 toques finalizando o jogo. E a cada toque anterior a este liga um buzzer que toca numa frequência cada vez mais "rápida" a cada toque.

# 5- Por que fazer o labirinto?
O labirinto elétrico por mais que não tenha nenhuma função social especifica é um brinquedo que cumpre uma das propostas iniciais do arduíno, que é a de mostrar para crianças a extenção que se cria  para diversas aréas utilizando-se da programação. Se você é um pai que tem alguma experiencia com programação, com certeza pode ser uma tarefa bem agradável para se fazer com o filho isto é, mostrar para ele como algo "chato" que é um monte de letras e números pode fazer algo divertido para se brincar. Para você que não tem experiencia alguma com programação você pode realizar este projeto apenas copiando a linha de código e adicionando ela ao arduíno. Se você é um curioso e entusiasta, você pode optar por fazer uma serie de mudanças na programação para por exemplo aumentar o número de toques. subistituir o alarme por um comando de voz, etc.

# 6- Créditos
Devo creditar primeiramente meu professor Epaminondas Lage, cujo propos este trabalho para ser feito.
Créditos ao canal Manual do Mundo onde a ideia do projeto foi retirada do video: https://www.youtube.com/watch?v=Nahbwcav8bE&list=PLYjrJH3e_wDNLUTN32WittrpBxeleEqNp&t=0s




