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

![LandingHomaPage](https://github.com/oli-tolnai/olab1/blob/main/kepek/1.%20Landing%20%20Home.jpeg)

**2. Regisztráció / Bejelentkezés**

**3. Dashboard (főmenü)**

![Dashboard (főmenü)](https://github.com/oli-tolnai/olab1/blob/main/kepek/3.%20Dashboard%20(f%C5%91men%C3%BC).jpeg)


![Dashboard (főmenü)](https://github.com/oli-tolnai/olab1/blob/main/kepek/alternativa.png)

**4. Gyakorlás beállítása**

![Gyakorlás beállítása](https://github.com/oli-tolnai/olab1/blob/main/kepek/4.%20Gyakorl%C3%A1s%20be%C3%A1ll%C3%ADt%C3%A1sa.jpeg)

**5. Kvíz nézet**

![Kvíz nézet](https://github.com/oli-tolnai/olab1/blob/main/kepek/5.%20Kv%C3%ADz%20n%C3%A9zet.jpeg)

**6. Eredmény oldal**

![Eredmény oldal](https://github.com/oli-tolnai/olab1/blob/main/kepek/6.%20Eredm%C3%A9ny.jpeg)

**7. Profil oldal**

**8. Admin kérdéskezelés**
