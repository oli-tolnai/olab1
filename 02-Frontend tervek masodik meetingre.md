```
1. Landing / Home
 ----------------------------------------------------
 |  LOGO (CodeLingo)                                |
 |--------------------------------------------------|
 |   [Bemutató szöveg röviden]                      |
 |                                                  |
 |   🎯 "Tanulj kódolni játékosan!"                 |
 |                                                  |
 |   [Regisztráció]   [Bejelentkezés]               |
 ----------------------------------------------------


2. Regisztráció / Bejelentkezés
  ----------------------------------------------------
 |  LOGO                                            |
 |--------------------------------------------------|
 |   Bejelentkezés / Regisztráció                   |
 |                                                  |
 |   Email: [___________]                           |
 |   Jelszó: [___________]                          |
 |                                                  |
 |   [Belépés]   vagy   [Google login]              |
 ----------------------------------------------------


3. Dashboard (főmenü)

 ----------------------------------------------------
 | LOGO   | Profil ikon | Menü (Ranglista, Profil)  |
 |--------------------------------------------------|
 |   Szint: 5   XP: 3200   🔥 Streak: 7 nap         |
 |                                                  |
 |   [Kezdj gyakorlást]                             |
 |                                                  |
 |   Ranglista kivonat:                             |
 |   1. UserA  5200 XP                              |
 |   2. UserB  4300 XP                              |
 |   3. TE     3200 XP                              |
 ----------------------------------------------------

4. Gyakorlás beállítása
 ----------------------------------------------------
 | Vissza | LOGO                                    |
 |--------------------------------------------------|
 |   ⚙️ Gyakorlás beállítása                         |
 |                                                  |
 |   Kérdések száma:   ( 5 ) ( 10 ) ( 20 )          |
 |                                                  |
 |   Nehézség:   ( Könnyű ) ( Közepes ) ( Nehéz )   |
 |                                                  |
 |   Programnyelv:  [ ] Python  [ ] C#  [ ] JS      |
 |                                                  |
 |   [Indítás]                                      |
 ----------------------------------------------------


5. Kvíz nézet
 ----------------------------------------------------
 | LOGO         | Kérdés 2/10                       |
 |--------------------------------------------------|
 |   "Mi lesz a kód kimenete?"                      |
 |                                                  |
 |   print(2 + 2)                                   |
 |                                                  |
 |   [ ] 3                                          |
 |   [ ] 4   ✅ helyes                              |
 |   [ ] 5                                          |
 |                                                  |
 |   [Következő ➡️]                                 |
 ----------------------------------------------------


6. Eredmény oldal
 ----------------------------------------------------
 | LOGO                                             |
 |--------------------------------------------------|
 |   ✅ Gratulálunk!                                |
 |   Helyes válaszok: 8/10                          |
 |   Új XP: +80 (Összesen: 3280)                    |
 |                                                  |
 |   🔥 Streak folytatódik (8 nap)                  |
 |                                                  |
 |   [Új gyakorlás]   [Vissza a főmenübe]           |
 ----------------------------------------------------

7. Profil oldal
 ----------------------------------------------------
 | LOGO                                             |
 |--------------------------------------------------|
 |   Felhasználónév: UserX                          |
 |   Szint: 5                                       |
 |   Össz XP: 3280                                  |
 |   Napi Streak: 8 nap                             |
 |                                                  |
 |   Statisztika:                                   |
 |   - Legtöbb helyes válasz: Python                |
 |   - Átlagos pontszám: 85%                        |
 |                                                  |
 |   [Profil szerkesztése]                          |
 ----------------------------------------------------

8. Admin kérdéskezelés
 ----------------------------------------------------
 | LOGO      | Menü: Kérdések | Import | Export     |
 |--------------------------------------------------|
 |   Kérdéslista:                                   |
 |   1. print(2+2) -> válasz: 4 (Python, Könnyű)    |
 |   2. for i in ... (JS, Közepes)                  |
 |                                                  |
 |   [Új kérdés]   [Szerkesztés]   [Törlés]         |
 ----------------------------------------------------
```

## Api hívások:
Felhasználókezelés:
   - POST /register – regisztráció
   - POST /login – bejelentkezés
   - POST /logout – kijelentkezés
   - GET /profile – profiladatok lekérése
   - PUT /profile – profil szerkesztése
   - PUT /profile/password – jelszó módosítása


Kvíz / kérdések
   - GET /questions?lang=python&difficulty=easy&count=10 – kérdések lekérése
   - GET POST /questions/answer – válasz beküldése, eredmény visszaadása
   - GET GET /results/session/{id} – adott gyakorló kör eredménye
   - GET POST /results/session – gyakorlás végén eredmény mentése


Pontszám / szint / ranglista
   - GET /leaderboard – ranglista adatok
   - GET /users/me/progress – XP, szint, streak


Admin funkciók
   - POST /questions – új kérdés
   - PUT /questions/{id} – kérdés módosítása
   - DELETE /questions/{id} – törlés
   - POST /questions/import – CSV/Aiken feltöltés
   - GET /questions/export – export   


5. Extra UX ötletek
   - Progress bar a gyakorló felületen (hányadik kérdésnél tart a felhasználó)
   - Animációk helyes válasznál (pl. ugráló pontszám, konfetti)
   - Motivációs üzenetek (pl. “Szép munka!”, “Csak így tovább!”)
   - Badge-ek, achievementek (pl. 10 helyes válasz egymás után)   





Felhasználókezelés
POST /register
Request:
```json
{
  "username": "oliver",
  "email": "oliver@email.com",
  "password": "jelszo123"
}
```
Response (sikeres):
```json
{
  "id": 123,
  "username": "oliver",
  "email": "oliver@email.com",
  "created_at": "2025-09-21T16:00:00Z"
}
```
Response (hiba):
```json
{
  "error": "Username already exists"
}
```

POST /login
Request:
```json
{
  "username": "oliver",
  "password": "jelszo123"
}
```
Response (sikeres):
```json
{
  "token": "jwt.token.string",
  "user": {
    "id": 123,
    "username": "oliver",
    "email": "oliver@email.com"
  }
}
```
Response (hiba):
```json
{
  "error": "Invalid credentials"
}
```

POST /logout
Request: (általában csak token a headerben)
Response:
```json
{
  "message": "Logged out successfully"
}
```

GET /profile
Response:
```json
{
  "id": 123,
  "username": "oliver",
  "email": "oliver@email.com",
  "created_at": "2025-09-21T16:00:00Z",
  "xp": 1200,
  "level": 5,
  "streak": 7,
  "avatar_url": "https://cdn.codelingo.com/avatars/oliver.png"
}
```

PUT /profile
Request:
```json
{
  "email": "uj@email.com",
  "avatar_url": "https://cdn.codelingo.com/avatars/oliver2.png"
}
```
Response:
```json
{
  "message": "Profile updated"
}
```

PUT /profile/password
Request:
```json
{
  "old_password": "jelszo123",
  "new_password": "ujjelszo456"
}
```
Response:
```json
{
  "message": "Password changed successfully"
}
```
Response (hiba):
```json
{
  "error": "Old password incorrect"
}
```

Kvíz / kérdések
GET /questions?lang=python&difficulty=easy&count=10
Response:
```json
{
  "session_id": "abc123",
  "questions": [
    {
      "id": 1,
      "type": "multiple_choice",
      "question": "Mi lesz az alábbi kód kimenete?",
      "code": "print(2 + 2)",
      "options": ["2", "4", "22", "Hiba"],
      "language": "python",
      "difficulty": "easy"
    },
    {
      "id": 2,
      "type": "fill_in_the_blank",
      "question": "Egészítsd ki a hiányzó részt!",
      "code": "for i in range(___):",
      "answer_length": 1,
      "language": "python",
      "difficulty": "easy"
    }
    // ... további kérdések
  ]
}
```

POST /questions/answer
Request:
```json
{
  "session_id": "abc123",
  "answers": [
    { "question_id": 1, "answer": "4" },
    { "question_id": 2, "answer": "10" }
  ]
}
```
Response:
```json
{
  "results": [
    { "question_id": 1, "correct": true, "correct_answer": "4" },
    { "question_id": 2, "correct": false, "correct_answer": "5" }
  ],
  "score": 1,
  "total": 2
}

```


GET /results/session/{id}
Response:
```json
{
  "session_id": "abc123",
  "user_id": 123,
  "score": 8,
  "total": 10,
  "answers": [
    { "question_id": 1, "answer": "4", "correct": true },
    { "question_id": 2, "answer": "10", "correct": false }
    // ...
  ],
  "completed_at": "2025-09-21T16:30:00Z"
}
```

POST /results/session
Request:
```json
{
  "session_id": "abc123",
  "score": 8,
  "total": 10
}
```
Response:
```json
{
  "message": "Session results saved"
}
```

Pontszám / szint / ranglista
GET /leaderboard
Response:
```json
{
  "leaderboard": [
    { "rank": 1, "username": "anna", "xp": 2500, "level": 8 },
    { "rank": 2, "username": "oliver", "xp": 2200, "level": 7 },
    { "rank": 3, "username": "bence", "xp": 2000, "level": 7 }
    // ...
  ],
  "user_rank": 2
}
```

GET /users/me/progress
Response:
```json
{
  "xp": 2200,
  "level": 7,
  "streak": 5,
  "next_level_xp": 2500
}
```


Admin funkciók
POST /questions
Request:
```json
{
  "type": "multiple_choice",
  "question": "Mi lesz az alábbi kód kimenete?",
  "code": "print(2 + 2)",
  "options": ["2", "4", "22", "Hiba"],
  "correct_answer": "4",
  "language": "python",
  "difficulty": "easy"
}
```
Response:
```json
{
  "id": 101,
  "message": "Question created"
}
```

PUT /questions/{id}
Request:
```json
{
  "question": "Mi lesz az alábbi kód kimenete?",
  "code": "print(3 + 3)",
  "options": ["3", "6", "33", "Hiba"],
  "correct_answer": "6",
  "language": "python",
  "difficulty": "easy"
}
```
Response:
```json
{
  "message": "Question updated"
}
```

DELETE /questions/{id}
Response:
```json
{
  "message": "Question deleted"
}
```

POST /questions/import
Request: (általában fájl feltöltés, de lehet metaadat is)
Response:
```json
{
  "imported": 25,
  "errors": [
    { "row": 3, "error": "Missing correct_answer" }
  ]
}
```

GET /questions/export
Response: (általában fájl, de lehet metaadat is)
```json
{
  "url": "https://cdn.codelingo.com/exports/questions_20250921.csv"
}
```


