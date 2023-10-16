# communication_between_pics_RS232
## communication between pics, binary encoder to letter decoder

_Comunicacion entre 2 microncontroladores en encoder y deencoder_

## Codigo de comunicacion de transmisor encoder 
_PIC 1_

``` C++
//codigo de codificador "encoder"
#include <16f877a.h> //libreria del microcontrolador
#DEVICE adc=10 // resolucion de trabajo
#fuses xt, nowdt 
#use delay (clock = 4M) //reloj interno
#use rs232 (baud=9600, xmit=pin_C6, rcv=pin_C7, parity=N, bits=8) //libreria de trabajo para comunicacion rs232     
#use i2c(Master,Fast=100000, sda=PIN_C4, scl=PIN_C3,force_sw)  // libreríá para manejar la comunicación I2C
#include "i2c_Flex_LCD.c" //driver para manejar la interface LCD I2C
#use standard_io (A,D,E) // declaracion de entradas en los pines A,B,E  
#include <string.h>
int letra = 0;
void main(){
   lcd_init(0x4E,16,2); //inicializacion de la lcd
   lcd_backlight_led(ON); //encendido de la luz de fondo
   lcd_putc("PIC Transmitter"); //mensaje inicial del codigo
    while (TRUE) {
      int SEND = INPUT(PIN_D0);//boton para enviar la cadena de caracteres     
    //LEER EL ESTADO DE LOS BOTONES
    int BT1 = INPUT(PIN_A0);
    int BT2 = INPUT(PIN_A1);
    int BT3 = INPUT(PIN_A2);
    int BT4 = INPUT(PIN_A3);
    int BT5 = INPUT(PIN_A5);
    int BT6 = INPUT(PIN_E0);
    int BT7 = INPUT(PIN_E1);
    int BT8 = INPUT(PIN_E2);
    //GENERAR EL CODIGO BINARIO
    if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 0 && BT7 == 0 && BT8==1){
      letra = 65;//A
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 0 && BT7 == 1 && BT8==0){
      letra = 66;//B 
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 0 && BT7 == 1 && BT8==1){
      letra = 67;//C
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 1 && BT7 == 0 && BT8==0){
      letra = 68;   //D 
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 1 && BT7 == 0 && BT8==1){
      letra = 69;//E
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 1 && BT7 == 1 && BT8==0){
      letra = 70;//F
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 0 && BT6 == 1 && BT7 == 1 && BT8==1){
      letra = 71;//G
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 0 && BT7 == 0 && BT8==0){
      letra = 72;//H
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 0 && BT7 == 0 && BT8==1){
      letra = 73;//I
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 0 && BT7 == 1 && BT8==0){
      letra = 74;//J
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 0 && BT7 == 1 && BT8==1){
      letra = 75;//K
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 1 && BT7 == 0 && BT8==0){
      letra = 76;//L
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 1 && BT7 == 0 && BT8==1){
      letra = 77;//M
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 1 && BT7 == 1 && BT8==0){
      letra = 78;//N
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 1 && BT4== 0 && BT5 == 1 && BT6 == 0 && BT7 == 0 && BT8==1){
      letra = 209;//Ñ
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 0 && BT5 == 1 && BT6 == 1 && BT7 == 1 && BT8==1){
      letra = 79;//O
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 0 && BT7 == 0 && BT8==0){
      letra = 80;//P
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 0 && BT7 == 0 && BT8==1){
      letra = 81;//Q
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 0 && BT7 == 1 && BT8==0){
      letra = 82;//R
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 0 && BT7 == 1 && BT8==1){
      letra = 83;//S
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 1 && BT7 == 0 && BT8==0){
      letra = 84;//T
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 1 && BT7 == 0 && BT8==1){
      letra = 85;//U
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 1 && BT7 == 1 && BT8==0){
      letra = 86;//V
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 0 && BT6 == 1 && BT7 == 1 && BT8==1){
      letra = 87;//W
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 1 && BT6 == 0 && BT7 == 0 && BT8==0){
      letra = 88;//X
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 1 && BT6 == 0 && BT7 == 0 && BT8==1){
      letra = 89;//Y   
    }else if(BT1 == 0 && BT2 == 1 && BT3 == 0 && BT4== 1 && BT5 == 1 && BT6 == 0 && BT7 == 1 && BT8==0){
      letra = 90;//Z
    }else if(BT1 == 0 && BT2 == 0 && BT3 == 1 && BT4== 0 && BT5 == 0 && BT6 == 0 && BT7 == 0 && BT8==0){
      letra = 32;//ESPACIO     
    }else{
      letra = 0;
    }
    //esperar hasta que se presione el boton de enviar
      if (SEND == 1) {
         PUTC(letra);
         lcd_gotoxy(1,2);
         printf(lcd_putc,"Send= %d",letra);
         printf(lcd_putc," #= %c",letra);
         delay_ms(500);
      } 
  }
}

``` 

## Codigo de comunicacion de receptor deencoder 
_PIC 2_

``` C++
//codigo de decodificador deencoder
#include <16f877a.h> //libreria del microcontrolador
#DEVICE adc=10 //resolucion de trabajo
#use delay (clock = 4M) //tiempo del reloj
#fuses xt, nowdt 
#use rs232 (baud=9600, xmit=pin_C6, rcv=pin_C7, parity=N, bits=8) //
#use i2c(Master,Fast=100000, sda=PIN_C4, scl=PIN_C3,force_sw)  // libreríá para manejar la comunicación I2C
#include "i2c_Flex_LCD.c" //driver para manejar la interface LCD I2C
#use standard_io(A)

char letra; //caracter receptor de datos
int i=1;//variable de incrementacion

void main ()
{
   lcd_init(0x4E,16,2); //inicializacion de la lcd
   lcd_backlight_led(ON); //encendido de la luz de fondo
   lcd_putc("PIC Receiver"); //mensaje inicial del codigo
  while (TRUE)
  {
   letra=getc();//linea de recepcion de datos rs232 
   lcd_gotoxy(i,2);
   printf(lcd_putc,"%c",letra);
   i++; 
   delay_ms(500);  
      
   }
 }    

```


## Diagrama esquematico realizado en proteus
_diagrama en proteus_
![image](https://github.com/Gaddiel0710/communication_between_pics_RS232/assets/135661300/c190221b-6107-49d8-8494-418e4a2af17a)

## Demostracion de funcionamiento en proteus
![image](https://github.com/Gaddiel0710/communication_between_pics_RS232/assets/135661300/8e97a740-a726-404a-8687-e8711fd75108)


## circuito fisico
![imagen](https://github.com/Gaddiel0710/communication_between_pics_RS232/assets/135661300/be46b1bf-12a5-4e0f-abd6-f2df612bcd04)



