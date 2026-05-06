### Workflow vagy Automatizmus (MBH szemmel)
#### Frontend‑es ORIGINATION‑ben: mindkettő van, de NEM ugyanarra valók.<br>
#### Workflow az originationben, automatizmus az ESB/core oldalon.<br>
👉 Workflow = üzleti folyamat, állapotokkal és emberi döntési pontokkal<br>
Jellemzői:
 - lépései vannak (state machine)
 - lehet benne:
     - user input
     - jóváhagyás
     - várakozás
     - visszalépés
 - nem determinisztikus
 - UX‑hez kötődik

ORIGINATION-ben tipikusan:
 - igény rögzítve
 - dokumentumhiány
 - scoring lefut
 - elutasítva / feltételesen elfogadva
 - manageri override
 - ügyfél visszalép
 - ajánlat elfogadás<br>
👉 Ez klasszikus workflow, nem automatizmus.<br>

#### Automatizmus = determinisztikus, szabályvezérelt, ember nélküli lépés
Jellemzői:
 - trigger → fix eredmény
 - nincs „állapota”, csak lefut
 - nem kérdez vissza
 - technikai szemléletű

Tipikusan:
 - napzárás elindul
 - scoring engine lefut
 - adatok átmennek ESB-n
 - könyvelés megtörténik<br>
👉 Ez nem workflow, hanem automatizmus.

#### ✅ ORIGINATION-ben Workflow kell
Mert az origination:
 - ügyfél‑vezérelt
 - nem lineáris
 - visszaléphető
 - emberi döntéseket tartalmaz

Példa (frontend):
```
Igény beadva
   ↓
Előszűrés
   ↓
(score OK?)
   ├─ NEM → elutasítás
   └─ IGEN
        ↓
Dokumentum feltöltés
        ↓
Manageri jóváhagyás
        ↓
Ajánlat elfogadva
```

#### ✅ ESB / Core oldalon jön az automatizmus
Amikor:
 - az origination lezárult
 - megszületett a döntés
 - nincs több üzleti vita

Példa (automatizmus):
```
Esemény: "Ügylet elfogadva"
→ ESB meghívja a core szolgáltatást
→ számla létrejön
→ limit rögzül
→ GL könyvel
→ visszajelzés
```

#### 👉 MBH‑s „aranyszabály”
```
Ahol ember gondolkodik: workflow
Ahol rendszer végrehajt: automatizmus

Az MBH frontend‑es origination folyamata workflow‑vezérelt, míg az ESB‑n és a core rendszereken túl már kizárólag automatizmus fut
(ez biztosítja az üzleti rugalmasságot és a prudenciális kontrollt egyszerre).
```

#### ✅ Rövid döntési táblázat
```
Ha ez a helyzet…             → Akkor
Emberi döntések vannak       → Workflow engine
Ügyfél lép be                → Workflow
Állapotok hetekig élnek      → Workflow
„Ha–akkor–különben” emberrel → Workflow
Determinisztikus végrehajtás → Automatizmus
```

#### 👉 Workflow vs. Automatizmus (MBH‑s határ) példa:
```
                ┌──────────────────────────┐
                │        FRONTEND UI        │
                │  (Netbank, Fiók, Portál)  │
                └─────────────┬────────────┘
                              │
                              ▼
────────────────────────────────────────────────
        WORKFLOW ZÓNA – ORIGINATION
        (üzleti folyamat, emberi lépések)
────────────────────────────────────────────────
                              │
    ┌───────────────┐   ┌───────────────┐
    │  Igény beadva │→→ │ Előszűrés     │
    └───────────────┘   └───────────────┘
             │                  │
             ▼                  ▼
    ┌───────────────┐   ┌───────────────┐
    │ Dokumentum    │   │ Scoring OK?   │
    │ bekérés       │   ├─────┬─────────┤
    └───────────────┘   │ IGEN │  NEM    │
             │          ▼      ▼
             │     Ajánlat   Elutasítás
             ▼
     Manageri jóváhagyás
             │
             ▼
       Ügyfél elfogadta
             │
             ▼
─────────────│──────────────────────────────────
             │   HATÁR – NINCS TÖBB EMBER
─────────────│──────────────────────────────────
             ▼
────────────────────────────────────────────────
        AUTOMATIZMUS ZÓNA – ESB / CORE
        (determinista, auditált végrehajtás)
────────────────────────────────────────────────
             │
             ▼
     ESB esemény: "Deal Accepted"
             │
             ▼
   Core banking számlanyitás
             │
             ▼
      Limit beállítás
             │
             ▼
        GL könyvelés
             │
             ▼
       Visszajelzés OK
```
#### 🧠 Ábra üzenete
 - Workflow fent: rugalmas, emberi, nem lineáris
 - Automatizmus lent: szigorú, reprodukálható
 - ESB = határőr, nem üzleti folyamatgazda

vagy

```mermaid
flowchart TB
    %% Frontend
    UI["Frontend UI<br/>(Netbank / Fiók / Portál)"]
    subgraph WF["WORKFLOW ZÓNA – ORIGINATION"]
        W1[Igény beadva]
        W2[Előszűrés]
        W3{Scoring OK?}
        W4[Dokumentum bekérés]
        W5[Manageri jóváhagyás]
        W6[Ügyfél elfogadás]
    end

    %% Boundary
    BND["[HATÁR<br/>Nincs több emberi döntés]"]
    subgraph AUTO["AUTOMATIZMUS ZÓNA – ESB / CORE"]
        A1[ESB esemény feldolgozás]
        A2[Core számlanyitás]
        A3[Limit rögzítés]
        A4[GL könyvelés]
        A5[Visszajelzés OK]
    end

    %% Flow
    UI --> W1 --> W2 --> W3
    W3 -- Igen --> W4 --> W5 --> W6 --> BND
    W3 -- Nem --> End1((Elutasítva))

    BND --> A1 --> A2 --> A3 --> A4 --> A5
```

#### 🧠 Értelmezés:
##### ✅ Workflow zóna
 - BPMN / workflow engine
 - emberi döntések
 - visszalépés, várakozás
 - UX‑vezérelt
##### ✅ Automatizmus zóna
 - ESB
 - determinisztikus
 - prudenciális
 - auditálható
 - nincs hosszú életű állapot

Röviden:
 - Az origination frontend oldalon workflow‑val kezelendő, mert ott emberi döntések és állapotok vannak →
 - amint az ügylet elfogadott, az ESB‑n túl már csak automatizmus futhat.

### Frontend ORIGINATION (BPMN) jellegű workflow (Mermaid-ban)
```mermaid
flowchart TD
    %% Start
    Start((Start))

    %% User & Service tasks
    A[User Task: Igény rögzítése]
    B[Service Task: Előszűrés futtatása]
    C{Előszűrés OK?}

    D[Service Task: Scoring futtatása]
    E{Scoring OK?}

    F[User Task: Dokumentum bekérés]
    G[User Task: Manageri jóváhagyás]
    H{Jóváhagyva?}

    I[User Task: Ajánlat elfogadása]
    J{Ügyfél elfogadta?}

    K[Service Task: Esemény küldése ESB felé]

    EndOK((Origination lezárva))
    EndReject((Elutasítva))
    EndWithdraw((Ügyfél visszalépett))

    %% Flow
    Start --> A --> B --> C
    C -- Nem --> EndReject
    C -- Igen --> D --> E
    E -- Nem --> EndReject
    E -- Igen --> F --> G --> H
    H -- Nem --> EndReject
    H -- Igen --> I --> J
    J -- Nem --> EndWithdraw
    J -- Igen --> K --> EndOK
```
#### 🧠 Ábra magyarázata:
 - User Task ↔ emberi lépés
 - Service Task ↔ automatizmus
 - Exclusive Gateway ↔ döntési pont
 - ESB esemény küldése = workflow vége
