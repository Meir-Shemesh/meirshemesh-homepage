# CLAUDE.md

מסמך-יסוד לפרויקט זה. פרויקט git עצמאי, לא קשור לפרויקטים אחרים באותה תיקיית-אב (למשל geopolitics-tracker) - אין ביניהם import, module, או תלות משותפת מכל סוג.

## מטרת הפרויקט

אתר-הבית האישי של מאיר שמש, ב-meirshemesh.com. אתר סטטי טהור, דו-לשוני עברית-אנגלית, מוגש דרך GitHub Pages מתוך `docs/`.

## מבנה הפרויקט

```
docs/
  index.html       redirect אוטומטי ל-he/index.html (meta refresh + JS fallback + קישור ידני)
  he/index.html     עמוד הבית בעברית - ברירת המחדל, RTL
  en/index.html     עמוד הבית באנגלית, LTR
  assets/images/    meir-photo.jpg (תמונת-פרופיל 480x480, מוצגת ב-hero כ-.avatar-photo בגודל 120px)
                    MS_Logo.png (לוגו מקור 1024x1024 - נכס-מקור בלבד, לא מוצג ישירות; לשימוש עתידי, למשל favicon)
                    MS_Logo-128.png (עותק 128x128 של הלוגו, מוצג בניווט העליון כ-.site-logo בגודל 32px)
```

- `he/index.html` ו-`en/index.html` הם קבצים עצמאיים לגמרי, כל אחד עם `<style>` inline משלו. אין stylesheet משותף, אין templating, אין build - זהו עיצוב מכוון, לא פער שצריך לתקן. כל שינוי עיצובי צריך להיעשות בשני הקבצים בנפרד.
- אין תלות בין `he/` ל-`en/` מעבר לקישורי מתג-השפה ביניהם (`../en/index.html` ↔ `../he/index.html`).
- אין JavaScript מעבר להכרחי: מתג השפה הוא קישור `<a>` רגיל, ואקורדיון ה"קרא עוד" (בכרטיסי "ייעוץ" ו"מודיעין תחרותי") בנוי על `<details>/<summary>` סמנטי ללא JS. שני הכרטיסים פתוחים כברירת מחדל (attribute `open`), והגולש יכול לכווץ אותם. קובץ ה-redirect העליון (`docs/index.html`) הוא היוצא מן הכלל היחיד - הוא משתמש ב-JS מינימלי (`location.replace`) כגיבוי ל-meta refresh.

## פלטת-צבעים וגופן

זהים לאתר geopolitics.meirshemesh.com הקיים (פרויקט נפרד, ללא תלות קוד - רק שיתוף שפה עיצובית מכוון):

| טוקן | ערך (light) | תפקיד |
|---|---|---|
| `--bg` | `#F3EFE8` | רקע כללי |
| `--bg-elevated` | `#FFFDFA` | רקע כרטיסים/ניווט |
| `--text` | `#221F1B` | טקסט (דיו) |
| `--text-muted` | `#6D675E` | טקסט משני |
| `--border` | `#E4DDD0` | קווים מפרידים |
| `--brand` | `#7A2E2A` | בורדו - accent, קישורים, כותרות סעיפים |
| `--hero-bg` / `--hero-text` | `#7A2E2A` / `#FFFDFA` | רקע ה-hero (עומד בפני עצמו, לא נגזר מ-`--brand` כדי שישאר "בורדו מלא" גם ב-dark mode) |
| `--avatar-shadow` | `0 6px 18px rgba(0,0,0,.30)` | צל תמונת-הפרופיל ב-hero (חזק יותר, `.55`, ב-dark mode) |
| `--cat-purple` | `#5C3D82` | ניתוח אסטרטגי / מודיעין תחרותי |
| `--cat-blue` | `#185FA5` | AI / Geopolitics Tracker |
| `--cat-green` | `#0F6E56` | אקולוגיה / AvantGuard |
| `--cat-coral` | `#993C1D` | ניהול ארגוני |

גופן: Assistant, נטען דרך Google Fonts (`fonts.googleapis.com`) - לא self-hosted, בניגוד ל-geopolitics-tracker.

## Theming

כל הצבעים עוברים דרך CSS custom properties תחת `:root`. לכל טוקן יש override תחת `@media (prefers-color-scheme: dark)` (עם guard של `:root:not([data-theme="light"])`) וגם תחת `:root[data-theme="dark"]` מפורש - כך שאם בעתיד תתווסף לחצן מתג-מצב ידני, הוא יעבוד מיד בלי לגעת בטוקנים. לעולם לא לקבוע צבע ישירות במקום להשתמש בטוקן קיים או חדש.

`--brand` ושאר טוקני ה-`--cat-*` הם "טוקני accent" שהופכים לגוון בהיר יותר ב-dark mode (לשמירה על ניגודיות על רקע כהה) - בהתאם למוסכמה הקיימת ב-geopolitics-tracker. `--hero-bg`/`--hero-text` הם טוקנים נפרדים שנשארים "בורדו כהה + טקסט בהיר" בשני המצבים (רק גוון הבורדו מעט מועמק ב-dark), כי מדובר ברקע-בלוק גדול ולא ב-accent קטן.

## כללי עבודה קבועים

- כל שינוי תוכן עתידי (טקסט, צבע, מבנה) מחייב רנדר-מחדש ובדיקה ויזואלית בדפדפן - פתיחת `docs/he/index.html` ו-`docs/en/index.html` ישירות מהדיסק - לפני commit. זה כולל בדיקת שני מצבי ה-accordion (פתוח/סגור) בכרטיסי "ייעוץ" ו"מודיעין תחרותי", ובדיקת קישור מתג-השפה בשני הכיוונים. התהליך הטכני כאן פשוט בהרבה מ-geopolitics-tracker (אין סקריפט build, אין נתונים דינמיים) אבל העיקרון זהה.
- כל הטקסט הגלוי הוא עברית (RTL) ב-`he/`, אנגלית (LTR) ב-`en/`. אין toggle דינמי בתוך אותו HTML - שני עמודים נפרדים.

## מגבלות והעדפות

- אין ואסור להוסיף build/bundler/package.json/תלויות - כל HTML נפתח ישירות בדפדפן.
- אין תלות קוד בפרויקטים אחרים בתיקיית-האב (First Project, תנך ופיזיקה, geopolitics-tracker) - זהו repo git נפרד לגמרי.
- קישורים חיצוניים (AvantGuard, Geopolitics Tracker) נפתחים בטאב חדש (`target="_blank" rel="noopener"`).
- תצוגת מחשב: מ-1024px ומעלה גדלי הפונט של תוכן הסקשנים מוגדלים ב-`@media (min-width: 1024px)` בסוף ה-CSS. ה-`max-width` של הסקשנים (880px) נשאר קבוע במכוון - התאמת מראה בדסקטופ נעשית דרך גדלי פונט, לא דרך הרחבת המכולה, אלא אם הוחלט אחרת.
- בדיקה ויזואלית לפני commit כוללת רוחבי דסקטופ (לפחות 1440px ו-1920px) ולא רק מובייל.

## פקודות הפעלה ובדיקה

אין build, אין lint, אין טסטים. "הרצה" = פתיחת `docs/he/index.html` או `docs/en/index.html` ישירות בדפדפן. פריסה: GitHub Pages מוגדר להגיש מתוך `docs/` בענף הראשי.
