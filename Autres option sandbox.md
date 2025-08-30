<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# quelles serait les autres option a ajouter pour avoir une super sandbox avec aces au réseau local et le plus d'option possible, activer windows 11

Absolument. Pour créer une "super sandbox" sur Windows 11 avec un maximum de fonctionnalités, notamment un accès complet au réseau local et des options d'automatisation, vous pouvez enrichir votre fichier de configuration `.wsb`.

Voici un fichier de configuration avancé et commenté qui inclut la plupart des options disponibles.[^1]

### Fichier de Configuration Avancé pour une "Super Sandbox"

Créez un fichier avec l'extension `.wsb` (par exemple, `SuperSandbox.wsb`) et copiez-y le contenu suivant. Ce fichier est conçu pour vous donner un maximum de contrôle et de fonctionnalités.

```xml
<Configuration>
    <!-- Accélération graphique matérielle -->
    <VGpu>Enable</VGpu>

    <!-- Accès au réseau (par défaut, activé) -->
    <Networking>Enable</Networking>

    <!-- Partage de dossiers de l'hôte vers la Sandbox -->
    <MappedFolders>
        <MappedFolder>
            <!-- Dossier sur votre machine (hôte) -->
            <HostFolder>C:\SANDBOX\Partage</HostFolder>
            <!-- Dossier correspondant sur le bureau de la Sandbox -->
            <SandboxFolder>C:\Users\WDAGUtilityAccount\Desktop\PartageHote</SandboxFolder>
            <!-- Autoriser l'écriture depuis la Sandbox -->
            <ReadOnly>false</ReadOnly>
        </MappedFolder>
    </MappedFolders>

    <!-- Exécuter des commandes au démarrage de la Sandbox -->
    <LogonCommand>
        <Command>powershell.exe -ExecutionPolicy Unrestricted -File "C:\Users\WDAGUtilityAccount\Desktop\PartageHote\install_apps.ps1"</Command>
    </LogonCommand>

    <!-- Partage des périphériques -->
    <AudioInput>Enable</AudioInput>
    <VideoInput>Enable</VideoInput>
    <PrinterRedirection>Enable</PrinterRedirection>

    <!-- Partage du presse-papiers (activé par défaut) -->
    <ClipboardRedirection>Enable</ClipboardRedirection>

    <!-- Allouer plus de mémoire vive à la Sandbox (en Mo) -->
    <MemoryInMB>8192</MemoryInMB>

    <!-- Mode de sécurité renforcé (peut parfois limiter certaines interactions) -->
    <ProtectedClient>Enable</ProtectedClient>
</Configuration>
```


### Détail des Options Clés pour une "Super Sandbox"

* **Accès au Réseau Local et Internet**
L'option `<Networking>Enable</Networking>` est la clé. Par défaut, Windows Sandbox utilise un commutateur virtuel Hyper-V qui lui donne accès à votre réseau local et à Internet. Vous n'avez rien de plus à faire pour que cela fonctionne.[^2]
* **Script de Démarrage (`LogonCommand`)**
C'est la fonctionnalité la plus puissante pour l'automatisation. Dans l'exemple ci-dessus, la sandbox exécute automatiquement un script PowerShell (`install_apps.ps1`) dès son lancement. Vous pouvez utiliser ce script pour :[^3][^4]
    * Installer des logiciels (avec Chocolatey ou Winget).
    * Configurer des paramètres Windows.
    * Télécharger des fichiers nécessaires.
    * Mapper des lecteurs réseau.

**Exemple de script `install_apps.ps1` à placer dans `C:\SANDBOX\Partage` :**

```powershell
# Installer des logiciels courants
winget install --id=Mozilla.Firefox -e --accept-package-agreements
winget install --id=Microsoft.VisualStudioCode -e --accept-package-agreements

# Créer un raccourci vers un serveur local
$Shell = New-Object -ComObject WScript.Shell
$Shortcut = $Shell.CreateShortcut("$Home\Desktop\ServeurNAS.lnk")
$Shortcut.TargetPath = "\\192.168.1.100\partage" # Adaptez l'adresse IP
$Shortcut.Save()
```

* **Allocation de Mémoire (`MemoryInMB`)**
Par défaut, la Sandbox peut être lente. Allouer plus de RAM via `<MemoryInMB>8192</MemoryInMB>` (pour 8 Go) améliore considérablement ses performances, surtout si vous utilisez des applications gourmandes.[^1]
* **Dossier Partagé Avancé (`MappedFolders`)**
Au lieu de simplement monter un dossier, vous pouvez spécifier un `SandboxFolder` pour choisir exactement où le dossier partagé apparaît dans la Sandbox, ce qui est plus propre qu'un simple raccourci sur le bureau.[^4]
* **Partage des Périphériques**
    * `<AudioInput>Enable</AudioInput>` : Partage le microphone de l'hôte.[^1]
    * `<VideoInput>Enable</VideoInput>` : Partage la webcam de l'hôte.[^1]
    * `<PrinterRedirection>Enable</PrinterRedirection>` : Permet d'imprimer depuis la Sandbox sur les imprimantes de l'hôte.[^1]


### Comment "Activer" Windows 11 dans la Sandbox ?

La Sandbox exécute **une image propre et à jour du système d'exploitation Windows installé sur votre machine hôte**. Si votre PC tourne sous Windows 11, la Sandbox lancera automatiquement une version de Windows 11. Il n'y a donc rien à "activer" : elle utilise une licence virtuelle liée à celle de votre système hôte.[^5]

Pour avoir une "super sandbox", l'essentiel est d'utiliser la puissance du `LogonCommand` pour automatiser l'installation et la configuration, vous évitant ainsi de tout refaire manuellement à chaque lancement.
<span style="display:none">[^10][^6][^7][^8][^9]</span>

<div style="text-align: center">⁂</div>

[^1]: https://learn.microsoft.com/fr-fr/windows/security/application-security/application-isolation/windows-sandbox/windows-sandbox-configure-using-wsb-file

[^2]: https://learn.microsoft.com/en-us/windows/security/application-security/application-isolation/windows-sandbox/windows-sandbox-configure-using-wsb-file

[^3]: https://www.it-connect.fr/installation-et-configuration-de-windows-sandbox/

[^4]: https://gist.github.com/QNimbus/83a86ee072d2b4dbfd13f2fe901796df

[^5]: https://learn.microsoft.com/fr-fr/windows/security/application-security/application-isolation/windows-sandbox/

[^6]: https://lecrabeinfo.net/tutoriels/windows-sandbox-comment-utiliser-le-bac-a-sable-de-windows-10/

[^7]: https://v2.ttrinfo.be/articles/os/virtualisation/sandbox-configuration/sandbox-configuration.pdf

[^8]: https://www.zebulon.fr/astuces/securite-systeme/comment-utiliser-la-sandbox-de-windows-10.html

[^9]: https://www.dannymoran.com/windows-sandbox-configuration/

[^10]: https://www.reddit.com/r/Windows10/comments/z6ecir/windows_sandbox_and_lan/?tl=fr

