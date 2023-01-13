import ddf.minim.spi.*;
import ddf.minim.signals.*;
import ddf.minim.*;
import ddf.minim.analysis.*;
import ddf.minim.ugens.*;
import ddf.minim.effects.*;

Minim minim;
AudioInput in;

String scene = "start";
int countF = 0;
float ms;
float basems = 0;
float timeLimit = 15.0;
float fl_countDown;
int in_countDown;
int interval = 0;
int rep;
int rerep;

int finTime = 0;

void setup(){
  frameRate(100);
  size(1000, 800);
  minim = new Minim(this);
  in = minim.getLineIn(Minim.STEREO, 512);
  background(0);
}

void draw(){
  if(scene == "start"){
    startWindow();
  }
  else if(scene == "measure"){
  measureWindow();
  }
}

void stop(){
  in.close();
  minim.stop();
  super.stop();
}

void startWindow(){
  background(255);
  fill(0);
  textSize(80);
  textAlign(CENTER,CENTER);
  text("PULSE × VOICE", width/2, height/2-150);
  textSize(30);
  textAlign(CENTER,CENTER);
  text("~ BIOMETRIC MEASUREMENT ~", width/2, height/2-80);
  textSize(30);
  textAlign(CENTER,CENTER);
  text("PRESS ANY KEY TO START", width/2, height/2+200);
  textSize(30);
  textAlign(CENTER,CENTER);
  text("© 2022-2023 N.Y.WINTER ASSIGNMENT", width/2, height/2+300);
  if(keyPressed){
    scene = "measure";
  }
}

void measureWindow(){
    background(0);
    ms = millis()/1000 - basems;
    fill(255,255,255);
    rect(0, 0, width, height);
    countF++;
      if(0<=countF && countF<100*3){
        background(242,231,0);
        fill(0);
        textSize(50);
        text("CAUTION",width/2-10, 280);
        textSize(50);
        textAlign(CENTER,CENTER);
        text("This measurment",width/2, height/2);
        text("is intended",width/2, height/2+80);
        text("for adults.",width/2, height/2+160);
      }
      else if(100*3<=countF && countF<100*4){
        fill(0);
        textSize(80);
        textAlign(CENTER,CENTER);
        text("3",width/2,height/2);
      }
      else if(100*4<=countF && countF<100*5){
        fill(0);
        textSize(80);
        textAlign(CENTER,CENTER);
        text("2",width/2,height/2);
      }
      else if(100*5<=countF && countF<100*6){
        fill(0);
        textSize(80);
        textAlign(CENTER,CENTER);
        text("1",width/2, height/2);
      }
      else if(100*6<=countF && countF<100*7){
        fill(0);
        textSize(80);
        textAlign(CENTER,CENTER);
        text("Start!!",width/2, height/2);
      }
      else if(countF == 100*7){
        basems = millis()/1000;
      }
      else if(100*7<=countF){
        float au = in.mix.level();
        float radious = 8 + map(au, 0, 0.5, 0, 12);
        fl_countDown = timeLimit - ms;
        in_countDown = Math.round(fl_countDown);
        if(in_countDown>0){
          fill(0);
          textSize(50);
          textAlign(LEFT,TOP);
          text(in_countDown,50,50);
          if(au>0.15){
            if(interval==0){
              noStroke();
              fill(199,0,68);
              ellipse(width/2, height/2, radious *10, radious * 10);
              rep = rep+1;
              interval++;
            }
            else if(0<interval && interval<50){
              interval++;
            }
            else if(50<=interval){
              interval = 0;
            }
          }
        }
        else{
          rerep = rep*4;
          result_numWindow();
          result_figureWindow();
        }
      }
}

void result_figureWindow(){
  int hundreds = rerep/100;
  int tens = (rerep/10)%10;
  int ones = rerep%10;
  if(hundreds == 0){
    fill(116,69,170);
    if(tens==0 || tens==1){
      stroke(206,80,48);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==2 || tens==3){
      stroke(125,125,125);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==4 || tens==5){
      stroke(195,145,67);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==6 || tens==7){
      stroke(255,105,180);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==8 || tens==9){
      stroke(0,0,0);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
  }
  else if(hundreds == 1){
    fill(227,199,0);
    if(tens==0 || tens==1){
      stroke(116,80,48);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==2 || tens==3){
      stroke(125,125,125);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==4 || tens==5){
      stroke(195,145,67);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==6 || tens==7){
      stroke(255,105,180);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
    else if(tens==8 || tens==9){
      stroke(0,0,0);
      if(ones==0 || ones==1){
        ellipse(width/2,height/2,150,150);
      }
      if(ones==2 || ones==3){
        rect(width/2-100,height/2-150,150,150);
      }
      if(ones==4 || ones==5){
        arc(width/2,height/2-100,300,300,PI*3/5,PI);
      }
      if(ones==6 || ones==7){
        triangle(500,325,425,475,575,475);
      }
      if(ones==8 || ones==9){
        quad(500,325,575,325,575,475,425,475);
      }
    }
  }
}

void result_numWindow(){
  if(rerep<50){
    background(25,113,255);
    fill(255);
    textSize(80);
    textAlign(LEFT,TOP);
    text("RESULT",10, 10);
    textSize(80);
    textAlign(CENTER,CENTER);
    text(rerep,width/2-150, height/2+140);
    textSize(30);
    textAlign(CENTER,CENTER);
    text("Times Per Minute",width/2+80, height/2+150);
    textSize(80);
    textAlign(CENTER,CENTER);
    text("TOO LOW",width/2, height/2+280);
  }
  else if(50<=rerep && rerep<=100){
    background(0,176,107);
    fill(255);
    textSize(80);
    textAlign(LEFT,TOP);
    text("RESULT",10, 10);
    textSize(80);
    textAlign(CENTER,CENTER);
    text(rerep,width/2-150, height/2+140);
    textSize(30);
    textAlign(CENTER,CENTER);
    text("Times Per Minute",width/2+80, height/2+150);
    textSize(80);
    textAlign(CENTER,CENTER);
    text("NO PLOBLEM",width/2, height/2+280);
  }
  else if(100<rerep){
    background(255,75,0);
    fill(255);
    textSize(80);
    textAlign(LEFT,TOP);
    text("RESULT",10, 10);
    textSize(80);
    textAlign(CENTER,CENTER);
    text(rerep,width/2-150, height/2+140);
    textSize(30);
    textAlign(CENTER,CENTER);
    text("Times Per Minute",width/2+80, height/2+150);
    textSize(80);
    textAlign(CENTER,CENTER);
    text("TOO HIGH",width/2, height/2+280);
  }
}
