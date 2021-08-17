# Prot-tipo-de-pr-tese-controlada-de-m-o
#include <IRremote.h> //INCLUSÃO DE BIBLIOTECA
 
int RECV_PIN = 2; //PINO DIGITAL UTILIZADO PELO RECEPTOR INFRAVERMELHO
 
IRrecv irrecv(RECV_PIN); //PASSA O PARÂMETRO PARA A FUNÇÃO irrecv
 
long int codTeclaCHM = 16753245; //DEDAO MENOS
long int codTeclaCH = 16736925; //DEDAO MAIS
long int codTeclaESQ = 16720605; //INDICADOR MENOS
long int codTeclaDIR = 16712445; //INDICADOR MAIS
long int codTeclaMENOS = 16769055; //TRÊS DEDOS MENOS
long int codTeclaMAIS = 16754775; //TRÊS DEDOS MAIS
long int codTecla0 = 16738455; //TESTE LED
long int codTecla1 = 16724175; //POSITIVO
long int codTecla2 = 16718055; //REGRA DA MÃO DIREITA
long int codTecla3 = 16743045; //INDICADOR
long int codTecla4 = 16716015; //PINÇA
long int codTecla5 = 16726215; //MÃO ABERTA
long int codTecla6 = 16734885; //MÃO FECHADA

const int sensorPin3=3; //TRES DEDOS
const int sensorPinIND=4; //INDICADOR
const int sensorPinDEDAO=5; //DEDAO
const int base = 100; //VALOR BASE SENSORES PIEZOELETRICOS
 
decode_results results; //VARIÁVEL QUE ARMAZENA OS RESULTADOS (SINAL IR RECEBIDO)

#include <Servo.h>

Servo myservoDEDAO; 
Servo myservoIND;
Servo myservoTRES;

int posDEDAO = 160; 
int posIND = 170;    
int posTRES = 90; 
 
void setup(){
  irrecv.enableIRIn(); //INICIALIZA A RECEPÇÃO DE SINAIS IR

  myservoIND.attach(9);
  myservoIND.write(posIND);
  myservoDEDAO.attach(12);
  myservoDEDAO.write(posDEDAO);
  myservoTRES.attach(11);
  myservoTRES.write(posTRES);
}
 
void loop() {
  //CAPTURA O SINAL IR
  if (irrecv.decode(&results)) {

    if(results.value == codTeclaCH){
      if(posDEDAO <= 160){
        posDEDAO = posDEDAO + 10;
        myservoDEDAO.write(posDEDAO);              // incrementa 10 graus ao motor do dedo polegar
        delay(7); 
      }else{}
    }

    if(results.value == codTeclaCHM){
      if(analogRead(sensorPinDEDAO)>=base){
      } else {
        posDEDAO = posDEDAO - 10;
        myservoDEDAO.write(posDEDAO);              // decrementa 10 graus ao motor do dedo polegar
        delay(7); 
      }
    }

    if(results.value == codTeclaDIR){
      if(posIND <= 170){
        posIND = posIND + 10;
        myservoIND.write(posIND);              // incrementa 10 graus ao motor do dedo indicador
        delay(7); 
      }else{}
    }

    if(results.value == codTeclaESQ){
      if(analogRead(sensorPinIND)>=base){
      }else{
        if(posIND >= 30){
          posIND = posIND - 10;
          myservoIND.write(posIND);              // decrementa 10 graus ao motor do dedo indicador
          delay(7); 
        }else{}
      }
    } 

    if(results.value == codTeclaMAIS){
      if(posTRES <= 90){
        posTRES = posTRES + 10;
        myservoTRES.write(posTRES);              // incrementa 10 graus ao motor dos dedos médio, anular e mínimo
        delay(7); 
      }else{}
    }

    if(results.value == codTeclaMENOS){
      if(analogRead(sensorPin3)>=base){
      }else{
        posTRES = posTRES - 10;
        myservoTRES.write(posTRES);              // decrementa 10 graus ao motor dos dedos médio, anular e mínimo
        delay(7); 
      }
    } 

    if(results.value == codTecla1){
        for(;posDEDAO <=160; posDEDAO++){
          myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 160 graus
          delay(7);
        }

        for(posIND; posIND >=50; posIND--){
          myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 50 graus
          delay(7);
        }
        for(;posTRES >= 70; posTRES--){
          myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
          delay(7);
        }
    } 

    if(results.value == codTecla2){
        if(posIND <=80){
          for(;posIND <=80; posIND++){
            myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 80 graus
            delay(7);
          }
        }else{
            for(;posIND >=80; posIND--){
              myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 50 graus
              delay(7);
            }
        }

        if(posTRES <=70){
          for(;posTRES <=70; posTRES++){
            myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
            delay(7);
          }
        }else{
            for(;posTRES >=70; posTRES--){
              myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
              delay(7);
            }
        }

        for(;posDEDAO <=160; posDEDAO++){
          myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 160 graus
          delay(7);
        }
    } 

    if(results.value == codTecla3){
        for(;posIND <=170; posIND++){
          myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 170 graus
          delay(7);
        }

        if(posTRES <=70){
          for(;posTRES <=70; posTRES++){
            myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
            delay(7);
          }
        }else{
            for(;posTRES >=70; posTRES--){
              myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
              delay(7);
            }
        }

        for(;posDEDAO >=0; posDEDAO--){
          myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 0 graus
          delay(7);
        }
    } 

    if(results.value == codTecla4){
        if(posTRES <=70){
          for(;posTRES <=70; posTRES++){
            myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
            delay(7);
          }
        }else{
            for(;posTRES >=70; posTRES--){
              myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
              delay(7);
            }
        }

        for(;posDEDAO >=0; posDEDAO--){
          myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 0 graus
          delay(7);
        }

        if(posIND <=100){
          for(;posIND <=100; posIND++){
            myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 100 graus
            delay(7);
          }
        }else{
            for(;posIND >=100; posIND--){
              myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 100 graus
              delay(7);
            }
        }
    }
    
    if(results.value == codTecla5){
        for(;posIND <=160; posIND++){
          myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 160 graus
          delay(7);
        }

        for(;posTRES <=90; posTRES++){
          myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
          delay(7);
        }

        for(;posDEDAO <=160; posDEDAO++){
          myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 160 graus
          delay(7);
        }
    } 

    if(results.value == codTecla6){
        if(posDEDAO <=60){
          for(;posDEDAO <=60; posDEDAO++){
            myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 60 graus
            delay(7);
          }
        }else{
            for(;posDEDAO >=60; posDEDAO--){
              myservoDEDAO.write(posDEDAO);              // posiciona o motor do dedo polegar em 60 graus
              delay(7);
            }
        }

        if(posIND <=50){
          for(;posIND <=50; posIND++){
            myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 50 graus
            delay(7);
          }
        }else{
            for(;posIND >=50; posIND--){
              myservoIND.write(posIND);              // posiciona o motor do dedo indicador em 50 graus
              delay(7);
            }
        }

        if(posTRES <=70){
          for(;posTRES <=70; posTRES++){
            myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
            delay(7);
          }
        }else{
            for(;posTRES >=70; posTRES--){
              myservoTRES.write(posTRES);              // posiciona o motor dos dedos médio, anular e mínimo em 70 graus
              delay(7);
            }
        }
    } 

    irrecv.resume(); //AGUARDA O RECEBIMENTO DE UM NOVO SINAL IR
  }
  delay(10); //INTERVALO DE 10 MILISSEGUNDOS
}
