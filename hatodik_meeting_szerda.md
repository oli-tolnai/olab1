# 2025.10.01. szerda - Hatodik meeting

## Design Leaderboard API Contracts

### **GET /leaderboard**

### Query Paraméterek
| Paraméter     | Típus   | Kötelező | Leírás                                                                                                  |
| ------------- | ------- | -------- | ------------------------------------------------------------------------------------------------------- |
| `page`        | int     | nem      | Oldalszám (alapértelmezett: 1)                                                                          |
| `pageSize`    | int     | nem      | Oldalméret, max. 100 (alapértelmezett: 20)                                                              |
| `language`    | string  | nem      | Szűrés programnyelv szerint (pl. `python`, `javascript`)                                                |
| `difficulty`  | string  | nem      | Szűrés nehézség szerint (`easy`, `medium`, `hard`)                                                      |
| `timeRange`   | string  | nem      | Ranglista időtartam (`alltime`, `weekly`, `daily`)                                                      |
| `includeUser` | boolean | nem      | Ha `true`, a bejelentkezett felhasználó helyezését is visszaadja, akkor is ha nem esik az adott oldalba |

### Válasz
```json
{
  "page": 1,
  "pageSize": 20,
  "totalEntries": 5234,
  "totalPages": 262,
  "filters": {
    "language": "python",
    "difficulty": "medium",
    "timeRange": "weekly"
  },
  "leaderboard": [
    {
      "rank": 1,
      "userId": "u123",
      "username": "CodeMaster",
      "challengesCompleted": 75,
      "score": 9800,
      "language": "python",
      "difficulty": "medium",
      "avatarUrl": "https://cdn.codelingo.com/avatars/u123.png"
    },
    {
      "rank": 2,
      "userId": "u456",
      "username": "DevNinja",
      "score": 9750,
      "language": "python",
      "difficulty": "medium",
      "avatarUrl": "https://cdn.codelingo.com/avatars/u456.png"
    }
  ],
  "currentUser": {
    "rank": 134,
    "userId": "u789",
    "username": "Me",
    "score": 4500,
    "language": "python",
    "difficulty": "medium",
    "avatarUrl": "https://cdn.codelingo.com/avatars/u789.png",
    "isOnPage": false
  }
}

```

### Hibakódok
| Kód | Üzenet               | Leírás                                           |
| --- | -------------------- | ------------------------------------------------ |
| 400 | `INVALID_FILTER`     | Hibás filter paraméter (pl. nem létező nyelv)    |
| 400 | `INVALID_PAGINATION` | Oldalszám vagy pageSize hibás                    |
| 404 | `USER_NOT_FOUND`     | Ha a `includeUser=true`, de a user nem található |
| 500 | `INTERNAL_ERROR`     | Szerver oldali hiba                              |
| 503 | `SERVICE_UNAVAILABLE`| Szolgáltatás nem elérhető                        |

### Ranking és Tie-breaking logika
- Elsődleges rendezés: pontszám csökkenő sorrendben
- Másodlagos rendezés (döntetlen esetén): a döntetlen helyezéseket azonos rangként kezeljük, és a következő helyezés kihagyásra kerül.
  - Példa: Ha két felhasználó is 9800 ponttal rendelkezik, mindketten az 1. helyen lesznek, a következő felhasználó pedig a 3. helyen szerepel.



------
----- 

<br><br>

## Design User Stats API Contracts

### GET /api/v1/progress/users/{id}/stats

### Path Paraméterek
| Paraméter | Típus  | Kötelező | Leírás                        |
| --------- | ------ | -------- | ----------------------------- |
| `id`      | string | igen     | A felhasználó egyedi azonosítója |

### Query Paraméterek
| Paraméter             | Típus   | Kötelező | Leírás                                                                           |
| --------------------- | ------- | -------- | -------------------------------------------------------------------------------- |
| `timeRange`           | string  | nem      | Az aggregáció időintervalluma. Értékek: `alltime` (default), `weekly`, `monthly` |
| `includeTrends`       | boolean | nem      | Ha `true`, akkor részletes trendadatokat is visszaad (alapértelmezett: true)     |
| `includeAchievements` | boolean | nem      | Ha `true`, akkor az achievementek/mérföldkövek státuszát is visszaadja           |

### Válasz
```json
{
  "userId": "u123",
  "username": "CodeMaster",
  "avatarUrl": "https://cdn.codelingo.com/avatars/u123.png",
  "aggregatedStats": {
    "totalScore": 15230,
    "accuracy": 87.5,
    "sessionsCompleted": 120,
    "challengesCompleted": 340,
    "currentStreak": 12,
    "longestStreak": 25
  },
  "languageBreakdown": [
    {
      "language": "python",
      "totalScore": 9000,
      "accuracy": 89.2,
      "challengesCompleted": 210
    },
    {
      "language": "javascript",
      "totalScore": 6230,
      "accuracy": 85.0,
      "challengesCompleted": 130
    }
  ],
  "difficultyBreakdown": [
    {
      "difficulty": "easy",
      "totalScore": 3000,
      "accuracy": 95.1
    },
    {
      "difficulty": "medium",
      "totalScore": 7200,
      "accuracy": 88.3
    },
    {
      "difficulty": "hard",
      "totalScore": 5030,
      "accuracy": 76.9
    }
  ],
  "timeTrends": {
    "daily": [
      { "date": "2025-09-25", "score": 120, "accuracy": 90.0 },
      { "date": "2025-09-26", "score": 350, "accuracy": 88.5 },
      { "date": "2025-09-27", "score": 200, "accuracy": 92.0 }
    ],
    "weekly": [
      { "week": "2025-W37", "score": 2100, "accuracy": 87.0 },
      { "week": "2025-W38", "score": 1890, "accuracy": 85.5 }
    ],
    "monthly": [
      { "month": "2025-08", "score": 7800, "accuracy": 86.2 },
      { "month": "2025-09", "score": 7430, "accuracy": 88.1 }
    ]
  },
  "achievements": [
    {
      "id": "achv_100",
      "name": "First 100 Challenges",
      "description": "Complete 100 challenges",
      "unlocked": true,
      "unlockedAt": "2025-07-15T14:32:00Z"
    },
    {
      "id": "achv_streak_10",
      "name": "10-Day Streak",
      "description": "Maintain a 10-day streak",
      "unlocked": true,
      "unlockedAt": "2025-09-27T09:20:00Z"
    },
    {
      "id": "achv_streak_30",
      "name": "30-Day Streak",
      "description": "Maintain a 30-day streak",
      "unlocked": false,
      "unlockedAt": null
    }
  ]
}
```
### Megjegyzések a számítási logikához
- Pontosság (accuracy): helyes válaszok / összes válasz * 100
- Streak számítás: egymást követő napokon végzett gyakorlások száma
- Trends adatok: cache-ből vagy előaggregált táblákból (performance optimalizáció miatt)
- Achievements: user progress alapján unlock, minden unlockedAt timestamp ISO 8601



------
----- 

<br><br>

## Language Management API Contract
### Entity: Language
```json
{
  "id": "lang_001",
  "name": "Python",
  "code": "python",
  "version": "3.11",
  "isActive": true,
  "createdAt": "2025-09-01T10:15:00Z",
  "updatedAt": "2025-09-20T08:45:00Z",
  "metadata": {
    "syntaxHighlighting": "python",
    "fileExtensions": [".py"],
    "paradigm": ["object-oriented", "procedural"]
  }
}
```

### Endpoints
#### 1. GET /admin/languages
Listázza az összes nyelvet (szűrhető állapot szerint).

### Query Paraméterek
| Paraméter  | Típus   | Kötelező | Leírás                                  |
| ---------- | ------- | -------- | --------------------------------------- |
| `isActive` | boolean | nem      | Csak az aktív/inaktív nyelvek listázása |

### 200 OK példa válasz:
```json
{
  "languages": [
    {
      "id": "lang_001",
      "name": "Python",
      "code": "python",
      "version": "3.11",
      "isActive": true,
      "createdAt": "2025-09-01T10:15:00Z",
      "updatedAt": "2025-09-20T08:45:00Z",
      "metadata": {
        "syntaxHighlighting": "python",
        "fileExtensions": [".py"],
        "paradigm": ["object-oriented", "procedural"]
      }
    },
    {
      "id": "lang_002",
      "name": "JavaScript",
      "code": "javascript",
      "version": "ES2023",
      "isActive": true,
      "createdAt": "2025-09-01T10:15:00Z",
      "updatedAt": "2025-09-20T08:45:00Z",
      "metadata": {
        "syntaxHighlighting": "javascript",
        "fileExtensions": [".js"],
        "paradigm": ["event-driven", "functional", "oop"]
      }
    }
  ]
}
```

### 2. POST /admin/languages
Új nyelv létrehozása.

**Request body:**
```json
{
  "name": "C#",
  "code": "csharp",
  "version": "12",
  "isActive": true,
  "metadata": {
    "syntaxHighlighting": "csharp",
    "fileExtensions": [".cs"],
    "paradigm": ["object-oriented"]
  }
}
```

### 201 Created példa válasz:
```json
{
  "id": "lang_003",
  "name": "C#",
  "code": "csharp",
  "version": "12",
  "isActive": true,
  "createdAt": "2025-10-01T12:20:00Z",
  "updatedAt": "2025-10-01T12:20:00Z",
  "metadata": {
    "syntaxHighlighting": "csharp",
    "fileExtensions": [".cs"],
    "paradigm": ["object-oriented"]
  }
}
```


### 3. PUT /admin/languages/{id}
Nyelv konfiguráció frissítése.

### Path paraméterek:
- id (string, kötelező) – nyelv azonosító

### Request body:
```json
{
  "name": "Python",
  "version": "3.12",
  "isActive": false,
  "metadata": {
    "syntaxHighlighting": "python",
    "fileExtensions": [".py", ".pyw"],
    "paradigm": ["object-oriented", "procedural", "functional"]
  }
}
```

### 200 OK példa válasz:
```json
{
  "id": "lang_001",
  "name": "Python",
  "code": "python",
  "version": "3.12",
  "isActive": false,
  "createdAt": "2025-09-01T10:15:00Z",
  "updatedAt": "2025-10-01T12:40:00Z",
  "metadata": {
    "syntaxHighlighting": "python",
    "fileExtensions": [".py", ".pyw"],
    "paradigm": ["object-oriented", "procedural", "functional"]
  }
}
```

### 4. DELETE /admin/languages/{id}
Nyelv törlése.

### Path paraméterek:
- id (string, kötelező) – nyelv azonosító

### 204 No Content – sikeres törlés esetén nincs response body

### Hibakódok
| Kód | Üzenet               | Leírás                                          |
| --- | -------------------- | ----------------------------------------------- |
| 400 | `VALIDATION_ERROR`   | Kötelező mezők hiányoznak vagy hibás formátum   |
| 400 | `DUPLICATE_LANGUAGE` | Már létezik ugyanilyen `code` mezővel nyelv     |
| 403 | `ACCESS_DENIED`      | Nincs admin jogosultság                         |
| 404 | `LANGUAGE_NOT_FOUND` | A kért nyelv nem található                      |
| 409 | `LANGUAGE_IN_USE`    | A nyelvhez tartozó kérdések miatt nem törölhető |
| 500 | `INTERNAL_ERROR`     | Szerver oldali hiba                             |
