### Epic: User Management
| Story          | API                   | Frontend feladat                 |
|----------------|-----------------------|----------------------------------|
| Registration   | POST /register        | Regisztrációs form, hibaüzenetek |
| Login          | POST /login           | Bejelentkezés, token mentés      |
| Logout         | POST /logout          | Token törlés, átirányítás        |
| Profile update | PUT /profile          | Profil szerkesztő form           |
| Password reset | PUT /profile/password | Jelszó módosító form             |

---
### Epic: Practice Mode
| Story                    | API                                   | Frontend feladat               |
|--------------------------|---------------------------------------|--------------------------------|
| Solve a question         | GET /questions                        | Kérdés megjelenítése           |
| Answer feedback          | POST /questions/answer                | Válasz beküldése, visszajelzés |
| Solve a set of questions | GET /questions, POST /results/session | Gyakorló kör kezelése          |

---
### Epic: Scoring and Level System
| Story                    | API                                           | Frontend feladat       |
|--------------------------|-----------------------------------------------|------------------------|
| Earn points              | POST /questions/answer, POST /results/session | Pontszám megjelenítése |
| Level display            | GET /users/me/progress                        | Szint, XP, streak UI   |

---
### Epic: Leaderboard
| Story                    | API                                   | Frontend feladat         |
|--------------------------|---------------------------------------|--------------------------|
| Top leaderboard display  | GET /leaderboard                      | Ranglista UI             |
| User leaderboard display | GET /leaderboard                      | Saját helyezés kiemelése |

---
### Epic: Administration
| Story             | API                    | Frontend feladat          |
|-------------------|------------------------|---------------------------|
| Add a question    | POST /questions        | Admin form új kérdéshez   |
| Edit a question   | PUT /questions/{id}    | Kérdés szerkesztő felület |
| Delete a question | DELETE /questions/{id} | Törlés gomb, megerősítés  |

---
### Extra API-k, amik még hasznosak lehetnek
| Story                          | API                         | Frontend feladat                              |
|--------------------------------|-----------------------------|-----------------------------------------------|
| View question details          | GET /questions/{id}         | Admin kérdés szerkesztő felület betöltése     |
| View question types            | GET /questions/types        | Admin UI: kérdéstípus választó (pl. dropdown) |
| View supported languages       | GET /languages              | Gyakorlás beállításánál nyelvválasztó         |



### Oldalak
**1. Landing / Home**

**2. Regisztráció / Bejelentkezés**

**3. Dashboard (főmenü)**

**4. Gyakorlás beállítása**

**5. Kvíz nézet**

**6. Eredmény oldal**

**7. Profil oldal**

**8. Admin kérdéskezelés**
