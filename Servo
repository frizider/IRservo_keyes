//Program za upravljanje arduino servo motorom pomoću daljinskog upravljača Keyes
#include <IRLib.h>
#include <Servo.h> 


#define MY_PROTOCOL NEC
#define BUTTON_Power 0xFFA25D //Motorić će se pomaknuti u smjeru kazaljke na satu
#define BUTTON_mode 0xFF629D //Motorić će se pomaknuti u smjeru suprotnom od kazaljke na satu
#define BUTTON_Mute 0xFFE21D //Centriranje motorića
#define BUTTON_Play 0xFF22DD //Povećaj broj stupnjeva za koji se servo pomakne
#define BUTTON_Step_back 0xFF02FD
#define BUTTON_Step_fw 0xFFC23D //Pozicioniraj motor na 180 stupnjeva
#define BUTTON_Eq 0xFFE01F //Pozicioniraj motor na 0 stupnjeva
#define BUTTON_- 0xFFA857 //Nije definirana funkcija
#define BUTTON_+ 0xFF906F //Nije definirana funkcija
#define BUTTON_loop 0xFF9867  //Nije definirana funkcija
#define BUTTON_SD 0xFFB04F  //Nije definirana funkcija
#define BUTTON_0 0xFF6897  //Pokreni motorić sa početne točke
#define BUTTON_1 0xFF30CF  //Pomakni motorić za 20 stupnjeva
#define BUTTON_2 0xFF18E7  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_3 0xFF7A85  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_4 0xFF10EF  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_5 0xFF38C7  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_6 0xFF5AA5  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_7 0xFF42BD  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_8 0xFF4AB5  //Pomakni motorić za dodatnih 20 stupnjeva
#define BUTTON_9 0xFF52AD  //Pomakni motorić za dodatnih 20 stupnjeva

IRrecv My_Receiver(11);//Signal se zaprima na pinu 11
IRdecode My_Decoder; 
Servo My_Servo;  // Kreiramo objekt koji će kontrolirati servo motor 
int pos;         // Kreiramo varijablu u koju ćemo spremati podatke o poziciji
int Speed;       // Definiramo koliko će se stupnjeva pomaknuti motor svaki put kada pritisnemo tipku
 
void setup() 
{ 
  My_Receiver.No_Output();//Gasimo bilo koji nekorišten infracrveni izlazni krug
  My_Servo.attach(9);  // Servo motor spajamo na pin 9 našeg arduina
  pos = 40;            // Krećemo s pozicije od 40 stupnjeva
  Speed = 10;           // Servo se pomakne za 10 stupnjeva svaki put kada pomaknemo tipke power i mode
  My_Servo.write(pos); // Podešavamo početnu poziciju
  My_Receiver.enableIRIn(); // Pokrećemo infracrvenu diodu koja će primati signal
} 
 
void loop() 
{ 
    if (My_Receiver.GetResults(&My_Decoder)) {
       My_Decoder.decode();
       if(My_Decoder.decode_type==MY_PROTOCOL) {
          switch(My_Decoder.value) {
            case BUTTON_Power:    pos=min(180,pos+Speed); break;
            case BUTTON_mode:   pos=max(0,pos-Speed); break;
            case BUTTON_Mute: pos=90; break;
            case BUTTON_Play:      Speed=min(10, Speed+1); break;
            case BUTTON_Step_back:    Speed=max(1, Speed-1); break;
            case BUTTON_Step_fw: pos=180; break;
            case BUTTON_Eq:      pos=0; break;
            case BUTTON_0:      pos=0*20; break;
            case BUTTON_1:      pos=1*20; break;
            case BUTTON_2:      pos=2*20; break;
            case BUTTON_3:      pos=3*20; break;
            case BUTTON_4:      pos=4*20; break;
            case BUTTON_5:      pos=5*20; break;
            case BUTTON_6:      pos=6*20; break;
            case BUTTON_7:      pos=7*20; break;
            case BUTTON_8:      pos=8*20; break;
            case BUTTON_9:      pos=9*20; break;
          }
        My_Servo.write(pos); // Servo motor se pomiče u poziciju koju definira varijabla pos 
       }
     My_Receiver.resume();
    }
}
