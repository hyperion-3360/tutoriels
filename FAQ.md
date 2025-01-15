# Problèmes et solutions

## VSCode reste pris à "Java initializing..." interminable quand vous ouvrez votre projet robot:

Dans la palette de commande VSCode (Ctrl-Shift-P), commencez à taper puis sélectionnez `Java: Clean Java Language Server Workspace`

## ./gradlew :spotlessApply ne formatte pas vos sources?
Effacer le répertoire .gradle dans le projet et refaire un build robot code.
Ensuite le `./gradlew :spotlessApply` devrait fonctionner.

## Vous voulez que spotless arrête de se vouloir corriger une section d'un fichier
Utiliser ceci:
```
// spotless:on
section de code que vous voulez que spotless ignore
// spotless:off
```
## Falcon 500 qui follow un autre Falcon
Il faut cree un Follower et mettre dans les parametres le id du master falcon et si il est inverser ou non : private Follower m_follower = new Follower(id,inverser); 
m_falcon.setControl(m_follower);

## CAN Spark Max import qui marche pas
si vous faites new CANSparkMax il existe plus. le nom a change a seulement SparkMax et l'import est import com.revrobotics.spark.SparkMax;