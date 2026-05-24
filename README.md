# ProjectApiAngular

פרויקט זה משלב אפליקציית Front-end מתקדמת מבוססת Angular יחד עם ממשק API אחורי (Backend) המנהל את הלוגיקה העסקית, מסדי הנתונים והאבטחה של המערכת.

---

## 🖥️ פרק א': צד הלקוח (Angular Front-End)

צד הלקוח בנוי בצורה מודולרית ורספונסיבית תוך שימוש ברכיבים הניתנים לשימוש חוזר ובשירותים ייעודיים לביצוע קריאות HTTP אל השרת.

### דרישות קדם
לפני הרצת הפרויקט בסביבה המקומית, ודא שהתקנת את התוכנות הבאות:
- Node.js (גרסה 16 ומעלה מומלצת)
- npm (מנהל החבילות הרשמי, המותקן אוטומטית יחד עם Node)
- Angular CLI (ניתן להתקנה גלובלית באמצעות: npm install -g @angular/cli)

### תחילת עבודה והרצה מקומית
בצע את השלבים הבאים כדי להגדיר, להתקין ולהריץ את הפרויקט באופן מקומי:

1. שכפול המאגר (Repository):
   git clone https://github.com/chasipovarsky/project_api_angular.git
   cd project_api_angular

2. התקנת תלויות (Dependencies):
   npm install

3. הגדרת משתני סביבה:
   נווט לתיקיית src/environments/ ועדכן את הקבצים environment.ts ו-environment.prod.ts עם כתובות ה-API של שרת הפיתוח ושרת הייצור בהתאמה.

4. הרצת שרת הפיתוח:
   ng serve
   
   האפליקציה תהיה זמינה בדפדפן בכתובת: http://localhost:4200/

### מבנה תיקיות הפרויקט
src/
├── app/
│   ├── components/      # רכיבי ממשק משתמש (UI Components)
│   ├── models/          # ממשקי TypeScript ומודלים של נתונים (Interfaces)
│   ├── pages/           # קומפוננטות דף ראשיות (Routes/Views)
│   ├── services/        # שירותי API ולוגיקת קשר מול השרת (HTTP Client)
│   ├── app-routing.module.ts
│   └── app.module.ts
├── assets/              # קבצים סטטיים (תמונות, אייקונים)
└── environments/        # קובצי הגדרות ומשתני סביבה (API Base URLs)

---

## ⚙️ פרק ב': ארכיטקטורה ולוגיקה של השרת (Server Logic)

השרת מתוכנן כ-RESTful API מודרני המבוסס על הפרדת רשויות (Separation of Concerns) ומחולק לשכבות לוגיות מרכזיות:

### 1. שכבת הניתוב והבקרים (Routing & Controllers)
שכבה זו אחראית על קבלת בקשות HTTP מצד הלקוח (Angular), פענוח הנתונים (Request Parameters / Body) והפנייתם לשירות המתאים.
- GET - שליפת נתונים ומשאבים מהשרת.
- POST - יצירת ישויות ונתונים חדשים.
- PUT / PATCH - עדכון נתונים קיימים.
- DELETE - מחיקת מידע ממסד הנתונים.

### 2. לוגיקה עסקית ואימות נתונים (Services & Validation)
- אימות קלט (Data Validation): השרת בודק את תקינות הנתונים המתקבלים לפני ביצוע פעולות כלשהן כדי למנוע הזרקות קוד או מידע חסר.
- ניהול שגיאות (Error Handling): השרת מחזיר קודי שגיאה תקניים (HTTP Status Codes) כגון 400 Bad Request, 401 Unauthorized, ו-500 Internal Server Error בצירוף הודעה מפורטת לצד הלקוח.

### 3. אבטחה, אימות והרשאות (Auth & Security)
- אימות מבוסס טוקן (JWT Authentication): תהליך ההתחברות וההרשמה מנפיק אסימון מוצפן (JSON Web Token) שנשלח לאפליקציית ה-Angular ונשמר שם לצורך אימות בקשות עתידיות ב-Header של ה-HTTP.
- מדיניות CORS: הגדרת מנגנוני Cross-Origin Resource Sharing המאפשרים לשרת לקבל בבטחה בקשות שמגיעות מכתובת הפיתוח של ה-Angular.

---

## 🛠️ כלי פיתוח ובדיקות

### יצירת רכיבים חדשים ב-Angular
ng generate component component-name

### הרצת בדיקות
- בדיקות יחידה (Unit Tests): ng test
- בדיקות מקצה לקצה (E2E Tests): ng e2e

### בנייה לסביבת ייצור (Production Build)
ng build --configuration production

תוצרי הבנייה המכווצים והממוטבים יישמרו בתוך תיקיית dist/ ויהיו מוכנים לפריסה בשרת האחסון.
