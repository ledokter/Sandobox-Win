# Configuration Personnalisée pour Windows Sandbox

[

Ce projet fournit un fichier de configuration `.wsb` simple pour lancer **Windows Sandbox** avec des paramètres personnalisés : un dossier partagé avec l'ordinateur hôte et l'accès réseau activé.

## Fonctionnalités

*   **Dossier Partagé** : Monte automatiquement le dossier `C:\SANDBOX` de votre machine hôte sur le bureau de la Sandbox.
*   **Accès en Lecture/Écriture** : Par défaut, le dossier partagé est accessible en lecture et en écriture.
*   **Réseau Activé** : La Sandbox a un accès complet au réseau, lui permettant de se connecter à Internet.

## Prérequis

*   **Système d'exploitation** : Windows 10/11 (éditions Pro, Entreprise ou Éducation).
*   **Fonctionnalité Windows** : La fonctionnalité "Bac à sable Windows" (Windows Sandbox) doit être activée.
    *   Pour l'activer : `Panneau de configuration` > `Programmes` > `Activer ou désactiver des fonctionnalités Windows` > Cochez `Bac à sable Windows`.

## Mode d'emploi

1.  **Créer le fichier de configuration** :
    *   Créez un nouveau fichier sur votre ordinateur.
    *   Nommez-le avec l'extension `.wsb` (par exemple, `MaSandbox.wsb`).

2.  **Copier le contenu** :
    *   Ouvrez ce fichier avec un éditeur de texte (comme Notepad, VS Code, etc.).
    *   Copiez-collez le code XML suivant à l'intérieur :

    ```xml
    <Configuration>
       <MappedFolders>
          <MappedFolder>
             <HostFolder>C:\SANDBOX</HostFolder>
             <ReadOnly>false</ReadOnly>
          </MappedFolder>
       </MappedFolders>
       <Networking>Enable</Networking>
    </Configuration>
    ```

3.  **Créer le dossier local** :
    *   Assurez-vous que le dossier `C:\SANDBOX` existe sur votre machine. S'il n'existe pas, créez-le. C'est ce dossier qui sera partagé avec la Sandbox.

4.  **Lancer la Sandbox** :
    *   Double-cliquez sur votre fichier `MaSandbox.wsb`.
    *   Windows Sandbox se lancera avec votre configuration personnalisée. Un raccourci vers le dossier `C:\SANDBOX` apparaîtra sur le bureau de la Sandbox.

## Personnalisation

Vous pouvez facilement modifier le fichier `.wsb` pour l'adapter à vos besoins.

### Changer le dossier partagé

Modifiez la ligne `<HostFolder>` pour pointer vers le dossier de votre choix.

```xml
<HostFolder>D:\MesProjets\Tests</HostFolder>
```

### Activer le mode lecture seule

Pour empêcher la Sandbox de modifier les fichiers dans le dossier partagé, passez la valeur de `<ReadOnly>` à `true`.

```xml
<ReadOnly>true</ReadOnly>
```

### Désactiver le réseau

Si vous n'avez pas besoin d'un accès réseau, vous pouvez supprimer la ligne `<Networking>Enable</Networking>` ou la passer à `Disable`.

```xml
<Networking>Disable</Networking>
```

## Licence

Ce projet est distribué sous la licence Apache 2.0. Voir le fichier `LICENSE` pour plus de détails.

Copyright 2025 LEDOKTER

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUTHOUT' WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
