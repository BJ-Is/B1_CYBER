## pour Lister tous les processus en cours d'exécution sur ma machine
 - on doit voir apparaître
le nom de chaque processus :
   - son identifiant unique (un nombre entier)
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-Process
```
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    140       9     2588       8344              8532   0 AggregatorHost
    597      21     7536      23412               296   0 AppHelperCap
    374      22    13852      29644       0,19  23444  86 ApplicationFrameHo
## 🌞 Trouver les 3 processus qui ont le plus petit identifiant


- leur nom et leur identifiant
- ce sont forcément des processus très importants : les premiers lancés par votre OS !
- pour le compte-rendu, isolez les 3 lignes qui les concernent dans la liste de tous les processus
```bash
PS C:\Users\jerem\OneDrive\Desktop> tasklist
```
Nom de l’image                 PID Nom de la sessio Numéro de s Utilisation
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0         8 Ko
System                           4 Services                   0       144 Ko
Secure System                  172 Services                   0    49 268 Ko
## 🌞 Lister tous les services de la machine...


- avec une commande, lister tous les services qui sont en cours d'exécution
```bash
PS PS C:\Users\jerem\OneDrive\Desktop> Get-Service
```
Status   Name               DisplayName
------   ----               -----------
Stopped  AarSvc_6879ea38    Agent Activation Runtime_6879ea38
Stopped  AJRouter           Service de routeur AllJoyn
Stopped  ALG                Service de la passerelle de la couc...
Running  AppIDSvc           Identité de l’application
- avec une autre commande, lister tous les services qui existent mais ne sont pas lancés


```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-Service | Where-Object {$_.Status -eq "Stopped"}
```
Status   Name               DisplayName
------   ----               -----------
Stopped  AarSvc_6879ea38    Agent Activation Runtime_6879ea38
Stopped  AJRouter           Service de routeur AllJoyn
Stopped  ALG                Service de la passerelle de la couc...
Stopped  AppReadiness       Préparation des applications
## 🌞 RAM
- afficher la quantité de RAM totale de la machine
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-WmiObject -Class Win32_ComputerSystem
```
Domain              : WORKGROUP
Manufacturer        : HP
Model               : Victus by HP Gaming Laptop 15-fa1xxx
Name                : HPVICTUSBJI
PrimaryOwnerName    : jeremieisraelbeugre@gmail.com
TotalPhysicalMemory : 16802762752
- afficher la quantité de RAM libre sur la machine


FreePhysicalMemory/1GB)
0,00567840412259102
## 🌞 CPU
- afficher l'utilisation du CPU
- ça peut être la charge CPU (CPU load) ou une utilisation en %
```bash
PS C:\Users\jerem\OneDrive\Desktop> get-counter
```
Timestamp                  CounterSamples
---------                  --------------
04/11/2024 17:23:24        \\hpvictusbji\interface réseau(realtek gaming
                           gbe family controller)\total des octets/s :
                           0


                           \\hpvictusbji\interface réseau(mediatek mt7921
                           wi-fi 6 802.11ax pcie adapter)\total des
                           octets/s :
                           13224,7366814687


                           \\hpvictusbji\processeur(_total)\% temps
                           processeur :
                           1,47179362901676


                           \\hpvictusbji\mémoire\pourcentage d’octets
                           dédiés utilisés :
                           73,5481008360042


                           \\hpvictusbji\mémoire\défauts de cache/s :
                           5,02650577022756


                           \\hpvictusbji\disque
                           physique(_total)\pourcentage du temps disque :
                           0,981672881602247


                           \\hpvictusbji\disque physique(_total)\taille de
                           file d’attente du disque actuelle :
                           0
## 🌞 Périphériques
- lister les périphériques de stockage
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-PnpDevice


Status     Class           FriendlyName
------     -----           ------------
OK         SoftwareComp... HP Application Enabling Services
OK         System          Ressources de la carte mère
OK         System          Ressources de la carte mère
OK         System          Ressources de la carte mère
OK         Mouse           ELAN Input Device
OK         HIDClass        Intel(R) HID Event Filter
OK         Computer        HP Victus by HP Gaming Laptop 15-fa1xxx
OK         MEDIA           Proxy de service de répartition Microsoft
OK         System          Contrôleur embarqué compatible ACPI Microsoft
Degraded   SoftwareComp... Intel(R) XTU Component Device
OK         Battery         Batterie à méthode de contrôle compatible ACP...
OK         Net             MediaTek MT7921 Wi-Fi 6 802.11ax PCIe Adapter
OK         System          Intel(R) PCI Express Root Port #5 - 51BC
OK         System          Agrégation de processeurs ACPI
OK         PrintQueue      File d’attente d’impression racine
OK         MTD             Realtek PCIE CardReader
OK         System          Contrôleur d'interruptions programmable
OK         System          Gestionnaire de volumes
OK         Bluetooth       Énumérateur Microsoft Bluetooth
OK         USB             Contrôleur hôte Intel(R) USB 3.20 eXtensible ...
OK         System          Intel(R) Serial IO GPIO Host Controller - INT...
OK         Net             WAN Miniport (PPPOE)
OK         System          Fournisseur de bus d’ordinateur virtuel Micro...
OK         Volume          Volume
OK         System          Pilote d’affichage de base Microsoft
OK         System          Intel(R) Host Bridge/DRAM Registers - 4649
OK         HIDClass        Pilote d’indicateur de portable ou de tablett...
```
- je veux voir les disques durs branchés à votre PC, pas les partitions
- genre je veux pas voir C: dans le retour de la commande
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-PnpDevice -Class 'USB'


Status     Class           FriendlyName                                                                     InstanceId
------     -----           ------------                                                                     ----------
OK         USB             Contrôleur hôte Intel(R) USB 3.20 eXtensible - 1.20 (Microsoft)                  PCI\VEN_...
OK         USB             Périphérique USB composite                                                       USB\VID_...
OK         USB             Périphérique USB composite                                                       USB\VID_...
OK         USB             Hub USB racine (USB 3.0)                                                         USB\ROOT...
OK         USB             Hub USB racine (USB 3.0)                                                         USB\ROOT...
OK         USB             Contrôleur hôte Intel(R) USB 3.10 eXtensible - 1.20 (Microsoft)                  PCI\VEN_...
```
### Partitions
- lister les partitions du système
- sur Windows, les partitions sont notamment C:, D: etc, mais y'en a d'autres qui ne sont pas utilisées actuellement et qui n'utilisent donc pas de lettres comme D:
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-Partition


   DiskPath : \\?\scsi#disk&ven_nvme&prod_sk_hynix_pc801_h#5&aac4e99&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}


PartitionNumber  DriveLetter Offset                                        Size Type
---------------  ----------- ------                                        ---- ----
1                           1048576                                     260 MB System
2                           273678336                                    16 MB Reserved
3                C           290455552                                475.91 GB Basic
4                           511294046208                                772 MB Recovery


```
### Espace disque
- afficher l'espace disque restant sur votre partition principale
- sur Windows, c'est C: la partition principale
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-CimInstance -Class Win32_LogicalDisk |
>>   Select-Object -Property DeviceID, Name, @{
>>     label='UsedSpace'
>>     expression={(($_.Size - $_.FreeSpace)/1GB).ToString('F2')}
>>   }


DeviceID Name UsedSpace
-------- ---- ---------
C:       C:   78,64


```
### 🌞 Cartes réseau
- afficher la liste des cartes réseau de votre PC
- on doit voit apparaître leur adresse IP et leur nom


```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-NetAdapter | fl Name, MacAddress




Name       : Connexion réseau Bluetooth
MacAddress : 20-0B-74-45-AA-9A


Name       : Ethernet
MacAddress : D0-AD-08-24-4E-82


Name       : Wi-Fi
MacAddress : 20-0B-74-45-AA-9B


```
### 🌞 Connexions réseau
- lister les connexions réseau actuellement en cours
- "actuellement en cours" c'est qu'elles sont dans l'état "établi" ou "established" en anglais
- on doit voir apparaître :
  - l'adresse IP du serveur auquel vous êtes connectés
  - le nom et/ou l'identifiant du processus responsable de cette connexion
```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-NetTCPConnection


LocalAddress                        LocalPort RemoteAddress                       RemotePort State       AppliedSetting
------------                        --------- -------------                       ---------- -----       --------------
::                                  63306     ::                                  0          Bound
::                                  51140     ::                                  0          Bound
::                                  51124     ::                                  0          Bound
::                                  49674     ::                                  0          Listen
::1                                 49673     ::                                  0          Listen
::                                  49672     ::                                  0          Listen
::                                  49667     ::                                  0          Listen
::                                  49666     ::                                  0          Listen
::                                  49665     ::                                  0          Listen
::                                  49664     ::                                  0          Listen
::                                  7680      ::                                  0          Listen
::                                  5357      ::                                  0          Listen
::                                  445       ::                                  0          Listen
::                                  135       ::                                  0          Listen
0.0.0.0                             58428     0.0.0.0                             0          Bound
0.0.0.0                             58427     0.0.0.0                             0          Bound
0.0.0.0                             57899     0.0.0.0                             0          Bound
0.0.0.0                             57785     0.0.0.0                             0          Bound
0.0.0.0                             57784     0.0.0.0                             0          Bound
0.0.0.0                             57783     0.0.0.0                             0          Bound
0.0.0.0                             57531     0.0.0.0                             0          Bound
0.0.0.0                             53299     0.0.0.0                             0          Bound
0.0.0.0                             53298     0.0.0.0                             0          Bound
0.0.0.0                             52920     0.0.0.0                             0          Bound
0.0.0.0                             52807     0.0.0.0                             0          Bound
0.0.0.0                             51143     0.0.0.0                             0          Bound
0.0.0.0                             51137     0.0.0.0                             0          Bound
0.0.0.0                             51136     0.0.0.0                             0          Bound
0.0.0.0                             51135     0.0.0.0                             0          Bound
0.0.0.0                             51134     0.0.0.0                             0          Bound
0.0.0.0                             51133     0.0.0.0                             0          Bound
0.0.0.0                             51128     0.0.0.0                             0          Bound
0.0.0.0                             51125     0.0.0.0                             0          Bound
0.0.0.0                             51121     0.0.0.0                             0          Bound
0.0.0.0                             51117     0.0.0.0                             0          Bound
0.0.0.0                             51102     0.0.0.0                             0          Bound
0.0.0.0                             51099     0.0.0.0                             0          Bound
0.0.0.0                             51096     0.0.0.0                             0          Bound
0.0.0.0                             51093     0.0.0.0                             0          Bound
0.0.0.0                             51080     0.0.0.0                             0          Bound
0.0.0.0                             51075     0.0.0.0                             0          Bound
0.0.0.0                             51074     0.0.0.0                             0          Bound
0.0.0.0                             51067     0.0.0.0                             0          Bound
0.0.0.0                             51063     0.0.0.0                             0          Bound
0.0.0.0                             51060     0.0.0.0                             0          Bound
0.0.0.0                             51055     0.0.0.0                             0          Bound
0.0.0.0                             51054     0.0.0.0                             0          Bound
0.0.0.0                             51053     0.0.0.0                             0          Bound
0.0.0.0                             51039     0.0.0.0                             0          Bound
0.0.0.0                             50998     0.0.0.0                             0          Bound
0.0.0.0                             50941     0.0.0.0                             0          Bound
0.0.0.0                             50940     0.0.0.0                             0          Bound
0.0.0.0                             50937     0.0.0.0                             0          Bound
0.0.0.0                             50926     0.0.0.0                             0          Bound
0.0.0.0                             50921     0.0.0.0                             0          Bound
0.0.0.0                             50902     0.0.0.0                             0          Bound
0.0.0.0                             50849     0.0.0.0                             0          Bound
0.0.0.0                             50844     0.0.0.0                             0          Bound
0.0.0.0                             50838     0.0.0.0                             0          Bound
0.0.0.0                             50791     0.0.0.0                             0          Bound
0.0.0.0                             50727     0.0.0.0                             0          Bound
0.0.0.0                             50682     0.0.0.0                             0          Bound
0.0.0.0                             50572     0.0.0.0                             0          Bound
0.0.0.0                             50496     0.0.0.0                             0          Bound
0.0.0.0                             50444     0.0.0.0                             0          Bound
0.0.0.0                             50443     0.0.0.0                             0          Bound
0.0.0.0                             50440     0.0.0.0                             0          Bound
0.0.0.0                             50439     0.0.0.0                             0          Bound
0.0.0.0                             50438     0.0.0.0                             0          Bound
0.0.0.0                             50437     0.0.0.0                             0          Bound
0.0.0.0                             50436     0.0.0.0                             0          Bound
0.0.0.0                             50396     0.0.0.0                             0          Bound
0.0.0.0                             50235     0.0.0.0                             0          Bound
0.0.0.0                             50071     0.0.0.0                             0          Bound
0.0.0.0                             49715     0.0.0.0                             0          Bound
0.0.0.0                             49713     0.0.0.0                             0          Bound
127.0.0.1                           65001     127.0.0.1                           52807      Established Internet
127.0.0.1                           65001     0.0.0.0                             0          Listen
10.3.220.120                        63306     10.3.220.113                        7680       Established Internet
10.3.220.120                        58428     192.229.221.95                      80         CloseWait   Internet
10.3.220.120                        58427     162.125.67.18                       443        CloseWait   Internet
10.3.220.120                        57899     64.233.166.188                      5228       Established Internet
10.3.220.120                        57531     20.199.120.85                       443        Established Internet
127.0.0.1                           52869     0.0.0.0                             0          Listen
127.0.0.1                           52807     127.0.0.1                           65001      Established Internet
10.3.220.120                        51143     142.250.178.131                     443        Established Internet
10.3.220.120                        51142     172.26.129.138                      53         TimeWait
10.3.220.120                        51141     172.26.129.138                      53         TimeWait
10.3.220.120                        51140     10.3.201.210                        7680       SynSent     Internet
10.3.220.120                        51139     216.239.34.157                      443        TimeWait
10.3.220.120                        51138     172.26.129.138                      53         TimeWait
10.3.220.120                        51137     3.64.143.176                        443        Established Internet
10.3.220.120                        51136     3.64.143.176                        443        Established Internet
10.3.220.120                        51135     3.64.143.176                        443        Established Internet
10.3.220.120                        51134     3.64.143.176                        443        Established Internet
10.3.220.120                        51133     3.64.143.176                        443        Established Internet
10.3.220.120                        51132     172.26.129.138                      53         TimeWait
10.3.220.120                        51131     172.26.129.138                      53         TimeWait
10.3.220.120                        51130     216.239.34.157                      443        TimeWait
10.3.220.120                        51129     172.26.129.138                      53         TimeWait
10.3.220.120                        51128     172.217.20.161                      443        Established Internet
10.3.220.120                        51127     172.26.129.138                      53         TimeWait
10.3.220.120                        51126     172.26.129.138                      53         TimeWait
10.3.220.120                        51125     172.217.20.206                      443        Established Internet
10.3.220.120                        51124     10.3.225.46                         7680       SynSent     Internet


```
### 🌞 Lister les utilisateurs de la machine
- on devrait voir au moins :
  - votre utilisateur
  - l'utilisateur qui est administrateur sur la machine


```bash
PS C:\Users\jerem\OneDrive\Desktop> Get-service|Get-Member




   TypeName : System.ServiceProcess.ServiceController


Name                      MemberType    Definition
----                      ----------    ----------
Name                      AliasProperty Name = ServiceName
RequiredServices          AliasProperty RequiredServices = ServicesDependedOn
Disposed                  Event         System.EventHandler Disposed(System.Object, System.EventArgs)
Close                     Method        void Close()
Continue                  Method        void Continue()
CreateObjRef              Method        System.Runtime.Remoting.ObjRef CreateObjRef(type requestedType)
Dispose                   Method        void Dispose(), void IDisposable.Dispose()
```