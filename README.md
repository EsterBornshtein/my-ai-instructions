# My AI Instructions

ריפו פרטי המכיל הנחיות אישיות לכלי AI (GitHub Copilot, Claude Code וכו'), החלות על כל הפרויקטים שלי - לא רק פרויקט ספציפי אחד.

## מבנה

- `task-workflow.instructions.md` - עמוד השדרה: כל שלבי התהליך על משימה, מהבקלוג ועד QA, לפי הסדר (כולל "עצירות חובה"). **אינו נטען אוטומטית** (ללא `applyTo`) - נטען רק כשבוחרים את ה-agent הייעודי `task-workflow.agent.md`.
- `task-workflow.agent.md` - **Custom Agent נפרד** (לא instructions) להרצת תהליך המשימה המלא. נבחר ידנית מתוך ה-agent picker ב-VS Code; קורא ל-task-workflow.instructions.md ועוקב אחריו שלב אחר שלב.
- `progress-checklist.instructions.md` - ניהול קובץ checklist חי למעקב התקדמות לאורך העבודה על משימה.
- `backlog-item-creation.instructions.md` - איך למלא פריט חדש בבקלוג (כותרת, תיאור, assignee, sprint, priority, סוג).
- `github-workflow.instructions.md` - הנחיות להתנהגות בכל הנוגע ל-Git/GitHub (commits, branches, PRs, Copilot review).
- `development-standards.instructions.md` - סטנדרטים לפיתוח (כיסוי טסטים, איסור שגיאות קומפילציה/TS).
- `copilot-review-triage.instructions.md` - איך לטפל בהערות של GitHub Copilot Review על PR.
- `investigation.agent.md` - **Custom Agent נפרד** (לא instructions) לחקירת/הבנת מערכת קיימת. עצמאי מתהליך task-workflow (ללא בקלוג/branch/PR/APPROVE), read-only + פקודות לא-הרסניות בלבד, מפיק קובץ תיעוד (למשל `docs/architecture.md`). נבחר ידנית מתוך ה-agent picker ב-VS Code.
- `bug-fixing.instructions.md` - מתודולוגיית חקירת באגים (שחזור, איסוף עדויות, בדיקת מספר כיוונים לפני קביעת שורש הבעיה). משלים את task-workflow.instructions.md עבור שלב האיפיון (2/4), ואינו נטען אוטומטית.
- `bug-fixing.agent.md` - **Custom Agent נפרד** לפתרון באגים. עוקב אחרי אותו תהליך מלא כמו Task Workflow, ובנוסף אחרי bug-fixing.instructions.md לחקירת שורש הבעיה לפני איפיון הפתרון. נבחר ידנית מתוך ה-agent picker ב-VS Code.

## איך זה מחובר

כל כלי AI שרוצה להשתמש בהנחיות האלו צריך "לשאוב" אותן מהקובץ כאן, במקום להעתיק את התוכן. כך יש מקור אמת יחיד.

לכל קובץ `.instructions.md` ברשימת ה"מבנה" למעלה יוצרים symlink/import נפרד, באותה שיטה:

### VS Code (GitHub Copilot)
Symlink מתיקיית ה-prompts האישית של VS Code אל כל קובץ כאן, למשל:

```
%APPDATA%\Code\User\prompts\github-workflow.instructions.md  -->  (symlink to) <clone-path>\github-workflow.instructions.md
```

### Claude Code
שורת import בתוך `~/.claude/CLAUDE.md`, אחת לכל קובץ:

```
@<clone-path>\github-workflow.instructions.md
@<clone-path>\task-workflow.instructions.md
@<clone-path>\progress-checklist.instructions.md
@<clone-path>\backlog-item-creation.instructions.md
@<clone-path>\development-standards.instructions.md
@<clone-path>\copilot-review-triage.instructions.md
```

## הגדרה במחשב חדש

1. שכפול הריפו:
   ```
   gh repo clone EsterBornshtein/my-ai-instructions <target-folder>
   ```
2. **VS Code**: יצירת symlink לכל קובץ (דורש הרשאות Admin או Developer Mode מופעל), למשל:
   ```
   mklink "%APPDATA%\Code\User\prompts\github-workflow.instructions.md" "<target-folder>\github-workflow.instructions.md"
   ```
   וכן הלאה לכל קובץ `.instructions.md` נוסף ברשימת ה"מבנה".
3. **Claude Code**: יצירת/עדכון `~/.claude/CLAUDE.md` עם שורת import לכל הקבצים, כמו למעלה.

## הוספת כלי AI נוסף (למשל Cursor, Windsurf וכו')

1. לברר מהו מיקום קובץ ההנחיות הגלובלי (user-level, לא project-level) של הכלי.
2. אם הכלי תומך ב-import/include בתוך קובץ ההנחיות שלו - להוסיף שורת הפניה לקובץ הרלוונטי כאן (כמו שנעשה ב-Claude Code).
3. אם הכלי לא תומך ב-import - ליצור symlink מהמיקום הגלובלי שלו אל הקובץ כאן (כמו שנעשה ב-VS Code).
4. לעדכן את הקובץ הזה (`README.md`) עם ההוראות הספציפיות לכלי החדש, כדי שיהיה תיעוד לפעם הבאה.

## הוספת הנחיה חדשה

אם רוצים הנחיות נוספות שלא קשורות ל-Git/GitHub, עדיף ליצור קובץ `.instructions.md` נפרד (עם `applyTo` מתאים), ולחבר אותו באותה שיטה (symlink / import) מכל כלי AI רלוונטי.
