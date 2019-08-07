# Brugerstyring

## Oprettelse, opdatering og sletning af brugere

Det første tanke med Brugerstyring var at systemet med jævne mellemrum, fx en
gang i døgnet, skulle oprette, opdatere eller slette brugere på registrerede
sites ved første at bruge “get users” til at finde ud af hvilke brugere der er
aktive på et givet site og derefter finde ud af hvilke bruge der skal
henholdsvis oprettes, opdateres og slettes.

Det er dog ikke et krav at det foregår på denne måde. Hvis Brugerstyring på
anden vis kan opdage at en bruger skal oprettes på et site, fx ved nyansættelse,
så kan system blot sende en “create user”-kommando til sitet. Tilsvarende kan
opdatering og sletning af brugere på et site håndteres når/hvis Brugerstyring
opdager at en bruger ændres i det centrale system.

## Håndtering af brugere uden `uuid`

Brugerstyring og det tilhørende api håndterer kun brugere der har et `uuid`,
altså et unikt id som styres af den centrale database.

Dette giver potentielt en udfordring på sites hvor brugere kan logge via ADFS og
dermed oprette en ny bruger (uden `uuid`) på et site.

Brugerstyring stiller ingen krav til hvad der faktisk sker ved oprettelse,
opdatering eller sletning af brugere via api'et og detaljerne er helt op til
implementeringen.

En snedig implementering vil ved `create` kunne tjekke om der allerede findes en
bruger på sitet som matcher den (fra Brugerstyrings synspunkt set) nye bruger, og
så knytte `uuid`'et til den allerede eksisterende bruger. Dette kræver
naturligvis at der findes et andet unikt id som man kan bruge til at
identificere en bruger, og `email-address` (eller `az-ident`) er oplagte
kandidater.

## Indledende knæbøjninger

Når Brugerstyring aktiveres på et site bør alle eksisterende brugere (som skal
styres af Brugerstyring) tilknyttes deres respektive `uuid`, fx ud fra
e-mailadresse eller az-ident. Dette håndteres mere eller mindre manuelt, dvs. vi
laver ikke automatik/funktionalitet til at håndtere denne engangsforeteelse.
