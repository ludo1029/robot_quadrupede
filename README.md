# 🤖 Robot Quadrupède — Projet en cours de développement 🚧

## 📋 Description
Ce projet consiste à concevoir et programmer un **robot quadrupède** articulé à l’aide de **8 servomoteurs**, commandés via un module **PCA9685** (contrôleur PWM I2C).  
L’objectif est d’obtenir une **marche stable et fluide**, en gérant les mouvements **patte par patte** pour éviter toute perte d’équilibre.

> ⚠️ **Projet actuellement en développement.**  
> Le code et la mécanique sont encore en phase d’expérimentation et d’ajustement.

---

## ⚙️ Matériel utilisé
- 🧠 1 × **Carte Arduino** (Nano)
- ⚙️ 1 × **Module PCA9685** (contrôle jusqu’à 16 servos)
- 🔩 8 × **Servomoteurs SG90**
- 🔋 1 × **Batterie Lipo2S + UBEC**
- 🦿 Structure mécanique 3D
- 🔌 Câbles Dupont M/F

---

## 🧠 Principe de fonctionnement
Le robot est constitué de **4 pattes**, chacune contrôlée par **2 servomoteurs** :
- **Servo 1** → mouvement latéral (droite/gauche)
- **Servo 2** → mouvement vertical (haut/bas)

L’algorithme de marche soulève et avance une patte à la fois, pour conserver un **centre de gravité stable**.  
Le robot utilise des **valeurs d’amplitude spécifiques** pour chaque servo, afin d’adapter la marche à la géométrie réelle du châssis.

---

## 💻 Code Arduino

### Bibliothèques nécessaires
```cpp
#include <Wire.h>
#include <Adafruit_PWMServoDriver.h>

Adafruit_PWMServoDriver pca = Adafruit_PWMServoDriver();

#define SERVOMIN 150
#define SERVOMAX 600

void setup() {
  Serial.begin(9600);
  Serial.println("Initialisation du robot quadrupède...");
  pca.begin();
  pca.setPWMFreq(50);
  delay(500);
}

// Exemple de fonctions (à définir dans le code complet)
void leverPos(int servo, int angle);
void avancerPos(int servo, int angle);
void parallelMove(int servoA, int angleA, int servoB, int angleB);

void loop() {
  // --- Patte 1 (avant droite) ---
  leverPos(4, 500);          // Lever la patte
  delay(200);
  avancerPos(0, 350);        // Avancer patte
  delay(200);
  leverPos(4, 400);          // Reposer patte
  delay(200);

  // --- Patte 3 (arrière gauche) ---
  leverPos(9, 225);
  delay(200);
  avancerPos(15, SERVOMIN);
  delay(200);

  // --- Mouvement simultané expérimental ---
  parallelMove(15, 350, 0, SERVOMIN);
  delay(300);
}
```

> 🚧 Le robot peut lever et avancer chaque patte, mais la marche complète reste en développement.  
> Le projet est **en travaux** et évoluera au fur et à mesure des tests.
> 📦 *Ce dépôt est en constante évolution. Suivez les commits pour suivre les progrès du robot quadrupède !*

