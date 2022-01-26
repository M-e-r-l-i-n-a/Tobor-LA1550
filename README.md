# Portfolioeintrag zu Tobor
Dieses Programm ist im Lernatelier entstanden, einem Fach in der Informatikmittelschule, in dem wir eigene Projekte programmieren dürfen. Dieses Mal haben wir mit Robocode, das mit Java programmiert wird, Roboter erschaffen, die gegeneinander antreten. So wurde Tobor geboren.

### Ziel:
Tobors Strategie verständlich beschreiben.

### Erklärung: 
Tobor sucht sich die nächste Ecke und wartet darauf, seine Gegner abschiessen zu können.
Er schaut zuerst, ob er näher links oder rechts an der Wand ist und geht da hin. Dann geht er, je nach dem, was näher ist, entweder nach oben oder nach unten. Während er in seine Ecke geht, scannt er seine gesamte Umgebung nach Feinden ab, auf die er dann schiesst. Je näher sie sind, desto stärker ist sein Schuss. Wenn er dann seine Ecke gefunden hat, scannt er nur noch den Bereich vom Feld, den er sieht.

### Code:
```java
package TafelskiElena;
import robocode.*;

public class Tobor extends JuniorRobot
{
	int position;
	int scanStart = 1;
	public void run() {

		setColors(black, black, black, red, black);
		
		if(robotX > fieldWidth/2) {
			turnTo(90);
			position = 1;
		} else {
			turnTo(-90);
			position = 3;
		}
		

		while(true) {
			ahead(100);
			
			if (scanStart == 1) {
				turnGunLeft(360);
			} else {
				turnGunTo(scanStart);
				turnGunLeft(90);
			}

			switch (position) {
				case 1:	scanStart = 270;
						break;
				case 2:	scanStart = 0;
						break;
				case 3:	scanStart = 180;
						break;
				case 4:	scanStart = 90;
						break;
			}	
		}
	}


	public void onScannedRobot() {
		turnGunTo(scannedAngle);
		if (scannedDistance < 50) {
			fire(3);
		} else if (scannedDistance < 100) {
			fire(2);
		} else {
			fire(1);
		}
	}


	public void onHitByBullet() {
		switch (position) {
				case 1:	if(hitByBulletAngle < 225) {
							turnTo(270);
						} else {
							turnTo(180);
						}
						break;
				case 2:	if(hitByBulletAngle < 315) {
							turnTo(0);
						} else {
							turnTo(270);
						}
						break;
				case 3:	if(hitByBulletAngle < 135) {
							turnTo(180);
						} else {
							turnTo(90);
						}
						break;
				case 4:	if(hitByBulletAngle < 45) {
							turnTo(90);
						} else {
							turnTo(0);
						}
						break;
		}
		out.println(position + "   " + hitByBulletAngle + "   " + heading);
		scanStart = 1;
	}
	

	public void onHitWall() {
		if(robotY > fieldHeight/2) {
			turnTo(0);
		} else {
			turnTo(180);
			if (position == 1 || position == 3) {
				position += 1;
			}
		}
	}	
}

```

### Video:


### Verifikation: 
Ich habe mein Ziel, Tobors Strategie verständlich zu beschreiben, im Abschnitt Erklärung erreicht.

### Reflexion: 
Die Arbeit hat eigentlich gut geklappt, allerdings konnte ich mich zum Teil nicht gut konzentrieren, da es zu laut war. Ich werde es nächstes Mal mit Musik probieren, allerdings bezweifle ich, dass ich mich dann viel besser konzentrieren kann. 
Letztes Mal wollte ich mehr auf andere zugehen und mit ihnen sprechen. Da es diesmal aber keine Gruppenarbeit war, habe ich es nicht einmal versucht.
