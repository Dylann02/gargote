# Reponse du niveau 0

1. Schema relationnel des 4 tables :
- categorie(<u>id</u>,libelle)
- plat(<u>id</u>,nom,prix,#id_categori)
- commande (<u>id</u>,date_commande,numero_table)
- comande_ligne(<u>id</u>,#id_commande,#id_plat,quantite,prix_unitaire)

2. 'Commande ligne' contient prix_unitaire car si un jour on decide de changer lprix d'un plat ,les autres commandes ne sera pas affecter.Ex:un plat ravitoto coute 5.000ar , au moment de la commande

3. Si on supprime une commande dans la table commande , toute les ligne dans la table commande_ligne ayant le meme id_commande seront supprime.L'instruction est la requete 'DELETE'.

4. Les erreurs que j'ai repere :
- on peut inserer un prix negatif pour un plat
-



5. Le code est 201 car c'est le code http pour l'ajout mais pour 200 c'est pour la modification.

6. Pour la requete d , c'esy Postgresql qui bloque la suppression car il y a un foreign key de id_plat dans la table commande_ligne.

7. La commande curl :
 curl -X POST http://localhost:8080/api/commandes \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "numero_table": 6,
    "lignes": [
      { "id_plat": 4,  "quantite": 2, "prix_unitaire": 7000 },
      { "id_plat": 10, "quantite": 1, "prix_unitaire": 1000 }
    ]
  }'


| # | Étape | Fichier | Fonction / ligne |
|---|---|---|---|
| 1 | Le formulaire est soumis | `components/PlatForm.vue` | `enregistrer()`|
| 2 | La requête HTTP est construite |`src/Api.js` | `requete()` |
| 3 | Vite transmet `/api/...` au port 8080 |`vite.config.js` | `defineConfig`|
| 4 | CodeIgniter choisit le contrôleur | `app/config/Route.php`| |
| 5 | Le contrôleur lit le JSON |`app/controller/ApicController.php` |`donneesJson()`|
| 6 | Les règles de validation sont vérifiées | `app/Models/PlatModel.php`| `validationMessages`|
| 7 | La ligne est insérée |`` |`create()` |
| 8 | Le formulaire prévient l’écran parent |`src/views/CommandeView.vue` | `emit(…)` |
| 9 | L’écran recharge la liste | `views/CarteView.vue` | `charger()`|

8. Le code de creation d'une commande est dans `app/services/CommandeService.php` car le controller doit just gerer l'appel de fonction pas la logique du code en soi.

11) 
CarteView fetch les categories via api.categories.liste() , puis envoyer a PlatForm en tant que props.


