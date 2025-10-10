# MyRoomify – Projektterv

## Szobafoglaló rendszer kis vendégházak számára

## 1. A projekt célja

A **MyRoomify** egy modern, reszponzív szobafoglaló rendszer, amely kis létszámú, nem lánchoz tartozó vendégházak, fogadók és hostel típusú szálláshelyek számára készült. A cél egy olyan digitális platform létrehozása, amely lehetővé teszi:

- A szálláshely online bemutatását
- A szobák böngészését és kényelmes foglalását
- A vendégek értékeléseinek megjelenítését
- Az adminisztrációs háttér biztosítását a tulajdonos számára

A rendszer alkalmas **online, telefonos és helyszíni** foglalások kezelésére is. A cél, hogy a vendéglátók **függetlenek maradjanak a külső foglalási rendszerektől** (pl. Booking.com), és saját weboldalukon keresztül kezelhessék foglalásaikat.

---

## 2. A rendszer célcsoportja

- Kis létszámú vendégházak (kb. 5–15 szoba)
- Diákszállók, hostelek, falusi turizmus egységek
- Olyan tulajdonosok, akik nem kívánnak nagy online platformhoz csatlakozni, de igénylik az egyszerű, saját foglalási lehetőséget

---

## 3. Főbb funkciók

### Nyilvános oldal (frontend)
- Szobák listázása, képgalériával
- Foglalási űrlap (érkezés, távozás, vendég adatok)
- Vélemények megtekintése és beküldése
- „Rólunk” szekció étterem-információval
- Kapcsolatfelvételi lehetőség (telefonszám, űrlap)
- Reszponzív megjelenés mobil eszközökön

### Admin felület
- Foglalások kezelése: listázás, manuális rögzítés (telefonos / helyszíni), lemondás, no-show státusz
- Szobák kezelése: hozzáadás, szerkesztés, képgaléria
- Vélemények moderálása
- Bejelentkezés Laravel Sanctum-alapú tokenes hitelesítéssel

---

## 4. Technológiai háttér

| Technológia | Verzió | Szerep |
|-------------|--------|--------|
| **Angular** | 18 | Frontend, SPA |
| **Laravel** | 12 | Backend, REST API |
| **MySQL**   | 8+ | Adatbázis |
| **Bootstrap** | 5 | Frontend stílus és reszponzivitás |
| **Laravel Sanctum** | – | API hitelesítés |
| **Email küldés** | Laravel Mail | Foglalás visszaigazolás |

---

## 5. Adatmodell főbb táblái

- `users`: admin felhasználók
- `rooms`: szobák adatai
- `bookings`: foglalások, forrás (online, telefon, helyszíni), státusz
- `reviews`: vendégvélemények
- `images`: képek a szobákhoz

---

## 6. Foglalási folyamat támogatása

- **Online**: vendég kitölti az űrlapot → email értesítés → admin visszaigazolja
- **Telefonos / helyszíni**: admin rögzíti manuálisan a foglalást az adminfelületen
- **Lemondás**: admin vagy vendég jelezheti → státusz `cancelled`
- **No-show**: admin állíthatja be, ha a vendég nem jelent meg

---

## 7. Kiegészítő lehetőségek

- Étkezés nem választható online, de a vendégház rendelkezik saját étteremmel
- Galéria funkció minden szobához
- Vélemények csak jóváhagyás után jelennek meg

---

## 8. Tervezett fejlesztési szakaszok

| Fázis | Leírás |
|-------|--------|
| 1. | Alapvető adatmodell és backend API |
| 2. | Frontend komponensek, foglalási űrlap |
| 3. | Adminfelület létrehozása |
| 4. | Vélemények, képgaléria |
| 5. | E-mail küldés és befejező funkciók |
| 6. | Tesztelés, dokumentáció, README írása |

-----------------------------------------------------------
