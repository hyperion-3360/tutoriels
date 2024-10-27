<!--
Copyright (c) 2024 Hypérion 3360

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
-->

# Programmer un Nouveau Sous-système pour un Robot avec WPIlib

## 1. Définition du Sous-système

### Création de la classe du sous-système
1. Dans VSCode, à gauche, faire un clic-droit sur **subsystems** et choisir **Create a new class/command**.
2. VSCode vous offrira des choix de types de classe. Sélectionner **Subsystem** pour obtenir une classe générique de sous-système.
3. Tapez le nom que vous voulez donner à votre classe de sous-système. Utilisez un nom distinctif qui représente bien votre sous-système dans le robot. Ex: `LanceurBalle`
4. Un nouveau fichier .java portant le nom désigné sera automatiquement créé pour vous.
Son contenu ressemblera à ceci :
    ```java
    public class LanceurBalle extends SubsystemBase {
      public LanceurBalle() {}
      @Override
      public void periodic() {
      }
    }
    ```
### Déclaration des composants
- **Moteurs, Capteurs, etc** : Dans la classe, en haut du constructeur, déclarer les variables pour les moteurs ou capteurs qui seront contrôlés dans ce sous-système. Par exemple :
    ```java
    private final DigitalInput m_limitSwitch = new DigitalInput(0);
    private final Servo m_servoMoteur = new Servo(0);
    ```

## 2. Implémentation des Méthodes

### Initialisation des composants
- **Constructeur** : Initialiser les composants dans le constructeur. Par exemple :
    ```java
    public LanceurBalle() {
      // Positionner le servo à la position initiale voulue au démarrage.
      // Disons 25 degrés
      m_servoMoteur.setAngle(25);
    }
    ```

### Méthodes principales
- **Contrôle du moteur** : Crée une ou plusieurs méthode(s) pour contrôler tes moteurs. Par exemple :
    ```java
    public void LancerBalle() {
      m_servoMoteur.setAngle(180);
      Timer.delay(0.25)
      m_servoMoteur.setAngle(25);
    }
    ```
- **Controle périodique** : Pour que le sous-système fasse quelque chose à toutes les 20 millisecondes, on peut écrire du code dans la fonction `periodic()`.
- **Commande**: On peut ajouter une fonction qui retourne une commande. Utile pour lier avec un bouton d'un contrôleur Xbox plus tard!
	```java
    public Command CommandeLanceBalle() {
      return this.run(() -> LancerBalle());
    }
  ```
		
 
## 3. Intégration dans le Robot

### Déclaration dans la classe RobotContainer
- **Instance** : Dans la classe principale du robot, déclarer une instance du sous-système :
    ```java
    private final LanceurBalle m_lanceBalle = new LanceurBalle();
    ```

### Commandes associées
**Classe de commandes** : Ceci est une alternative à la fonction de commande mentionnée plus haut. On peut vouloir créer une classe pour des commandes plus complexes qui nécessitent plus d'un sous-système!
1. Dans VSCode, à gauche, faire un clic-droit sur **commands** et choisir **Create a new class/command**.
2. VSCode vous offrira des choix de types de classe. Sélectionner **Command** pour obtenir une classe générique de commande.
3. Taper le nom que vous voulez donner à votre classe de commande. Utilisez un nom distinctif qui représente bien votre commande dans le robot.
4. Un nouveau fichier .java portant le nom désigné sera automatiquement créé pour vous. Il ne reste qu'à programmer la commande.
  ```java
  public class ExempleCommande extends CommandBase {
    private final LanceurBalle m_lanceballe;
    private final AutreSousSysteme m_autreSysteme;

    public ExempleCommande(LanceurBalle lanceLaBalle, AutreSousSystème voilaLautreSousSysteme) {
      m_lanceballe = lanceLaBalle;
      m_autreSysteme = voilaLautreSousSysteme;
      addRequirements(m_lanceballe);
      addRequirements(m_autreSysteme);
    }
    @Override
    public void initialize() {
    // Appelé lorsque la commande est lancée. 
    // Appeler les fonctions des sous-systèmes nécessaires à les préparer à exécuter la commande
    }
    @Override
    public void execute() {
    // Écrire le code que le robot doit exécuter pour cette commande
    }
    @Override
    public void end() {
    // Si nécessaire, les actions à prendre quand la commande est finie
    }
    @Override
    public boolean isFinished() {
    // Cette fonction doit retourner true lorsque la commande est terminée ou false sinon.
    }
  }
  ```

## 4. Tests et Débogage

### Débogage
- **Breakpoints** : Utilise les breakpoints dans ton VSCode pour analyser le comportement de ton programme étape par étape pendant l'exécution.
- **Tests en conditions réelles** : Si possible, teste ton programme sur un robot physique pour valider les résultats.
### Simulations (avancé)
- **Simulateur** : Utilise le simulateur intégré de WPIlib pour tester ton code sans avoir besoin de matériel réel.
- **Logs** : Vérifie les logs pour repérer toute erreur ou comportement inattendu.


## 5. Documentation et Finalisation

### Commentaires
- **Clarté** : Ajoute des commentaires explicatifs dans ton code pour chaque méthode et fonction importante.

### Documentation externe
- **Guide détaillé** : Crée un document détaillé, expliquant chaque étape de la création et de l'intégration du sous-système, incluant des captures d'écran et des exemples de code.


