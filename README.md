# Motor de Sancionadors — DGPAMN

Tramitació dels expedients sancionadors de la Direcció General de Polítiques Ambientals i Medi Natural. Fa servir el mateix disseny i el mateix sistema de carpeta de treball que el Motor Patrimoni i el Motor de Contractació.

## Mòduls

- **Inici**: resum de cada mòdul, tasques pendents del perfil i avisos de terminis.
- **Tramitació**: entrada de la denúncia → validació inicial (jurídic) → informe tècnic (tècnic) → incoació i instrucció (jurídic) → resolució (jurídic).
- **Recursos**: recursos contra expedients incoats o resolts, amb els seus informes tècnics i la seva resolució.
- **Dades**: filtres per territori, temàtica, data, gravetat, denunciant, espècie, recursos i reincidència. No mostra dades personals.

## Perfils

| Perfil | Què fa |
|---|---|
| Jurídic/a | Entra i valida les denúncies, demana informes, incoa, instrueix, resol i tramita els recursos |
| Tècnic/a | Redacta i lliura els informes tècnics |
| Consulta | Només consulta |

Fins a la integració a SINATCAT, cada persona indica el seu nom i el seu perfil en entrar. És un control d'organització, no de seguretat.

## Lectura dels PDF del CAR

En una denúncia nova es poden arrossegar alhora l'acta de denúncia (model D01) i l'informe complementari, en PDF:

- **Acta**: el programa en llegeix els camps del formulari.
- **Informe complementari**: el programa en llegeix el text (núm. de servei, data, lloc, persona, descripció dels fets i conclusions). Només omple els camps que l'acta ha deixat buits i desa la descripció i les conclusions en un apartat propi.
- Avisa si l'acta i l'informe no coincideixen (número d'acta, DNI, data o coordenades a més de 500 m) i si l'acta ja és en un altre expedient.
- Detecta l'espai natural protegit pel nom (parcs i consorcis de les unitats del Motor de Contractació).
- Els camps llegits es marquen en verd i el jurídic els pot modificar. Amb una carpeta de treball connectada, els dos PDF es desen a `actes/` i `informes_car/`.

Si l'acta és escanejada (sense camps de formulari), les dades s'entren a mà.

## Si el repositori no té dades

El programa busca les dades a la carpeta de treball, després a la carpeta `data/` del costat del programa i després al GitHub. Si no les troba, fa servir una còpia de `catalegs.json` i `variables.json` que porta incrustada, perquè no es quedi sense comarques, matèries ni estats. El peu de pàgina indica d'on s'han llegit.

## Exemples ficticis (`exemples/`)

Cinc sancionadors inventats, cadascun amb l'acta D01 (amb camps de formulari) i l'informe complementari, marcats com a «DOCUMENT FICTICI · NOMÉS PER A PROVES»:

| Acta | Lloc | Fets | Persona |
|---|---|---|---|
| 901-26 | Santa Pau · PN Zona Volcànica de la Garrotxa | Quad fora de pista a la Fageda d'en Jordà | Pere Exemple Ficticí |
| 902-26 | Bagà · PN Cadí-Moixeró | Arrencada de 7 sabatetes de la Mare de Déu | Laia Prova Inventada |
| 903-26 | Deltebre · PN Delta de l'Ebre | Abocament de runes en zona humida | Construccions Ficticies del Delta, SL |
| 904-26 | Ulldemolins · PN Montsant | Captura de caderneres amb vesc | Joan Simulat Riera |
| 905-26 | El Port de la Selva · PN Cap de Creus | Acampada i foc en època de risc | Pere Exemple Ficticí (reincidència) |

## Dades (`data/`)

| Fitxer | Contingut |
|---|---|
| `expedients.json` | Un registre per expedient amb totes les fases: `validacio`, `informes[]`, `instruccio`, `resolucio` i `recursos[]` (cada recurs amb els seus `informes[]`) |
| `persones.json` | Persones denunciades, separades per detectar la reincidència i concentrar les dades personals |
| `catalegs.json` | Llistes dels desplegables: matèries del CAR, temàtiques, qualificacions, tipus de recurs, comarques → àmbit territorial, `tipificacions` (pendent) |
| `variables.json` | Perfils, estats, transicions per perfil i terminis dels avisos |
| `historial_canvis.json` | Registre de cada canvi (persona, perfil, data, acció) |
| `metadata.json` | Versió i sistema de coordenades (ETRS89 / UTM 31N) |

Les unitats (espais naturals i serveis territorials) es llegeixen directament de `marcvila1/Motor-Contractacio-DGPA/unitats_promotores.json`.

## Pendents de validar

- Taula de tipificacions (`catalegs.json › tipificacions`).
- Terminis dels avisos (`variables.json › terminis`): termini de l'informe tècnic i de caducitat del procediment.
- Correspondència comarca → àmbit territorial (`catalegs.json › comarques`).

> Les dades d'aquest repositori són de prova. L'expedient `SAN-2024-0001` reprodueix els fets d'una acta real del CAR amb les dades personals substituïdes per dades fictícies.
