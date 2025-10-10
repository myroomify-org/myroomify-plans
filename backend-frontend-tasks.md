# Backend – Adatbázis és API végpontok

## Fejlesztési feladatok
- **Adatbázis-tervezés:** 
  - Szobák, foglalások, felhasználók, értékelések, szobaképek tábláinak létrehozása, 
  - státuszok kezelése 
      - szobák: available, inactive, booked, maintenance; 
      - pénzügy: unpaid, paid; 
      - foglalások típusa: online, telefonos, helyszíni; 
      - foglalási státuszok: pending, confirmed, cancelled, no-show, completed.
- **Üzleti logika:** 
  - Foglalások kezelése, dátumütközések vizsgálata, automatikus no-show állapot beállítása, foglalás lemondása.
- **Felhasználókezelés:** 
  - Regisztráció, bejelentkezés, jelszó visszaállítása, jogosultságok kezelése (vendég, admin, recepciós szerepkörök).
- **E-mail küldés:** 
  - Regisztráció, jelszó visszaállítása, foglalás visszaigazolása, lemondás, no-show értesítések.
- **Hibakezelés:** 
  - Validációs és üzleti hibák visszaküldése frontendnek.
- **Tesztelés:** 
  - API végpontok Insomnia/Postman eszközökkel történő tesztelése.
- **Dokumentáció:** 
  - API végpontok és rendszer működésének részletes leírása.

## API végpontok

| Végpont | HTTP metódus | Leírás |
|--------|---------------|--------|
| `/api/rooms` | GET | Szobák listázása |
| `/api/rooms` | POST | Új szoba létrehozása |
| `/api/rooms/{id}` | PUT / PATCH | Szoba módosítása |
| `/api/rooms/{id}` | DELETE | Szoba törlése |
| `/api/rooms/{id}/status` | PATCH | Szoba állapotának módosítása (`available`, `inactive`) |
| `/api/rooms/{id}/images` | POST | Szobához képek feltöltése |
&nbsp;
| `/api/bookings` | GET | Foglalások listázása |
| `/api/bookings` | POST | Foglalás létrehozása |
| `/api/bookings/{id}` | PUT / PATCH | Foglalás adatainak módosítása |
| `/api/bookings/{id}/status` | PATCH | Foglalás státuszának módosítása (`pending`, `confirmed`, `cancelled`, `no_show`) |
| `/api/bookings/{id}/payment-status` | PATCH | Fizetési státusz módosítása (`unpaid`, `paid`, `refunded`) |
| `/api/bookings/user/{user_id}` | GET | Egy felhasználó foglalásainak lekérése |
&nbsp;
| `/api/register` | POST | Felhasználó regisztráció |
| `/api/login` | POST | Bejelentkezés (token visszaadás) |
| `/api/logout` | POST | Kilépés (token visszavonása) |
| `/api/profile` | GET | Bejelentkezett felhasználó profiladatai |
| `/api/password/forgot` | POST | Jelszó-visszaállítási e-mail küldése |
| `/api/password/reset` | POST | Jelszó visszaállítása token alapján |
&nbsp;
| `/api/users` | GET | Felhasználók listázása (admin jogosultsággal) |
| `/api/users/{id}` | DELETE | Felhasználó törlése (saját vagy admin jogosultsággal)|
| `/api/users/{id}/role` | PATCH | Szerepkör módosítása (`admin`, `recepciós`, `vendég`) |
&nbsp;
| `/api/reviews` | GET | Összes értékelés lekérése |
| `/api/reviews` | POST | Új értékelés beküldése |
| `/api/reviews/room/{room_id}` | GET | Adott szoba értékelései |
| `/api/reviews/user/{user_id}` | GET | Egy felhasználó értékelései |
| `/api/reviews/{id}` | DELETE | Értékelés törlése (saját vagy admin jogosultsággal) |

## Extra javasolt végpontok

| Végpont | HTTP metódus | Leírás |
|--------|---------------|--------|
| `/api/statistics` | GET | Admin/recepciós statisztikák (foglalások, bevétel, kihasználtság) |
| `/api/calendar-view` | GET | Naptárnézet (foglalások szobánként napi bontásban) |

---

## Technológiák
- Laravel PHP keretrendszer v12
- MySQL adatbázis
- REST API kialakítás
- E-mail küldés SMTP-n keresztül
- API tesztelés Insomnia/Postman eszközökkel

---

# Frontend1 – Admin és recepciós felület

## Fejlesztési feladatok

### Super Admin feladatok
- Szobák CRUD műveletek (hozzáadás, módosítás, törlés).
- Fényképek feltöltése.
- Super Admin regisztráció és bejelentkezés.
- Admin (recepciós) felhasználók létrehozása és kezelése.

### Recepciós feladatok
- Foglalások listázása.
- Vendégek státuszának kezelése (pending, confirmed, cancelled, automatikus no-show ellenőrzése).
- Telefonos foglalások rögzítése.
- Statisztikák megtekintése.
- Naptárnézet szobafoglalásokkal.

## API végpontok

| Végpont | HTTP metódus | Leírás |
|---------|--------------|--------|
| `/api/rooms` és `/api/rooms/{id}` | GET, POST, PUT/PATCH, DELETE | Szobák CRUD műveletek |
| `/api/rooms/{id}/photos` | POST | Fényképek feltöltése |
| `/api/admin/register` | POST | Super Admin regisztráció |
| `/api/admin/login` | POST | Super Admin bejelentkezés |
| `/api/admin/users` | GET, POST | Admin/recepciós felhasználók kezelése |
| `/api/bookings` | GET | Foglalások listázása |
| `/api/bookings/{id}/status` | PATCH | Foglalás státuszának frissítése |
| `/api/bookings/phone` | POST | Telefonos foglalás rögzítése |
| `/api/statistics` | GET | Statisztikák lekérése |
| `/api/calendar/bookings` | GET | Naptárnézet adatainak lekérése |

## Technológiák
- HTML, CSS, JavaScript
- Angular v18 frontend keretrendszer
- API hívások biztonságos kezelése token alapú autentikációval
- Felhasználói jogosultság kezelés
- Dokumentáció készítés és tesztelés


# Frontend2 – Publikus vendégoldal

## Fejlesztési feladatok
- Navigációs sáv és menüpontok kezelése.
- Kezdőoldal: szálláshely bemutatása, elérhetőségek megjelenítése.
- Szobák listázása és részletes megtekintése (képek, felszereltség, ágyak száma).
- Foglalási űrlap a backend foglalás kezelő API-jával való kapcsolattal.
- Szálláshely értékelése kijelentkezéskor (1-5 csillag + vélemény).
- Névjegy, kapcsolat, lábléc (ÁSZF, impresszum, fejlesztők elérhetőségei).

## API végpontok

| Végpont | HTTP metódus | Leírás |
|---------|--------------|--------|
| `/api/rooms` | GET | Szobák listázása |
| `/api/rooms/{id}` | GET | Egy szoba részletes adatainak lekérése |
| `/api/bookings` | POST | Foglalás beküldése |
| `/api/reviews` | POST | Értékelés beküldése |

## Technológiák
- HTML, CSS, JavaScript
- Angular v18
- API hívások HTTP klienssel
- Reszponzív kialakítás
- UI tervek, színek, képek, arculat
- Dokumentáció készítése és tesztelés