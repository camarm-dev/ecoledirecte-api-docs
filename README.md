# EcoleDirecte Api Documentation

## Introduction


Bienvenue sur la documentation non officielle de l'api d'ecoledirecte.

Si jamais cette documentation vient a être défaillante, merci de faire une issue avec les problèmes rencontrés

(Si jamais vous avez des idées de formatage, hésitez pas à me le faire savoir [MaitreRouge#1712](https://discord.gg/V5GMMGJ9ep))

----

## Index


Juste un rapide sommaire pour naviguer plus facilement dans la documentation

- [Codes erreur](#codes-erreur)
- [Account objects](#accounts-objects)
    - [Modules](#account-modules)
- [Servers.json](#server.json)

* [Login](#login)

----
## Reference

L'url de base utilisé est ``https://api.ecoledirecte.com/v3/`` (cette doc ne se base que sur la v3)

Dans presques toutes les requetes, on aura besoin d'un token utilisateur, il peut être obtenu par l'endpoint [login](#login)

Si jamais des informations sont a envoyer en ``POST``, il faudra alors obligatoirement les envoyer en ``plain text / raw`` (indiqué le cas contraire)

### Codes erreur

Liste de differents condes erreur trouvés au fil du temps avec leur description et des solutions pour fixer le pb

```
Code: 505
Problème: Les identifiants donnés à l'api sont erronés
Solution: Il faut vérifier que le nom d'utiliser et le mot de passe soient corrects

Code: 40129
Problème: Format JSON invalide
Solution: Vérifier que le body de la requete a bien été envoyé en raw (ou plain text) et qu'il respecte le formatage donné dans la documentation
```

### Accounts objects

Voici la structure détaillée d'un utilisateur (et commentée)

```js
{
    "idLogin": 1324, //int | ???
    "id": 1234,  //int | Numéro de compte
    "uid": "00000000000000000000000000000000", //string
    "identifiant": "Username", //string | Username du compte
    "typeCompte": "E", //string | Voir Type de compte dans la référence
    "codeOgec": "000000000", //string | ???
    "main": true, //bool | Indique si cet account est le principal (il peut en avoir plusieur comme avec un parent)
    "lastConnexion": "2021-10-05 18:28", //string | Date de dernière connexion à l'api via l'endpoint login (multiples connexions possibles)
    "civilite": "", 
    "prenom": "Jhon", 
    "particule": "", 
    "nom": "DOE", 
    "email": "email@example.com", 
    "anneeScolaireCourante": "2050-2051", 
    "nomEtablissement": "Github", 
    "logoEtablissement": "",
    "couleurAgendaEtablissement": "#1796b0",
    "dicoEnLigneLeRobert": false,
    "socketToken": "secret token", //string | ???
        "modules": [
          //Liste des modules, voir la référence pour plus
        ],
        "parametresIndividuels": {
          "lsuPoilDansLaMainBorne1": "", // ???
          "lsuPoilDansLaMainBorne2": "", // ???
          "lsuPoilDansLaMainBorne3": "", // ???
          "modeCalculLSU": "", // ???
          "isQrcode": false, // ???
          "modeAccessibiliteVisuelle": false,
          "typeSaisieNotesDefaut": "",
          "nbJoursMaxRenduDevoirCDT": "",
          "typeViewCDTDefaut": ""
        },
        "profile": {
          "sexe": "M",
          "infoEDT": "",
          "nomEtablissement": "Github",
          "idEtablissement": "0",
          "rneEtablissement": "0000000",
          "telPortable": "",
          "idReelEtab": "0",
          "photo": "//doc1.ecoledirecte.com/PhotoEleves/x/y.jpg",
          "classe": {
            "id": 44,
            "code": "TB",
            "libelle": "Terminale B",
            "estNote": 1
          }
        }
      }
```

### Account modules

Ces modules là sont ceux disponibles dans l'object account, ils ressemblent à ça :

```js
{
    "code": "CANTINE_BARCODE", //string | Nom du module
    "enable": false, //bool | Si le module est actif pour l'account en question
    "ordre": 1, //int | Position dans la sidebar
    "badge": 0, //int | ???
    "params": {} //object | Parametres du modules
}
```

Voici la liste des modules qui ont été documentés jusqu'a présent

```js
{
    "code": "CANTINE_BARCODE",
    "enable": false,
    "ordre": 1,
    "badge": 0,
    "params": {}
},
{
    "code": "VIE_SCOLAIRE",
    "enable": true,
    "ordre": 10,
    "badge": 0,
    "params": {}
},
{
    "code": "VIE_DE_LA_CLASSE",
    "enable": true,
    "ordre": 20,
    "badge": 0,
    "params": {}
},
{
    "code": "NOTES",
    "enable": true,
    "ordre": 30,
    "badge": 0,
    "params": {}
},
{
    "code": "CLOUD",
    "enable": false,
    "ordre": 90,
    "badge": 0,
    "params": {}
},
{
    "code": "MESSAGERIE",
    "enable": true,
    "ordre": 40,
    "badge": 0,
    "params": {
        "isActif": "1",
        "canParentsLireMessagesEnfants": "1",
        "destAdmin": "0",
        "destEleve": "0",
        "destFamille": "0",
        "destProf": "1",
        "destEspTravail": "0",
        "disabledNotification": "0",
        "notificationEmailEtablissement": "1",
        "choixMailNotification": "0",
        "autreMailNotification": "",
        "mailPro": "",
        "mailPerso": "",
        "messagerieApiVersion": "v3",
        "blackListProfActive": "0",
        "estEnBlackList": "0",
        "afficherToutesLesClasses": "0"
    }
},
{
    "code": "EDT",
    "enable": true,
    "ordre": 50,
    "badge": 0,
    "params": {}
},
{
    "code": "DOCUMENTS_ELEVE",
    "enable": true,
    "ordre": 71,
    "badge": 0,
    "params": {
        "DocumentsNotesActif": "1",
        "DocumentsVSActif": "1",
        "DocumentsAdministratifActif": "1"
    }
},
{
    "code": "CAHIER_DE_TEXTES",
    "enable": true,
    "ordre": 60,
    "badge": 0,
    "params": {
        "compteRenduSeance": "1",
        "compteRenduSeancePrevisionnel": "0",
        "isCDTPrimaire": "0"
    }
},
{
    "code": "MANUELS_SCOLAIRES",
    "enable": false,
    "ordre": 62,
    "badge": 0,
    "params": {}
},
{
    "code": "QCM",
    "enable": true,
    "ordre": 65,
    "badge": 0,
    "params": {}
},
{
    "code": "RESERVATIONS",
    "enable": false,
    "ordre": 80,
    "badge": 0,
    "params": {
        "regime": "Externe",
        "repasmidi_1": "0",
        "repassoir_1": "0",
        "repasmidi_2": "0",
        "repassoir_2": "0",
        "repasmidi_3": "0",
        "repassoir_3": "0",
        "repasmidi_4": "0",
        "repassoir_4": "0",
        "repasmidi_5": "0",
        "repassoir_5": "0",
        "repasmidi_6": "0",
        "repassoir_6": "0",
        "repasmidi_7": "0",
        "repassoir_7": "0"
    }
},
{
    "code": "COMMANDE_PASSAGE",
    "enable": false,
    "ordre": 81,
    "badge": 0,
    "params": {}
},
{
    "code": "CARNET_CORRESPONDANCE",
    "enable": false,
    "ordre": 70,
    "badge": 0,
    "params": {}
},
{
    "code": "ESIDOC",
    "enable": false,
    "ordre": 110,
    "badge": 0,
    "params": {}
},
{
    "code": "EDUNAO",
    "enable": false,
    "ordre": 100,
    "badge": 0,
    "params": {}
},
{
    "code": "CATER",
    "enable": false,
    "ordre": 90,
    "badge": 0,
    "params": {}
},
{
    "code": "ARD",
    "enable": false,
    "ordre": 120,
    "badge": 0,
    "params": {}
},
{
    "code": "PEARLTREES",
    "enable": false,
    "ordre": 170,
    "badge": 0,
    "params": {}
},
{
    "code": "EDUMALIN",
    "enable": false,
    "ordre": 171,
    "badge": 0,
    "params": {}
},
{
    "code": "SUIVI_STAGE",
    "enable": false,
    "ordre": 43,
    "badge": 0,
    "params": {}
},
{
    "code": "CLICKNPLAY",
    "enable": false,
    "ordre": 171,
    "badge": 0,
    "params": {}
},
{
    "code": "VOLTAIRE",
    "enable": false,
    "ordre": 175,
    "badge": 0,
    "params": {}
},
{
    "code": "ONISEPSERVICES",
    "enable": false,
    "ordre": 172,
    "badge": 0,
    "params": {}
},
{
    "code": "AVENRIA",
    "enable": false,
    "ordre": 173,
    "badge": 0,
    "params": {}
},
{
    "code": "SACOCHE",
    "enable": false,
    "ordre": 174,
    "badge": 0,
    "params": {}
},
{
    "code": "ETUDIANT",
    "enable": false,
    "ordre": 176,
    "badge": 0,
    "params": {}
},
{
    "code": "IJBOX",
    "enable": false,
    "ordre": 177,
    "badge": 0,
    "params": {}
},
{
    "code": "FUTURNESS",
    "enable": false,
    "ordre": 178,
    "badge": 0,
    "params": {}
},
{
    "code": "IMPALA",
    "enable": false,
    "ordre": 179,
    "badge": 0,
    "params": {}
},
{
    "code": "SITUATION_FINANCIERE",
    "enable": false,
    "ordre": 92,
    "badge": 0,
    "params": {}
}

```

### Servers.json

EcoleDirecte n'utilise pas qu'un seul serveur, il est possible d'obtenir des informations sur les serveurs du site en une seule requete.
La raison pour laquelle cette partie est dans la partie référence c'est car cela n'a pas trop d'utilitée a vraiment parler...

Request
```
    Endpoint: https://www.ecoledirecte.com/EDCluster/servers.json
    Endpoint information: On peut noter que cet endpoit prends un argumenent get, "c" qui semble optonnel jusqu'a présent
    Type of request: GET
    Body:
        None
    Headers:
        None
```

Response
```js
{
  "servers": [ //On va recevoir une liste d'objets comme celui ci dessous
    {
      "profile": "API", //string | Alterne enre API / APIP et ALL
      "lastCheck": "Mon Mar 16 2020 20:55:47 GMT+0100 (CET)", // ???
      "name": "api.ecoledirecte.com", //string | url du serveur
      "ip": "213.32.36.118", //string | ip du serveur
      "status": 1,//int | 1 = en marche; 2 = off ???
      "responseTime": 338.23671800643206, //float | ping
      "weigth": 3, //int | ???
      "timeout": false, //bool | Si le serveur a timeout
      "version": "Maj du 16/03/2020 à 16h27", //string, version logicielle du serveur
      "bdTested": "95", //string | ???
      "elapsedTime": 338, //int | ???
      "timingPhases": { //Object representatant la latence avec des détails
        "wait": 78.6058100014925,
        "dns": 3.143696002662182,
        "tcp": 7.182815000414848,
        "firstByte": 249.2012169957161,
        "download": 0.10318000614643097,
        "total": 338.23671800643206
      },
      "timings": {
        "socket": 78.6058100014925,
        "lookup": 81.74950600415468,
        "connect": 88.93232100456953,
        "response": 338.1335380002856,
        "end": 338.23671800643206
      },
      "httptested": "HTTP76",
      "nbConnexions": 1,//int | Nombre d'utilisateur connectés ??
      "errorCode": "ESOCKETTIMEDOUT"
    },
```

----
## Documentation

Ici se trouve toute la documentation, assurez vous d'avoir lu la référence avant de commencer 

### Login

Request
```
    Endpoint : https://api.ecoledirecte.com/v3/login.awp
    Type of request : POST
    Body : 
        data={
            "identifiant": "Username",
            "motdepasse": "Password"
        }
    Headers : 
        None
```

Response (200)
```js
{
  "code": 200,
  "token": "Super secret token here", //Token de connexion (+3100 long)
  "message": "", //Utilisé pour afficher des messages d'erreur
  "data": {
    "accounts": [
        //Liste d'utilisateur liés au compte, voir la référence pour plus
    ]
  }
}

```