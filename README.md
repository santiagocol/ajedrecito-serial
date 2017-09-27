# ajedrecito-serialimport processing.serial.*;
PImage peonB,peonN,torreN1,torreN2,torreB1,torreB2,alfilB1,alfilB2,alfilN1,alfilN2,caballoN1,caballoN2,caballoB1,caballoB2,reinaN,reyN,reinaB,reyB,logo;

boolean locked = false;
float[][] fichasB = new float[16][2];
float[][] fichasN = new float[16][2];
int ficha, pintura, contx=0, conty=0;
Serial AJEDRECITO;
byte[] datos= new byte[5];

void setup(){   
  size(1100,630);// el tablero lo diseñamos con un size de (1100,600)
  imageMode(CENTER);
  textAlign(CENTER);
    String portName = Serial.list()[0];
  AJEDRECITO = new Serial(this, portName, 9600);

  //IMAGENES FICHAS NEGRAS
  reinaN=loadImage("reina-negra.jpg");
  reyN=loadImage("rey-negro.jpg");
  alfilN1=loadImage("alfil-negro.jpg");
  alfilN2=loadImage("alfil-negro.jpg");
  caballoN1=loadImage("caballo-negro.jpg");
  caballoN2=loadImage("caballo-negro.jpg");
  torreN1=loadImage("torre-negra.jpg");
  torreN2=loadImage("torre-negra.jpg");
  peonN=loadImage("peon-negro.jpg");
  //IMAGENES FICHAS BLANCAS
  reinaB=loadImage("reina-blanca.jpg");
  reyB=loadImage("rey-blanco.jpg");
  alfilB1=loadImage("alfil-blanco.jpg");
  alfilB2=loadImage("alfil-blanco.jpg");
  caballoB1=loadImage("caballo-blanco.jpg");
  caballoB2=loadImage("caballo-blanco.jpg");
  torreB1=loadImage("torre-blanca.jpg");
  torreB2=loadImage("torre-blanca.jpg");
  peonB=loadImage("peon-blanco.jpg");
  logo=loadImage("logo.png");
  
  //LETRAS Y NUMEROS
  textSize(25);

  float t=539;
for(int g=0; g<8; g++){
  fichasB[g][0] = t+(75*g);
  fichasB[g][1] = 37.5;
  fichasB[g+8][0]= t+(75*g);
  fichasB[g+8][1]= 112.5;
}
 for(int w=0; w<8; w++){
  fichasN[w][0] = t+(75*w);
  fichasN[w][1] = 562.5;
  fichasN[w+8][0]= t+(75*w);
  fichasN[w+8][1]= 487.5;  
}

}
void draw(){
  rectMode(CENTER);
  background(0);

   float i=537.5;
   float j=562.5;

  for( i=i; i<1100; i=i+150){
      rect(i,j,75,75);
      rect(i,j-150,75,75);
      rect(i,j-300,75,75);
      rect(i,j-450,75,75);
      rect(i+75,j-75,75,75);
      rect(i+75,j-225,75,75);
      rect(i+75,j-375,75,75);
      rect(i+75,j-525,75,75); 
     }    
    rectMode(CORNER);
  fill(144,9,9);
  rect(0,0,470,450);
  fill(116,115,115);
  rect(470,600,630,30);
  rect(470,0,30,600);
  
  

  image(reinaN,fichasN[3][0],fichasN[3][1],55,55);
  image(reyN,fichasN[4][0],fichasN[4][1],55,55);
  image(alfilN1,fichasN[5][0],fichasN[5][1],55,55);
  image(alfilN2,fichasN[2][0],fichasN[2][1],55,55);
  image(caballoN1,fichasN[6][0],fichasN[6][1],55,55);
  image(caballoN2,fichasN[1][0],fichasN[1][1],55,55);
  image(torreN1,fichasN[7][0],fichasN[7][1],55,55);
  image(torreN2,fichasN[0][0],fichasN[0][1],55,55);
  for(int k=8; k<=15; k++){
      image(peonN,fichasN[k][0],fichasN[k][1],55,55);
  }
  image(reinaB,fichasB[3][0],fichasB[3][1],55,55);
  image(reyB,fichasB[4][0],fichasB[4][1],55,55);
  image(alfilB1,fichasB[5][0],fichasB[5][1],55,55);
  image(alfilB2,fichasB[2][0],fichasB[2][1],55,55);
  image(caballoB1,fichasB[6][0],fichasB[6][1],55,55);
  image(caballoB2,fichasB[1][0],fichasB[1][1],55,55);
  image(torreB1,fichasB[7][0],fichasB[7][1],55,55);
  image(torreB2,fichasB[0][0],fichasB[0][1],55,55);
  for(int k=8; k<=15; k++){
      image(peonB,fichasB[k][0],fichasB[k][1],55,55);
      
  }
  
  //LETRAS Y NUMEROS
  fill(255);
  for(int p=1; p<9; p++){
  text(p,485,((p*50)+((p-1)*25)));
  text(char('A'+p-1),(490+((p*50)+((p-1)*25))),625);
  }
  image(logo,235,540,470,180);
}

void mousePressed()
{  
   for(int b=0; b<16; b++){
    if(mouseX > (fichasB[b][0]-27.5) && mouseX < (fichasB[b][0]+27.5) &&
      mouseY > (fichasB[b][1]-27.5) && mouseY < (fichasB[b][1]+27.5) ) {
      locked = true;
      ficha = b;
      pintura=0;
      datos[0]= byte(int ((fichasB[ficha][0]/75)-6));
      datos[1]= byte(int ((fichasB[ficha][1]/75)+1));
        break;  
    } 
        if(mouseX > (fichasN[b][0]-27.5) && mouseX < (fichasN[b][0]+27.5) &&
      mouseY > (fichasN[b][1]-27.5) && mouseY < (fichasN[b][1]+27.5) ) {
      locked = true;
      ficha = b;
      pintura=1;
        datos[0]= byte(int ((fichasN[ficha][0]/75)-6));
        datos[1]= byte(int ((fichasN[ficha][1]/75)+1));
       
      break;
    }  
  }
}

void mouseDragged()
{
  if( locked ){
    if(pintura==0){
    fichasB[ficha][0] = mouseX;
    fichasB[ficha][1] = mouseY;
    } 
    else{
    fichasN[ficha][0] = mouseX;
    fichasN[ficha][1] = mouseY;    
    
    }
}  
   
}

void mouseReleased()
{
  locked = false;
  
  if(pintura==0){
    fichasB[ficha][1] = int(fichasB[ficha][1]/75)*75+37.5;
    fichasB[ficha][0] = int(fichasB[ficha][0]/75)*75+14;
    datos[2]= byte(int ((fichasB[ficha][0]/75)-6));
    datos[3]= byte(int ((fichasB[ficha][1]/75)+1));
    datos[4]='\n';
  }else{
    fichasN[ficha][1] = int(fichasN[ficha][1]/75)*75+37.5;
    fichasN[ficha][0] = int(fichasN[ficha][0]/75)*75+14;
    datos[2]= byte(int ((fichasN[ficha][0]/75)-6));
    datos[3]= byte(int ((fichasN[ficha][1]/75)+1));
    datos[4]='\n';
  }   
    for(int z=0; z<=15;z++){
        if(pintura == 0){
          if(fichasN[z][0]==fichasB[ficha][0] && fichasN[z][1]==fichasB[ficha][1]){
                    fichasN[z][0]= 37.5+contx*75;
                    fichasN[z][1]= 37.5+conty*75;
                    contx = contx+1;
                    if(contx == 6){
                      contx = 0;
                      conty = conty + 1;
                    }
                     break;
            }
        }else{
           if(fichasB[z][0]==fichasN[ficha][0] && fichasB[z][1]==fichasN[ficha][1]){
                    fichasB[z][0]= 37.5+contx*75;
                    fichasB[z][1]= 37.5+conty*75;
                    contx = contx+1;
                    if(contx == 6){
                      contx = 0;
                      conty = conty + 1;
                    }
                     break;
            }
        }
    
    
    }
  
    AJEDRECITO.write(datos);
    println(datos);

}
