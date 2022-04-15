# OAuth - Samenvatting van de OAuth-NL standaard

> link naar de standaard: https://publicatie.centrumvoorstandaarden.nl/api/oauth/v1.0
> Versie 1.0 vastgesteld op 09 juli 2020

## Inleiding

Deze standaard is voor het ontsluiten van services van publieke/overheids organisaties. De services ontsluiten data via een zogenaamde Resource Server (verder aangeduid als de API). De resource server ofwel de API is afhankelijk van een Authorization Server. Deze Authorization Server voorziet in de identificatie en autorisatie van de user die de API bevraagd. De user gebruikt een Client die hij dient te vertrouwen om namens hem de vraag naar de API te sturen en de response op de vraag te ontvangen en presenteren.

### Schematische weergave van de flow van de standaard

![OAuth-Abstract_Authorization_Code_Flow](./OAuth-Abstract_Authorization_Code_Flow.svg)



## Vereisten

De standaard biedt simpel gezegd access control voor RESTful API's. Dergelijke API's worden momenteel door de overheid ontwikkeld conform de API Design Rules (ADR) en beschreven conform de Open API Specification (OAS). 

Deze standaard beschrijft vereisten voor de API (Resource Server), Authorization Server en de Client. Hieronder is een samenvatting van de vereisten toegelicht:

### 1. Introductie

- Iedere Authorization Server moet voldoen aan alle vereisten uit de standaard (paragraaf 1.3)
- Iedere Client moet alle functies uit de standaard gebruiken (paragraaf 1.3)
- Iedere API moet alle functies uit de standaard gebruiken (paragraaf 1.3)

### 2. Client profiel

- Clients zijn Full clients, ofwel web applicaties die centraal draaien of Native clients, instanties van software die draaien op het device van de user, de zogenaamde apps. Beide client types hebben verschillende vereisten (paragraaf 2.1)
- Clients moeten vooraf zijn geregistreerd bij de Authorization Server (paragraaf 2.2)
- Clients mogen geen gebruik maken van een redirect naar de localhost en mogen ook geen waardes doorsturen naar andere URI's (paragraaf 2.2.1)
- Clients moeten een willekeurige status parameter genereren en koppelen aan de client sessie om deze vervolgens mee te sturen naar de Authorization server en te verifiëren of deze ook correct in de response wordt meegegeven (paragraaf 2.3)
- Clients moeten de volledige redirect URI meesturen in het verzoek aan de Authorization server (paragraaf 2.3)
- De Authorization Server moet de redirect URI controleren ten opzichte van de URI die vooraf is geregistreerd door de Client (paragraaf 2.3)
- Native Clients moeten PCKE toepassen (paragraaf 2.3)
- Wanneer de API, Client en Authorisation Server niet onder verantwoordelijkheid vallen van één organisatie moeten PIKOverheid certificaten worden gebruikt (met OIN) (paragraaf 2.3.4)
- Clients moeten autorisatie requests over TLS sturen en moeten het certificaat van de API verifiëren (paragraaf 2.4)

### 3. Authorization Server profiel

- De Authorization Server moet alle communicatie versleutelen met TLS en voldoen aan alle security eisen (paragraaf 3)
- De Authorization Server moet dynamic client registration toestaan. De autorisatie server mag de Scopes beperken van dynamisch geregistreerde clients (paragraaf 3.1.3)
- De Authorization Server moet de user laten weten welke Client is geregistreerd en welke access die Client vraagt (paragraaf 3.1.4)
- De Authorization Server moet OpenID.Discovery aanbieden (paragraaf 3.1.5)
- De Authorization Server moet op verzoek van de Client tokens intrekken (paragraaf 3.1.4)
- De Authorization Server moet JWT tokens verstrekken die de API kan verifiëren (paragraaf 3.2.1)
- De Authorization Server moet authenticatie vereisen voor de revocation en introspection endpoints (paragraaf 3.2)
- Alle uitgegeven tokens mogen worden ingetrokken (paragraaf 3.2)
- Access tokens hebben verschillende lifetimes (paragraaf 3.4)
- De Authorization Server zou Scopes moeten definieren en documenteren (paragraaf 3.5)

### 4. Protected Resource (API) profiel

- De API geeft de Client toegang wanneer deze een geldig access token en de correcte Scope heeft. De API vertrouwt erop dat de Authorization Server de security en access control waarborgt (paragraaf 4.1)
- De API (met vertrouwelijke data) die een hoger vertrouwensniveau vereist van de eindgebruiker moet de data alleen beschikbaar stellen binnen een unieke Scope (paragraaf 4.1)
- De Client die vertrouwelijke data wil opvragen bij de API moet een hoger vertrouwensniveau Scope meegeven in het verzoek aan de Authorization Server (paragraaf 4.1)
- De Authorization Server moet de authenticatie van de eindgebruiker op het juiste vertrouwensniveau vaststellen (paragraaf 4.1)
- Een API moet Bearer tokens accepteren in de authorization header en mag deze ook accepteren als form parameter (paragraaf 4.2)
- Een API mag geen access tokens accepteren als query parameter (paragraaf 4.2)
- Een API moet documenteren welke scopes vereist zijn voor toegang tot vertrouwelijke data (paragraaf 4.2)
- Een API moet een access token verifiëren (paragraaf 4.3)
- Een API moet limiteren welke Authorization Servers het vertrouwt (paragraaf 4.3)

### 6. Security overwegingen

- Alle transacties moeten worden versleuteld met TLS en het is aanbevolen om hierbij de richtlijken van het NCSC op te volgen (paragraaf 6)

## !! Disclaimer

Deze samenvatting is een interpretatie van de standaard en is niet volledig in de opsomming of beschrijving van alle vereisten. Wanneer de standaard moet worden geimplementeerd dient altijd de officiële en actuele  standaard te worden gebruikt zoals gepubliceerd door het Forum Standaardisatie op: https://forumstandaardisatie.nl/open-standaarden/nl-gov-assurance-profile-oauth-20.



