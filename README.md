#define ledPin 13

int velRuedas = 70;
int velPinza  = 60;

void setup() {
  motorSpeed(M1, velRuedas);
  motorSpeed(M2, velRuedas);
  motorSpeed(M3, velPinza);
  Serial.begin(9600);
  Serial1.begin(9600);
  pinMode(ledPin, OUTPUT);
  Serial.println("Innobot - Agarrar objetos");
  detenerTodo();
}

void loop() {
  if (Serial1.available()) {
    delay(2);
    int comando = Serial1.read();
    Serial.print("Comando recibido: ");
    Serial.println((char)comando);
    ejecutar(comando);
  }
}

void ejecutar(int c) {
  switch (c) {
    case 'E': digitalWrite(ledPin, HIGH); goForward(M1, M2); break;
    case 'G': digitalWrite(ledPin, HIGH); goReverse(M1, M2); break;
    case 'H': digitalWrite(ledPin, HIGH); turnLeft(M2, M1);  break;
    case 'F': digitalWrite(ledPin, HIGH); turnRight(M2, M1); break;
    case 'B': digitalWrite(ledPin, HIGH); motorOn(M3, FORWARD); break;
    case 'D': digitalWrite(ledPin, HIGH); motorOn(M3, REVERSE); break;
    case 'A': myTone(La5, blanca); myTone(Fa5, blanca); break;
    case 'C': myTone(Si5, blanca); myTone(Do5, blanca); break;
    default:  detenerTodo(); break;
  }
}

void detenerTodo() {
  motorsOff(M1, M2);
  motorOff(M3);
  digitalWrite(ledPin, LOW);
}
