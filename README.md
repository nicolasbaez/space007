## : : s p a c e 0 0 7

![space](https://github.com/nicolasbaez/space007/blob/master/space007.gif)

```processing
int qX=16;
int qY=qX/2;
int cantidad=qX*qX;
float radio=qY;
float maxAng[]=new float[cantidad];
float rot=0;
float dZ=8;
float dCirc=8;
float zPos[]=new float[cantidad];
float tx[]=new float[cantidad];
int cuentaCuadros=1;
void setup() {
  size(512, 256, P3D);
  for (int i=0; i<cantidad; i++) {
    maxAng[i]=random(180, 360);
    tx[i]=random(128, 256);
    if (i==0) {
      zPos[i]=0;
    } else {
      zPos[i]=zPos[i-1]+random(-dZ, dZ);
    }
  }
}
void draw() {
  translate(width/2, height/2, 0);
  rotateX(radians(rot));
  rotateY(radians(rot));
  background(0);
  int qPos=0;
  for (float i=-width/2; i<=width/2; i+=width/qX) {
    for (float j=-height/2; j<=height/2; j+=height/qY) {
      pushMatrix();
      translate(i, j, 0);
      stroke(0, random(128, 255), random(128, 255));
      strokeWeight(random(4));
      point(0, 0);
      popMatrix();
      pushMatrix();
      translate(i, j, zPos[qPos]);
      for (int k=0; k<=maxAng[qPos]; k+=dCirc) {
        stroke(255, 0, 0, tx[qPos]);
        strokeWeight(2);
        point(radio*cos(radians(k)), radio*sin(radians(k)));
      }
      qPos++;
      popMatrix();
    }
  }
  rot+=0.5;
  if (cuentaCuadros<=720) {
    saveFrame("gif/space007-######.png");
    cuentaCuadros++;
  }
}
```
