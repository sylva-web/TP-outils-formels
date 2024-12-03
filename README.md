# TP-outils-formels
### Rapport du TP : Système de Contrôle d'Accès

#### **Introduction**

L’objectif de ce TP était de développer un **système de contrôle d’accès** permettant d’ajouter, de vérifier et de sécuriser des cartes d’accès associées à des codes secrets. Chaque carte devait être enregistrée dans une base de données interne. Si une tentative de réutilisation du même numéro de carte était détectée, le système devait alerter l’utilisateur que cette carte existait déjà. De plus, après trois tentatives de code incorrect, une alarme devait se déclencher et le système devait être réinitialisé après un délai de 10 secondes.

---

### **1. Spécifications Initiales**

Le système devait permettre de :
1. **Ajouter une carte** : Chaque carte comprend un **numéro unique** et un **code secret**.
2. **Vérifier une carte** : Si la carte existe dans la base de données, le code saisi est comparé au code enregistré. Si le code est correct, l’accès est accordé.
3. **Détecter les doublons** : Si un utilisateur tente d’ajouter une carte déjà existante, le système doit afficher un message indiquant que la carte existe déjà.
4. **Gérer les tentatives incorrectes** : Si un utilisateur saisit un mauvais code trois fois consécutivement, une alarme est déclenchée.
5. **Réinitialisation automatique** : Après l’alarme, le système se réinitialise après un délai de 10 secondes.

---

### **2. Conception du Système**

#### **Structure du Code**

Le programme est structuré autour de trois principales classes :
1. **`Carte`** : Représente les cartes d’accès avec un numéro unique et un code secret.
2. **`BaseDeDonnees`** : Gère les cartes enregistrées dans une base de données simulée (utilisation d’un `HashMap` pour stocker les cartes).
3. **`AutomateAcces`** : Gère les états du système, les tentatives d’accès et l’activation de l’alarme.

#### **Logique de Fonctionnement**

- Lorsqu’un utilisateur souhaite ajouter une carte, le système vérifie si le numéro de la carte existe déjà dans la base. Si c’est le cas, il affiche un message d’erreur ; sinon, la carte est ajoutée avec succès.
- Pour vérifier une carte, le programme compare le numéro de carte et le code saisi avec les informations enregistrées. Si le code est correct, l’accès est accordé. Sinon, après trois tentatives incorrectes, une alarme est déclenchée.

---

### **3. Résultats des Vérifications et Tests**

Des scénarios de test ont été réalisés pour s’assurer du bon fonctionnement du système :

1. **Ajout d’une nouvelle carte** : 
   - Test : Ajouter un numéro de carte et un code secret non existants.
   - Résultat attendu : La carte est ajoutée avec succès.
   - Résultat obtenu : Fonctionne comme prévu.

2. **Ajout d’une carte existante** :
   - Test : Réessayer d’ajouter une carte avec le même numéro.
   - Résultat attendu : Le système doit afficher un message indiquant que la carte existe déjà.
   - Résultat obtenu : Fonctionne comme prévu.

3. **Accès avec un code correct** :
   - Test : Saisir un numéro de carte existant et le code correct.
   - Résultat attendu : Accès accordé.
   - Résultat obtenu : Fonctionne comme prévu.

4. **Accès avec un code incorrect** :
   - Test : Saisir un numéro de carte existant avec un code incorrect trois fois.
   - Résultat attendu : Accès refusé et déclenchement de l’alarme après trois tentatives.
   - Résultat obtenu : Fonctionne comme prévu.

5. **Réinitialisation après l’alarme** :
   - Test : Observer le comportement après le déclenchement de l’alarme.
   - Résultat attendu : Le système attend 10 secondes, se réinitialise, et permet une nouvelle tentative.
   - Résultat obtenu : Fonctionne comme prévu.

---

### **4. Défis Rencontrés et Solutions Apportées**

#### **Défis rencontrés :**

1. **Gestion des doublons** :
   - Initialement, il était possible d’ajouter plusieurs cartes avec le même numéro. Cela créait des incohérences dans la base de données et compliquait la vérification des codes.
   
2. **Réinitialisation après alarme** :
   - Mettre en place un délai après le déclenchement de l’alarme pour permettre une nouvelle tentative tout en gardant le système stable a été un défi.

#### **Solutions apportées :**

1. **Détection des doublons** :
   - Une vérification préalable a été ajoutée dans la méthode `ajouterCarte()` de la classe `BaseDeDonnees` pour s’assurer qu’un numéro de carte ne soit pas ajouté plusieurs fois.

2. **Délai de réinitialisation** :
   - L’utilisation de la fonction `Thread.sleep(10000)` a permis de simuler une attente de 10 secondes après l’alarme, avant de réinitialiser les états du système.

---

### **5. Conclusion**

Le système de contrôle d’accès conçu répond bien aux spécifications initiales. Il permet :
- L’ajout de nouvelles cartes, tout en évitant les doublons.
- La vérification des cartes et des codes associés.
- Une gestion stricte des tentatives incorrectes, avec une alarme activée après trois erreurs.
- Une réinitialisation automatique après l’alarme, permettant de nouvelles tentatives.

#### **Fiabilité et Efficacité**
Le système est fiable car il respecte les règles définies. Il est également efficace car il utilise des structures simples comme le **`HashMap`** pour gérer les données en mémoire. De plus, les tests montrent que toutes les fonctionnalités fonctionnent correctement.

#### **Améliorations possibles**
1. Ajouter une **persistence des données**, comme un fichier ou une base de données réelle, pour que les cartes restent enregistrées entre les sessions.
2. Intégrer une interface graphique pour rendre l’utilisation du système plus conviviale.
3. Permettre une gestion avancée des utilisateurs, comme la modification ou la suppression de cartes existantes.

En conclusion, ce TP a permis de comprendre les concepts de gestion d’états, de validation des données et de contrôle d’accès sécurisé. Le programme est fonctionnel et peut être amélioré pour répondre à des besoins plus complexes.
