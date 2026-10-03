# HANDOFF.md

תמונת-מצב נוכחית של הפרויקט. נכתב מחדש במלואו בכל סגירת-סשן (`/handoff`) - לא יומן כרונולוגי.

## מצב הפרויקט הנוכחי

אתר-הבית האישי של מאיר שמש חי ב-meirshemesh.com (GitHub Pages, מ-`docs/` בענף `master`). כל מה שתואר במפרט המקורי קיים ועובד: עמודי he/en עצמאיים, hero עם תמונת-פרופיל אמיתית ולוגו בניווט, 4 כרטיסי כישורים, 4 כרטיסי פעילות (2 קישורים חיצוניים + 2 accordion פתוחים כברירת מחדל), יצירת קשר (מייל + LinkedIn), פלטת-צבעים חדשה (warm tan/dark) עם toggle ידני ל-dark/light (שמור ב-localStorage) ו-`@media print` שכופה תמיד light.

`.git` הוא symlink קיים אל `C:\git-data\meirshemesh-homepage.git` (מחוץ לעץ-המסונכרן-ע"י-OneDrive) - `git fsck --full --strict` נקי. ראו הרחבה בסעיף "OneDrive וסנכרון .git" ב-CLAUDE.md.

## מה הושלם

1. מבנה ראשוני: `docs/he/`, `docs/en/`, `docs/index.html` (redirect ל-he), `CLAUDE.md`, `README.md`.
2. תמונת-פרופיל אמיתית (`meir-photo.jpg`) ולוגו (`MS_Logo.png` מקור + `MS_Logo-128.png` לניווט) - הוחלפו placeholder-ים.
3. תיקוני תצוגת-דסקטופ: לוגו הוגדל ל-44px, פונטי תוכן הוגדלו מ-1024px, שני כרטיסי ה-accordion נפתחים כברירת מחדל, תיקון ניסוח "אקולוגית וברת-קיימא" ל"ובת-קיימא".
4. פלטת-צבעים חדשה (warm tan/dark, טוקן `--accent2` חדש) + כפתור toggle ידני ל-dark/light עם localStorage (מפתח `ms-theme`) + `@media print` שכופה light.
5. תיקוני ניסוח בפסקת-האודות (שתי השפות, כולל שחזור משפט-הפתיחה ו-"the Israeli Prime Minister's Office" באנגלית), תיקון "מידע... רב-מקורי" ל"ממקורות רבים ומגוונים" בשני המקומות שהופיע, הסרת "תשעה"/"nine" מתיאור Geopolitics Tracker.
6. הוספת קישור LinkedIn לסקשן יצירת-הקשר (שתי השפות).
7. **(סשן נוכחי)** הקמת מנגנון resume-project/handoff: נוצרו `.claude/skills/resume-project/SKILL.md` ו-`.claude/skills/handoff/SKILL.md`, נוסף סעיף "המשכיות בין-סשנים" ל-CLAUDE.md, נוסף סעיף "OneDrive וסנכרון .git" ל-CLAUDE.md (עם ממצאי ה-fsck/symlink), נוצרו קובץ זה ו-`PROJECT_LOG.md` (המשתמש אישר).

## קבצים שנוצרו או שונו (בסשן הנוכחי)

- `.claude/skills/resume-project/SKILL.md` - חדש
- `.claude/skills/handoff/SKILL.md` - חדש
- `CLAUDE.md` - שונה (שני סעיפים נוספו: המשכיות בין-סשנים, OneDrive וסנכרון .git)
- `HANDOFF.md` - חדש (קובץ זה)
- `PROJECT_LOG.md` - חדש, לבקשת המשתמש

## החלטות שהתקבלו

- `--hero-bg`/`--hero-text`/`--avatar-shadow`/`--cat-*` נשארו בכוונה מהפלטה הישנה כששונתה הפלטה הבסיסית ב-2026-09-27 - לא התבקש עדכון שלהם.
- ה-symlink הקיים של `.git` (אל `C:\git-data\meirshemesh-homepage.git`) לא שונה ל-Junction - הוא עובד (`fsck` נקי), ושינוי תשתית-git לא נדרש בלי בעיה בפועל. אם יתגלה כשל בעתיד (למשל במחשב נוסף בלי הרשאת-symlink) - ההליך לתיקון מתועד ב-CLAUDE.md.
- לא נוצר `.gitignore` - אין קבצים שצריך להחריג; כל עץ הפרויקט (346K) כבר ב-git.

## משימות פתוחות

- רצף ה-git (add + אישור הודעת commit + commit + push) לכל התוספות של הסשן הנוכחי (הסקילים, CLAUDE.md, HANDOFF.md) - ממתין לאישור המשתמש, ראו "בעיות ידועות".
- `favicon` לאתר (מ-`MS_Logo.png`, באותה מוסכמה כמו geopolitics-tracker) - צוין כ"לשימוש עתידי" אבל עדיין לא בוצע.
- לא אומת בפועל (על-ידי Claude) שהגדרות GitHub Pages/DNS עבור `meirshemesh.com` תואמות ל-`docs/CNAME` הקיים - זה נוסף ע"י המשתמש ישירות ב-GitHub, לא דרך הסשנים האלה.

## בעיות ידועות

- `.git` הוא symbolic link ולא Junction - עובד כרגע במחשב הזה, אך symlink-ים יכולים לדרוש הרשאה שלא בהכרח קיימת בכל מחשב/חשבון. אם זה יתגלה כבעיה במחשב אחר - יש הליך מתועד ב-CLAUDE.md (לשכפל מה-remote, לא לתקן במקום).
- אין lint/test/CI כלל בפרויקט הזה (במכוון - אין build). כל אימות עד כה היה רינדור ויזואלי ידני (headless Chrome) לפני כל commit.

## הצעד הבא המומלץ

להציג `git status`/`git diff --cached --stat` של כל השינויים (סקילים + CLAUDE.md + HANDOFF.md + PROJECT_LOG.md), להציע הודעת commit, ולבצע commit+push רק אחרי אישור מפורש.

## סשן אחרון

**2026-10-03** - הקמת מנגנון resume-project/handoff לפרויקט: שני קבצי-סקיל (`resume-project`, `handoff`, שניהם `disable-model-invocation: true`), בדיקת `.git`/OneDrive (נמצא symlink קיים ותקין אל `C:\git-data\meirshemesh-homepage.git`, `git fsck` נקי, אין נתוני-סיכון נוספים בעץ), עדכון CLAUDE.md בהתאם, ויצירת HANDOFF.md ו-PROJECT_LOG.md (המשתמש אישר את האחרון). טרם בוצע commit - ממתין לאישור הודעת commit.
