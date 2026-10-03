# HANDOFF.md

תמונת-מצב נוכחית של הפרויקט. נכתב מחדש במלואו בכל סגירת-סשן (`/handoff`) - לא יומן כרונולוגי.

## מצב הפרויקט הנוכחי

אתר-הבית האישי של מאיר שמש חי ב-meirshemesh.com (GitHub Pages, מ-`docs/` בענף `master`). כל מה שתואר במפרט המקורי קיים ועובד: עמודי he/en עצמאיים, hero עם תמונת-פרופיל אמיתית ולוגו בניווט, 4 כרטיסי כישורים, 4 כרטיסי פעילות (2 קישורים חיצוניים + 2 accordion פתוחים כברירת מחדל), יצירת קשר (מייל + LinkedIn), פלטת-צבעים חדשה (warm tan/dark) עם toggle ידני ל-dark/light (שמור ב-localStorage) ו-`@media print` שכופה תמיד light.

`.git` הוא symlink קיים אל `C:\git-data\meirshemesh-homepage.git` (מחוץ לעץ-המסונכרן-ע"י-OneDrive) - `git fsck --full --strict` נקי. ראו הרחבה בסעיף "OneDrive וסנכרון .git" ב-CLAUDE.md.

מנגנון ההמשכיות (`/resume-project`, `/handoff`, הקובץ הזה, `PROJECT_LOG.md`) פעיל ומתוחזק מאז 2026-10-03.

## מה הושלם

1. מבנה ראשוני: `docs/he/`, `docs/en/`, `docs/index.html` (redirect ל-he), `CLAUDE.md`, `README.md`.
2. תמונת-פרופיל אמיתית (`meir-photo.jpg`) ולוגו (`MS_Logo.png` מקור + `MS_Logo-128.png` לניווט) - הוחלפו placeholder-ים.
3. תיקוני תצוגת-דסקטופ: לוגו הוגדל ל-44px, פונטי תוכן הוגדלו מ-1024px, שני כרטיסי ה-accordion נפתחים כברירת מחדל, תיקון ניסוח "אקולוגית וברת-קיימא" ל"ובת-קיימא".
4. פלטת-צבעים חדשה (warm tan/dark, טוקן `--accent2` חדש) + כפתור toggle ידני ל-dark/light עם localStorage (מפתח `ms-theme`) + `@media print` שכופה light.
5. תיקוני ניסוח בפסקת-האודות (שתי השפות, כולל שחזור משפט-הפתיחה ו-"the Israeli Prime Minister's Office" באנגלית), תיקון "מידע... רב-מקורי" ל"ממקורות רבים ומגוונים" בשני המקומות שהופיע, הסרת "תשעה"/"nine" מתיאור Geopolitics Tracker.
6. הוספת קישור LinkedIn לסקשן יצירת-הקשר (שתי השפות).
7. הקמת מנגנון resume-project/handoff: `.claude/skills/resume-project/SKILL.md`, `.claude/skills/handoff/SKILL.md`, סעיפי "המשכיות בין-סשנים" ו-"OneDrive וסנכרון .git" ב-CLAUDE.md, `HANDOFF.md`, `PROJECT_LOG.md`. **בוצע commit+push** (`73d7429`).

## קבצים שנוצרו או שונו

כל השינויים עד כה כבר committed ו-pushed ל-`origin/master`. שום קובץ לא שונה בסשן הנוכחי (ראו "סשן אחרון").

## החלטות שהתקבלו

- `--hero-bg`/`--hero-text`/`--avatar-shadow`/`--cat-*` נשארו בכוונה מהפלטה הישנה כששונתה הפלטה הבסיסית ב-2026-09-27 - לא התבקש עדכון שלהם.
- ה-symlink הקיים של `.git` (אל `C:\git-data\meirshemesh-homepage.git`) לא שונה ל-Junction - הוא עובד (`fsck` נקי), ושינוי תשתית-git לא נדרש בלי בעיה בפועל. אם יתגלה כשל בעתיד (למשל במחשב נוסף בלי הרשאת-symlink) - ההליך לתיקון מתועד ב-CLAUDE.md.
- לא נוצר `.gitignore` - אין קבצים שצריך להחריג; כל עץ הפרויקט (346K) כבר ב-git.

## משימות פתוחות

- `favicon` לאתר (מ-`MS_Logo.png`, באותה מוסכמה כמו geopolitics-tracker) - צוין כ"לשימוש עתידי" אבל עדיין לא בוצע.
- לא אומת בפועל (על-ידי Claude) שהגדרות GitHub Pages/DNS עבור `meirshemesh.com` תואמות ל-`docs/CNAME` הקיים - זה נוסף ע"י המשתמש ישירות ב-GitHub, לא דרך הסשנים האלה.

## בעיות ידועות

- `.git` הוא symbolic link ולא Junction - עובד כרגע במחשב הזה, אך symlink-ים יכולים לדרוש הרשאה שלא בהכרח קיימת בכל מחשב/חשבון. אם זה יתגלה כבעיה במחשב אחר - יש הליך מתועד ב-CLAUDE.md (לשכפל מה-remote, לא לתקן במקום).
- אין lint/test/CI כלל בפרויקט הזה (במכוון - אין build). כל אימות עד כה היה רינדור ויזואלי ידני (headless Chrome) לפני כל commit.

## הצעד הבא המומלץ

אין משימה פתוחה דחופה. הצעד הבא הוא איזו מהמשימות הפתוחות שתירצה (favicon / אימות DNS), או כל בקשה חדשה.

## סשן אחרון

**2026-10-03** - הפעלת `/handoff` בלי עבודה חדשה מאז ה-commit הקודם (`73d7429`, הקמת מנגנון resume-project/handoff). נבדק `git status` - נקי, אין מה לבצע לו commit. תוקן מידע ישן ב-HANDOFF.md שהתייחס ל-commit כ"ממתין לאישור" (הוא כבר בוצע ונדחף). `PROJECT_LOG.md` לא נגע - הסשן היה טכני-בלבד, בלי החלטה/ממצא/שינוי-אסטרטגי חדש.
