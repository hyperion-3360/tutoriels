# Problèmes et solutions

## VSCode reste pris à "Java initializing..." interminable quand vous ouvrez votre projet robot:

Dans la palette de commande VSCode (Ctrl-Shift-P), commencez à taper puis sélectionnez `Java: Clean Java Language Server Workspace`

## ./gradlew :spotlessApply ne formatte pas vos sources?
Effacer le répertoire .gradle dans le projet et refaire un build robot code.
Ensuite le `./gradlew :spotlessApply` devrait fonctionner.

## Vous voulez que spotless arrête de se vouloir corriger une section d'un fichier
Utilisez ceci:
```
// spotless:off
section de code que vous voulez que spotless ignore
// spotless:on
```
## Falcon 500 qui follow un autre Falcon
Il faut cree un Follower et mettre dans les parametres le id du master falcon et si il est inverser ou non : private Follower m_follower = new Follower(id,inverser); 
m_falcon.setControl(m_follower);

## CAN Spark Max import qui marche pas
si vous faites new CANSparkMax il existe plus. le nom a change a seulement SparkMax et l'import est import com.revrobotics.spark.SparkMax;
si vous voulez d'autres infos sur les changements de spark max regarder : https://docs.revrobotics.com/brushless/revlib/revlib-overview/migrating-to-revlib-2025

## "j'arrive pas a lire mes id"
on a eu ce probleme avec les swerves, mais il faut s'assurer de regarder la map du board. voir le "board.png" pour plus d'infos.

## "je viens d'update WPILib et mon gradle task marche pas"
regardez dans vos fichiers, car il est possible que le download que vous venez de faire de vscode se base sur l'ancienne version. effacez tout de l'ancienne version avant d'installer la nouvelle, cela vous eviteras des problemes.

## mon initSendable ne me permet pas d'éditer les valeurs affichées ou n'affiche pas toutes les valeurs des properties
Il faut appeler l'instruction suivante au début de la méthode initSendable comme suit:
@Override
  public void initSendable(SendableBuilder builder) {
    builder.setSmartDashboardType("RobotPreferences");

Si la classe qui override le initSendable ne dérive pas d'une classe qui implément l'interface Sendable, il est IMPÉRATIF d'ajouter:
    SendableRegistry.add(this, "<nom du module>", instances); 

    ou instances est incrémenté à chaque appel du constructeur

