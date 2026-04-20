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
