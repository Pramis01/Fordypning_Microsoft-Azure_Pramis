# Azure Fordypningsprosjekt – Azure CLI

## Prosjektoversikt

Dette prosjektet er en del av mitt fordypningsfag, hvor jeg lærer å bruke skytjenester gjennom Microsoft Azure. Fokus så langt har vært på bruk av Azure CLI for å administrere ressurser.

---

## Hva jeg har lært

### Installasjon av Azure CLI

For å kunne bruke Azure fra terminalen på Mac, installerte jeg Azure CLI ved hjelp av Homebrew.

Kommando:

```
brew install azure-cli
```

Dette installerer Azure CLI slik at jeg kan kjøre Azure-kommandoer direkte fra terminalen.

---

### Innlogging i Azure via CLI

Etter installasjonen koblet jeg Azure-kontoen min til CLI.

Kommando:

```
az login
```

Når jeg kjørte kommandoen, ble jeg sendt videre til nettleseren hvor jeg logget inn med Microsoft-kontoen min. Etter innlogging ble kontoen koblet til terminalen.

---

### Valg av abonnement (Subscription)

Etter innlogging måtte jeg velge hvilket abonnement jeg skulle bruke. Jeg har et gratis abonnement, og valgte dette.

Dette abonnementet brukes når jeg oppretter og administrerer ressurser i Azure.

---

### Opprettelse av Resource Group

#### Hva er en Resource Group

En Resource Group er en samling av ressurser i Azure, for eksempel virtuelle maskiner, databaser og nettverk. Den brukes til å organisere og administrere relaterte ressurser.

#### Kommando brukt

```
az group create --name Project-Name --location northeurope
```

#### Forklaring

* `--name`: Navnet på resource groupen
* `--location`: Hvilken region ressursene blir opprettet i

---

### Vise liste over Resource Groups

For å se hvilke resource groups jeg har opprettet, brukte jeg følgende kommando:

```
az group list --output table
```

#### Forklaring

* Viser alle resource groups i abonnementet
* `--output table` gjør at resultatet vises som en tabell, som er lettere å lese

---

### Slette en Resource Group

For å slette en resource group brukte jeg følgende kommando:

```
az group delete --name Project-Name --yes
```

#### Forklaring

* `--name`: Navnet på resource groupen som skal slettes
* `--yes`: Bekrefter slettingen automatisk uten ekstra spørsmål

Når en resource group slettes, blir alle ressursene som ligger inni også slettet.

---

## Refleksjon

Gjennom dette arbeidet har jeg lært grunnleggende bruk av Azure CLI, hvordan jeg kobler til en konto, og hvordan jeg kan opprette, vise og slette ressurser. Dette gir en god forståelse for hvordan man kan administrere skyressurser på en strukturert måte.

## Azure Fordypningsprosjekt – Fase 1: Virtuell maskin (VM)

### Opprettelse av virtuell maskin

Jeg opprettet en virtuell maskin ved hjelp av Azure-portalen i Microsoft Azure. Under opprettelsen valgte jeg et Ubuntu-operativsystem. Prosessen ligner på opprettelse av en vanlig virtuell maskin, hvor man må konfigurere blant annet lagring, nettverk og brukerinformasjon.

Jeg valgte brukernavn og passord som senere ble brukt for innlogging til serveren.

---

### Tilkobling til VM via SSH

Etter at den virtuelle maskinen var opprettet, kopierte jeg den offentlige IP-adressen (Public IP). Denne brukes for å koble til serveren eksternt.

Jeg koblet til VM-en via terminalen ved hjelp av SSH med følgende kommando:

```id="vmssh01"
ssh Pramis01@20.2.86.50
```

Her er:

* `Pramis01` brukernavnet jeg opprettet
* `20.2.86.50` den offentlige IP-adressen til VM-en

Ved første tilkobling måtte jeg bekrefte forbindelsen og deretter skrive inn passordet jeg valgte under opprettelsen.

**Skjermbilde: SSH-tilkobling i terminal **
![SSH tilkobling i terminal](Bilder/Virtual_Machine/SSH_tilkobling-i-terminal.png)

---

### Oppdatering av system og installasjon av Nginx

Når jeg var koblet til serveren, oppdaterte jeg først pakkelisten for systemet:

```id="vmcmd01"
sudo apt update
```

Deretter installerte jeg webserveren Nginx:

```id="vmcmd02"
sudo apt install nginx -y
```

Dette installerer og setter opp en enkel webserver på den virtuelle maskinen.

**Skjermbilde: Installasjon av Nginx i terminal**
![Installsjon av Nginx Server](Bilder/Virtual_Machine/Installing_Nginx_Server.png)

---

### Testing av webserver

Etter installasjonen testet jeg webserveren ved å åpne den offentlige IP-adressen i en nettleser. Hvis installasjonen var vellykket, vises standard Nginx-side.

Dette bekrefter at serveren er tilgjengelig over internett og at webserveren fungerer som forventet.

**Skjermbilde: Nginx standard side i nettleser**
![Running Nginx Server](Bilder/Virtual_Machine/Running_Nginx_Server.png)
---

## Refleksjon

Gjennom dette arbeidet har jeg lært hvordan man oppretter og konfigurerer en virtuell maskin i Azure, samt hvordan man kobler til en server ved hjelp av SSH. Jeg har også fått praktisk erfaring med Linux-kommandoer og installasjon av tjenester som Nginx.

Jeg har forstått viktigheten av offentlig IP-adresse for ekstern tilgang, og hvordan en server kan brukes til å levere tjenester over nettverk.

# Azure Fordypningsprosjekt – Fase 2: Networking

## Prosjektoversikt
I denne fasen har jeg jobbet med nettverk (Networking) i Microsoft Azure. Målet var å forstå hvordan trafikk til en virtuell maskin styres ved hjelp av Network Security Groups (NSG), og hvordan regler som Allow og Deny påvirker tilgang til serveren.

---

## Hva jeg har gjort

### 1. Analyse av nettverk til virtuell maskin
Jeg undersøkte nettverksoppsettet til den virtuelle maskinen i Azure-portalen.

Jeg fant og dokumenterte følgende informasjon:
- Public IP-adresse
- Private IP-adresse
- Virtual Network (VNet)
- Network Security Group (NSG)

**Skjermbilde: Nettverksinformasjon for VM**  
![VM nettverksinformasjon](Bilder/Networking/Network_Informasjon.png)

---

### 2. Testing av Allow- og Deny-regel (port 80)

Jeg opprettet og testet inbound regler i Network Security Group (NSG) for å kontrollere trafikk til den virtuelle maskinen.

Først opprettet jeg en **Allow-regel** på port 80 (HTTP), som gjør at webserveren (nginx) er tilgjengelig fra internett via VM sin offentlige IP-adresse.

Deretter opprettet jeg en **Deny-regel** på samme port, som blokkerer all innkommende trafikk. Når denne regelen er aktiv, blir nettsiden utilgjengelig i nettleseren.

Dette viser hvordan NSG fungerer som en brannmur som styrer tilgang til serveren basert på regler og prioritet.

**Skjermopptak: Allow og Deny-regler i NSG (samlet)**  
Video som viser opprettelse av Allow og Deny rule:

Dette skjermopptaket viser hele prosessen med opprettelse av Allow og Deny-regler i Azure NSG.
[Åpne video](Bilder/Networking/Making_Allow&Deny_InnboundRules.mov)

---

---

## Hva jeg har lært

I denne fasen har jeg lært:

- Hva et Virtual Network (VNet) er
- Forskjellen mellom public og private IP-adresser
- Hvordan Network Security Groups (NSG) fungerer
- Hvordan inbound rules kontrollerer tilgang til en server
- Hvordan Allow og Deny påvirker nettverkstrafikk
- Hvordan prioritet i regler påvirker hvilke regler som gjelder

---

## Refleksjon

Gjennom dette arbeidet har jeg fått en bedre forståelse av hvordan nettverk i skyen fungerer. Jeg har sett i praksis hvordan en server kan være tilgjengelig eller utilgjengelig basert på brannmurregler.

Dette har gitt meg en mer praktisk forståelse av IT-drift og hvordan sikkerhet i nettverk håndteres i Azure.

---

## Konklusjon

Jeg har nå gjennomført grunnleggende networking i Azure og forstått hvordan trafikk til en virtuell maskin kan kontrolleres. Dette er en viktig del av cloud computing og IT-drift.

## Azure Fordypningsprosjekt – Fase 3: Storage i Azure (Blob Storage)

### Opprettelse av Storage Account
I denne fasen opprettet jeg en Storage Account i Microsoft Azure for å lagre filer i skyen. Jeg brukte samme resource group som tidligere og valgte region North Europe.

En Storage Account er en tjeneste i Azure som brukes til å lagre data som filer, bilder og dokumenter. Den fungerer uavhengig av virtuelle maskiner.

**Skjermbilde: Opprettelse av Storage Account**  
![Opprettelse av Storage Account](Bilder/Storage_Account/Creating_storage_account.png)
![Opprettelse av Storage Account](Bilder/Storage_Account/Creating_Storage_account_2.png)
![Opprettelse av Storage Account](Bilder/Storage_Account/Creating_storage_account_3.png)

---

### Opprettelse av Blob Container
Etter at Storage Account var opprettet, opprettet jeg en container for lagring av filer.

- Navn: files  
- Tilgangsnivå: Private (standard)

En Blob Container fungerer som en mappe hvor filer (blobs) lagres i skyen.

**Skjermbilde: Opprettelse av container**  
![Opprettelse av container](Bilder/Storage_Account/Creating_Container.png)
![Opprettelse av container](Bilder/Storage_Account/Creating_Container_2.png)

---

### Opplasting av filer
Jeg lastet opp bilder til containeren ved hjelp av Azure-portalen.

Dette viser hvordan filer kan lagres i skyen uten å være avhengig av lokal lagring eller en virtuell maskin.

**Skjermbilde: Opplasting av filer**  
![Opplasting av filer](Bilder/Storage_Account/Uploading_files.png)
![Opplasting av filer](Bilder/Storage_Account/Uploading_Files_2.png)

---

### Testing av tilgang
Jeg testet tilgang ved å åpne filens URL i nettleseren. Først fikk jeg en feilmelding fordi offentlig tilgang ikke var tillatt.

Dette skyldes at Azure blokkerer offentlig tilgang som standard av sikkerhetsgrunner.

For å løse dette:
- Aktiverte jeg "Allow Blob Public Access" på Storage Account  
- Endret tilgangsnivå på container til "Blob (anonymous read access)"  

Etter dette kunne filene åpnes via nettleser ved hjelp av URL.

**Skjermbilde: Testing av tilgang til fil**  
![Testing av tilgang](Bilder/Storage_Account/No_blob_access.png)
![Testing av tilgang](Bilder/Storage_Account/Testing_File_Error.png)
![Testing av tilgang](Bilder/Storage_Account/blob_acces.png)
![Testing av tilgang](Bilder/Storage_Account/Testing_File_Access.png)

---

### Forskjell på VM storage og Cloud storage

VM storage er lokal lagring som tilhører den virtuelle maskinen. Denne lagringen brukes av operativsystemet og applikasjoner som kjører på VM-en.

Cloud storage (Blob Storage) brukes til å lagre filer separat fra VM-en. Disse filene kan nås via internett og er ikke knyttet til én spesifikk maskin.

---

### Hva jeg har lært
I denne fasen har jeg lært:

- Hva en Storage Account er  
- Hva Blob Storage er  
- Hvordan Blob Containers brukes til å organisere filer  
- Hvordan laste opp filer til skyen  
- Hvordan teste tilgang til filer via nettleser  
- At Azure blokkerer offentlig tilgang som standard  

---

### Refleksjon
Gjennom denne fasen har jeg fått en bedre forståelse av hvordan data kan lagres i skyen uavhengig av virtuelle maskiner. Jeg har også sett hvordan sikkerhetsinnstillinger påvirker tilgjengeligheten til filer, og hvordan disse må konfigureres riktig.

Dette gir en praktisk forståelse av hvordan cloud storage fungerer i Azure.

# Azure Fordypningsprosjekt – Fase 4: IAM (Identity and Access Management)

### Tilgangsstyring i Azure
I denne fasen jobbet jeg med IAM (Identity and Access Management) i Microsoft Azure for å forstå hvordan tilgang til ressurser styres.

IAM brukes til å kontrollere hvem som har tilgang til ressurser i Azure, og hva de har lov til å gjøre.

---

### Rollebasert tilgang (RBAC)
Jeg brukte rollebasert tilgangsstyring (RBAC) på resource group-nivå for å gi tilgang til prosjektet.

**Skjermbilde: IAM oversikt i Azure (Access control - IAM)**  
![IAM oversikt](Bilder/IAM/iam-overview.png)

---

### Reader-rolle
Jeg ga en bruker tilgang med **Reader-rollen**.

Reader-rollen gir:
- Mulighet til å se ressurser
- Ingen mulighet til å endre eller slette ressurser

Dette er en sikker rolle som brukes for lesetilgang.

**Skjermbilde: Tildeling av Reader-rolle**  
![Reader rolle](Bilder/IAM/iam-reader-role.png)

---

### Hvordan jeg ga tilgang
Jeg ga tilgang via Azure-portalen:

- Gikk til Resource Group
- Åpnet “Access control (IAM)”
- La til en rolle (Reader)
- Valgte bruker ( testbruker)
- Bekreftet tilgang

**Skjermbilde: Legge til rolle i IAM**  
![Legg til rolle](Bilder/IAM/iam-add-role.png)
![Legg til rolle](Bilder/IAM/iam-add-role-2.png)
![Legg til rolle](Bilder/IAM/iam-add-role-3.png)
![Legg til rolle](Bilder/IAM/iam-add-role-4.png)

---

### Hva jeg har lært
I denne fasen har jeg lært:

- Hva IAM er i Azure
- Hvordan tilgang styres med roller
- Forskjellen mellom Reader og Contributor
- Hvordan tilgang gis på resource group-nivå
- Hvor viktig tilgangskontroll er i cloud miljøer

---

### Refleksjon
Gjennom denne fasen har jeg forstått hvordan tilgangsstyring fungerer i skyen. IAM er en viktig del av sikkerhet i cloud computing, og sikrer at brukere kun har tilgang til det de trenger.