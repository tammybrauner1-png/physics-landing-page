# פיזיקה בתדר גבוה — דף נחיתה

דף נחיתה להרשמה לקבוצת הפיזיקה "פיזיקה בתדר גבוה" מבית התדר.

## הגדרה

### 1. תמונות
שימו את התמונות בתיקיית `assets/`:
- `assets/logo-brain.png` — לוגו המוח
- `assets/physics-group.jpg` — תמונת הקבוצה ב-hero

### 2. Google Sheets (טופס הרשמה)
1. צרו Google Sheet חדש
2. Extensions → Apps Script
3. הדביקו את הקוד הבא:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data = JSON.parse(e.postData.contents);
  
  // Add headers if sheet is empty
  if (sheet.getLastRow() === 0) {
    sheet.appendRow(['תאריך', 'שם מלא', 'טלפון', 'כיתה', 'יחידות', 'בית ספר', 'מה דיבר אליך', 'הערות', 'מקור']);
  }
  
  sheet.appendRow([
    new Date().toLocaleString('he-IL'),
    data.fullName,
    data.phone,
    data.grade,
    data.units,
    data.school,
    (data.interests || []).join(', '),
    data.notes,
    data.source
  ]);
  
  return ContentService.createTextOutput(JSON.stringify({ status: 'ok' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Deploy → New deployment → Web app → Anyone can access
5. העתיקו את ה-URL שקיבלתם
6. ב-`index.html` החליפו את `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` ב-URL שלכם

### 3. GitHub Pages
1. צרו repo חדש ב-GitHub
2. דחפו את הקבצים:
```bash
git init
git add .
git commit -m "Initial commit - physics landing page"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```
3. Settings → Pages → Source: Deploy from branch → main → / (root) → Save
4. הדף יהיה זמין ב: `https://YOUR_USERNAME.github.io/YOUR_REPO/`

## מבנה הקבצים
```
physics/
├── index.html          # דף הנחיתה
├── assets/
│   ├── logo-brain.png  # לוגו מוח
│   └── physics-group.jpg # תמונת hero
└── README.md           # קובץ זה
```
