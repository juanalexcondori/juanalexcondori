#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>

#define SS_PIN 10      // Pin SS para el módulo RC522
#define RST_PIN 9      // Pin RST para el módulo RC522

MFRC522 r
MFRC522 rfid(SS_PIN, RST_PIN);  // Crea una instancia del lector RFID

Servo servoMotor;  

Servo servoMotor;
// Crea una instancia del servo motor



/
// UID de la tarjeta permitida (cambia estos valores con el UID de tu tarjeta)
byte tarjetaPermitida[] = {
byte tarjetaPermitida[] = {

byte tarj

byte t

byt
0xDE, 0xAD, 0xBE, 0xEF};  // Ejemplo de UID



voi
void setup() {
  Serial.
  Serial.beg

  Seri
begin(9600);      // Inicia la comunicación serial
  SPI.
  SPI.begin

 
begin();             // Inicia la comunicación SPI
  rfid.
  rfid.PCD_I

  rf
PCD_Init();         // Inicia el lector RC522
  servoMotor.
  servoMotor.att

  servoMoto

  serv
attach(7);    // Conecta el servo al pin 7
  servoMotor.write(0);     // Coloca el servo en posición cerrada (0 grados)
  Serial.
  Serial.printl

  Serial.pr

  Seri

 
println("Sistema de Seguridad Iniciado");
}

void loop() {
  
  /
// Verifica si hay una tarjeta en el rango
  if (!rfid.PICC_IsNewCardPresent() || !rfid.PICC_ReadCardSerial()) {
    return;
  }

  Serial.
  }

  Seria

  }

  Se

  }

 
print("UID de la tarjeta: ");
  bool accesoPermitido = true;

  // Compara la UID leída con la UID de la tarjeta permitida
  
 
for (byte i = 0; i < rfid.uid.size; i++) {
    Serial.
    Serial.prin

    Serial
print(rfid.uid.uidByte[i], HEX);
    
   
if (rfid.uid.uidByte[i] != tarjetaPermitida[i]) {
      accesoPermitido = 
      accesoPermitido = fals

      accesoPermitido

      acce

      

  
false;
    }
  }
  Serial.
    }
  }
  Serial.println

    }
  }
  Serial.p

    }
  

   
println();

  

 
// Verifica acceso
  if (accesoPermitido) {
    Serial.
    Serial.prin

    Seri

 
println("Acceso permitido");
    servoMotor.
    servoMotor.wri

    servoMot

    s
write(90);  // Mueve el servo a 90 grados para abrir
    
  
delay(3000);           // Mantiene la posición abierta por 3 segundos
    servoMotor.
    servoMotor.wri

    servoMotor

    servoM

    s
write(0);   // Vuelve a la posición cerrada
  } 
  } e
else {
    Serial.
    Serial.print

    Serial.

    S
println("Acceso denegado");
  }

  
  }

  /
// Detiene la lectura de la tarjeta actual
  rfid.
  rfid.PICC_Ha

  rfid.P

  
PICC_HaltA();
}
