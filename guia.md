# Guia tècnica de seguretat per a Digital World Art

**Gestor de contrasenyes (KeePass) i verificació en dos passos (Google Authenticator)**

---

## 1. Introducció

Aquesta guia explica, pas a pas, com ha de fer servir el personal de **Digital World Art** dues eines que protegeixen els comptes i la informació de l'empresa:

1. **KeePass**, un gestor de contrasenyes, per desar-hi totes les contrasenyes de forma segura.
2. **Google Authenticator**, una aplicació del mòbil que genera un codi extra per entrar als comptes (verificació en dos passos, o 2FA).

> Les captures de pantalla es troben a la carpeta `img/` del repositori.

## 2. Per què cal fer-ho?

Una empresa del sector digital i creatiu treballa amb dades de clients, projectes i comptes en línia (correu, núvol, xarxes socials, servidors). Si algú aconsegueix una sola contrasenya, pot accedir a tot això. Els problemes més habituals són:

- Fer servir **la mateixa contrasenya** a molts serveis: si se'n filtra una, cauen totes.
- Fer servir contrasenyes **curtes o fàcils d'endevinar**.
- Apuntar les contrasenyes en papers, fulls de càlcul o missatges.
- Que algú robi una contrasenya (per exemple amb un correu fals de *phishing*) i entri al compte sense que ningú se n'adoni.

Les dues eines resolen aquests problemes:

| Problema | Solució |
|---|---|
| Massa contrasenyes per recordar | KeePass les guarda totes; només cal recordar-ne una |
| Contrasenyes dèbils o repetides | El generador de KeePass crea contrasenyes llargues i úniques |
| Contrasenya robada | El 2FA demana un segon codi del mòbil, així que la contrasenya sola no serveix |

## 3. Eines recomanades i justificació

Es van comparar dos gestors de contrasenyes: **Bitwarden** i **KeePass**. La nostra proposta per a Digital World Art és **KeePass**, juntament amb **Google Authenticator** per al 2FA.

### Per què KeePass?

- **Gratuït i de codi obert:** no té cost de llicències per a l'empresa.
- **Les dades es queden a l'empresa:** la base de dades és un únic arxiu (`.kdbx`) xifrat, que no depèn de cap servidor extern.
- **Molt segur:** fa servir algorismes de xifratge reconeguts (AES, ChaCha20, Twofish).
- **Funciona sense connexió** i es pot configurar a mida (grups, perfils del generador, arxiu clau).

El punt més fluix de KeePass és que és una mica menys còmode que Bitwarden (no sincronitza sola entre dispositius i cal fer les còpies de seguretat manualment). Per això aquesta guia inclou un apartat de còpies de seguretat.

### Per què Google Authenticator?

- L'empresa ja fa servir comptes de Google, i l'aplicació s'hi integra directament.
- És gratuïta, senzilla i funciona en Android i iPhone.
- Els codis es generen al mòbil, sense necessitat de cobertura.

## 4. KeePass: instal·lació i configuració inicial

### 4.1 Descàrrega i instal·lació

1. Obrir el navegador i anar a la web oficial: **https://keepass.info**.
2. Entrar a l'apartat **Downloads** i descarregar l'instal·lador (*Installer*) per a Windows.
3. Executar l'arxiu descarregat i seguir l'assistent (acceptar la llicència i deixar les opcions per defecte).
4. Obrir KeePass des del menú d'inici.

![Web oficial de KeePass](img/keepass-01-web.png)
*Figura 1. Web oficial de KeePass, d'on es descarrega el programa.*

En obrir-lo per primera vegada, la finestra principal apareix buida perquè encara no hi ha cap base de dades.

![Finestra principal buida](img/keepass-02-finestra-buida.png)
*Figura 2. Finestra principal de KeePass sense cap base de dades.*

### 4.2 Creació de la base de dades

1. Anar a **File > New** (o prémer `Ctrl+N`).
2. Triar la carpeta i posar-li un nom. En aquest cas: `Base_datos_empresa.kdbx`, a la carpeta Documents.
3. Fer clic a **Guardar**.

![Nom i ubicació de la base de dades](img/keepass-03-guardar-bd.png)
*Figura 3. Selecció del nom i la ubicació de la nova base de dades.*

### 4.3 Creació de la clau mestra

KeePass demana ara la **clau mestra**. És l'única contrasenya que cal recordar i protegeix tot el contingut. Escriviu-la i repetiu-la al camp inferior.

![Creació de la clau mestra](img/keepass-04-clau-mestra.png)
*Figura 4. Creació de la clau mestra.*

**Consells per a la clau mestra:**

- Ha de ser **llarga**: millor una frase de 14 caràcters o més que una paraula amb números.
- No l'han de saber ni l'han d'apuntar altres persones.
- **Si s'oblida, no es pot recuperar** i es perden totes les contrasenyes.
- Opcionalment es pot afegir un **arxiu clau** com a segon element de protecció. Si es perd, la base de dades no es pot obrir, així que se n'ha de guardar una còpia en un lloc diferent.

> L'indicador de qualitat de la captura (50 bits) és massa baix per a ús real. A l'empresa s'ha de fer servir una clau més llarga.

Un cop creada, la base de dades apareix amb uns grups per defecte (General, Windows, Network, Internet, eMail, Homebanking) i unes entrades d'exemple que es poden esborrar.

![Base de dades creada](img/keepass-05-bd-creada.png)
*Figura 5. Base de dades creada, amb els grups per defecte.*

## 5. KeePass: generar contrasenyes segures

KeePass inclou un generador de contrasenyes. S'hi accedeix des de **Tools > Password Generator** o des del botó del generador en crear una entrada.

- **Longitud:** com més llarga, més segura. Mínim recomanat: **16 caràcters** (a la captura se n'han fet servir 20).
- **Tipus de caràcters:** majúscules, minúscules i dígits com a mínim. Afegir símbols augmenta la seguretat, però alguns serveis no els accepten.
- **Perfil:** es poden desar perfils diferents (per exemple, un sense símbols per a serveis restrictius).

![Opcions del generador](img/keepass-06-generador.png)
*Figura 6. Opcions del generador de contrasenyes (longitud 20; majúscules, minúscules i dígits).*

Una contrasenya generada de 20 caràcters assoleix uns 105 bits de qualitat, molt per sobre d'una contrasenya triada a mà. **Cada servei ha de tenir una contrasenya diferent.**

## 6. KeePass: ús diari

### 6.1 Desar el compte de correu de l'empresa

1. Seleccionar el grup **eMail** a l'arbre de l'esquerra.
2. Fer clic a **Entry > Add Entry** (o `Ctrl+I`).
3. Omplir el **Title** (nom descriptiu), el **User name** (adreça de correu) i la **URL** del servei.
4. A **Password**, utilitzar el generador (icona de la clau) per crear una contrasenya segura.
5. Fer clic a **OK** i desar la base de dades amb `Ctrl+S`.

![Nova entrada](img/keepass-07-nova-entrada.png)
*Figura 7. Nova entrada "Correu corporatiu" amb contrasenya generada (105 bits, 20 caràcters).*

Per **modificar** una entrada, es fa doble clic damunt seu (o **Entry > Edit Entry**). Es poden canviar l'usuari, la contrasenya o la URL, i KeePass desa un historial de versions.

![Edició d'una entrada](img/keepass-08-editar-entrada.png)
*Figura 8. Edició d'una entrada existent.*

Un cop desada, l'entrada apareix al grup eMail i la contrasenya queda amagada amb asteriscs.

![Entrada desada](img/keepass-09-entrada-desada.png)
*Figura 9. Entrada del correu desada al grup eMail.*

### 6.2 Desar altres comptes o serveis web

El procés és el mateix, però es tria el grup més adequat (Internet, Network, etc.):

1. Seleccionar el grup i fer **Entry > Add Entry**.
2. Posar com a *Title* el nom del servei (p. ex. "Panell d'administració del servidor") i omplir *User name* i *URL*.
3. Generar una contrasenya única amb el generador i acceptar amb **OK**.
4. Si cal, afegir informació extra al camp **Notes** (per exemple, el rol de l'usuari), **sense incloure-hi contrasenyes**.

> **Recomanació:** a la URL, deixeu només l'adreça (`https://...`), sense claudàtors ni parèntesis, perquè l'emplenament automàtic funcioni bé.

### 6.3 Emplenament automàtic

KeePass pot escriure l'usuari i la contrasenya per nosaltres, sense haver-les de copiar a mà:

- **Auto-Type (inclòs a KeePass):** s'obre la pàgina d'inici de sessió, es fa clic al camp d'usuari i es prem `Ctrl+Alt+A`. KeePass busca l'entrada que coincideix i escriu usuari i contrasenya.
- **Extensió del navegador:** KeePassXC (variant de KeePass) té l'extensió *KeePassXC-Browser* per a Edge, Chrome i Firefox. Amb KeePass 2.x, l'equivalent és el connector KeePassRPC amb l'extensió Kee.
- **Còpia puntual:** clic dret a l'entrada i triar **Copy Password** o **Copy User Name**. El porta-retalls s'esborra automàticament al cap d'uns segons.

## 7. KeePass: còpies de seguretat

Tota la informació és dins d'un únic arxiu (`Base_datos_empresa.kdbx`), així que fer la còpia és tan simple com copiar-lo.

### 7.1 Com fer la còpia

1. Desar els canvis (`Ctrl+S`).
2. Anar a **File > Save As > Save to File** i triar la ubicació de la còpia (per exemple, un USB), o bé tancar KeePass i copiar l'arxiu des de la carpeta Documents.
3. Comprovar que la còpia s'obre correctament amb la clau mestra (**File > Open**).
4. Si s'utilitza un arxiu clau, fer-ne també una còpia i guardar-la en un lloc diferent.

### 7.2 Bones pràctiques

- **USB xifrat:** guardar la còpia en un USB protegit amb BitLocker To Go (clic dret a la unitat > *Activar BitLocker*) i desar-lo en un lloc segur.
- **Núvol xifrat:** pujar la còpia a un servei empresarial amb xifratge i verificació en dos passos.
- **Regla 3-2-1:** tres còpies, en dos suports diferents, una d'elles fora de l'oficina.
- **Separar secrets:** no guardar mai la clau mestra ni l'arxiu clau al mateix lloc que la còpia.
- **Periodicitat:** fer una còpia després de cada canvi important i, com a mínim, una vegada al mes. Provar de restaurar-la de tant en tant.

## 8. Verificació en dos passos amb Google Authenticator

### 8.1 Què és?

És una manera de protegir el compte. A més de la contrasenya, el compte demana un **codi que surt al mòbil**. Així, si algú sap la contrasenya, no pot entrar igualment.

### 8.2 Què es necessita?

- Un mòbil (Android o iPhone).
- L'aplicació **Google Authenticator**, que és a Google Play o a l'App Store.
- L'usuari i la contrasenya del compte de Google de l'empresa.

### 8.3 Passos per activar-la

**Pas 1.** Instal·lar Google Authenticator al mòbil.

**Pas 2.** Entrar al Compte de Google i fer clic a **Seguretat i inici de sessió**. Es veurà que la verificació en dos passos està desactivada.

![Pantalla de seguretat](img/2fa-01-seguretat.png)
*Imatge 1. Pantalla de seguretat del Compte de Google.*

**Pas 3.** Fer clic a **Verificació en dos passos**. A l'apartat "Segon pas" hi ha diferents opcions. Escollir **Authenticator**.

![Opcions de segon pas](img/2fa-02-segon-pas.png)
*Imatge 2. Opcions de segon pas.*

**Pas 4.** Surt un codi QR a la pantalla. Al mòbil, obrir l'aplicació, tocar el botó **+** i escollir **Escaneja un codi QR**. Escanejar el QR i fer clic a **Següent**.

![Codi QR](img/2fa-03-qr.png)
*Imatge 3. Codi QR per vincular l'aplicació.*

**Pas 5.** L'aplicació mostra un codi de 6 números. Escriure'l a l'ordinador. *Compte: el codi canvia cada poc temps.*

![Autenticador afegit](img/2fa-04-autenticador-afegit.png)
*Imatge 4. Autenticador afegit.*

**Pas 6.** Fer clic a **Activa la verificació en dos passos**. Quan surti el missatge de confirmació, fer clic a **Fet**.

![Verificació activada](img/2fa-05-activada.png)
*Imatge 5. Verificació en dos passos activada.*

### 8.4 Com s'entra al compte a partir d'ara?

1. Escriure l'usuari i la contrasenya.
2. Google demana confirmar des del mòbil. Per usar l'aplicació, fer clic a **Provar una altra manera**.
3. Escollir l'aplicació d'autenticació i escriure el codi de 6 números que surt al mòbil.

### 8.5 Codis de seguretat

Genereu els **10 codis de seguretat d'un sol ús**. Serveixen si no es té el mòbil o no hi ha cobertura. Descarregueu-los o imprimiu-los i **guardeu-los en un lloc segur** (mai al mateix lloc que el mòbil).

## 9. Resum de bones pràctiques

- Una **clau mestra llarga**, que només sap la persona que la fa servir.
- **Una contrasenya diferent** per a cada servei, generada amb KeePass.
- **2FA activat** a tots els comptes importants (correu, núvol, administració).
- **Còpies de seguretat** de l'arxiu `.kdbx`, provades i guardades en llocs segurs.
- Mai compartir contrasenyes per correu, xat o paper.
- Si se sospita que un compte s'ha vist compromès, **canviar-ne la contrasenya immediatament** i avisar el responsable de seguretat.
