# My AI Instructions

ריפו פרטי המכיל הנחיות אישיות לכלי AI (GitHub Copilot, Claude Code וכו'), החלות על כל הפרויקטים שלי - לא רק פרויקט ספציפי אחד.

## מבנה

- `github-workflow.instructions.md` - הנחיות להתנהגות בכל הנוגע ל-Git/GitHub (commits, branches, PRs).

## איך זה מחובר

כל כלי AI שרוצה להשתמש בהנחיות האלו צריך "לשאוב" אותן מהקובץ כאן, במקום להעתיק את התוכן. כך יש מקור אמת יחיד.

### VS Code (GitHub Copilot)
Symlink מתיקיית ה-prompts האישית של VS Code אל הקובץ כאן:

```
%APPDATA%\Code\User\prompts\github-workflow.instructions.md  -->  (symlink to) <clone-path>\github-workflow.instructions.md
```

### Claude Code
שורת import בתוך `~/.claude/CLAUDE.md`:

```
@<clone-path>\github-workflow.instructions.md
```

## הגדרה במחשב חדש

1. שכפול הריפו:
   ```
   gh repo clone EsterBornshtein/my-ai-instructions <target-folder>
   ```
2. **VS Code**: יצירת symlink (דורש הרשאות Admin או Developer Mode מופעל):
   ```
   mklink "%APPDATA%\Code\User\prompts\github-workflow.instructions.md" "<target-folder>\github-workflow.instructions.md"
   ```
3. **Claude Code**: יצירת/עדכון `~/.claude/CLAUDE.md` עם שורת ה-import שלמעלה.

## הוספת כלי AI נוסף (למשל Cursor, Windsurf וכו')

1. לברר מהו מיקום קובץ ההנחיות הגלובלי (user-level, לא project-level) של הכלי.
2. אם הכלי תומך ב-import/include בתוך קובץ ההנחיות שלו - להוסיף שורת הפניה לקובץ הרלוונטי כאן (כמו שנעשה ב-Claude Code).
3. אם הכלי לא תומך ב-import - ליצור symlink מהמיקום הגלובלי שלו אל הקובץ כאן (כמו שנעשה ב-VS Code).
4. לעדכן את הקובץ הזה (`README.md`) עם ההוראות הספציפיות לכלי החדש, כדי שיהיה תיעוד לפעם הבאה.

## הוספת הנחיה חדשה

אם רוצים הנחיות נוספות שלא קשורות ל-Git/GitHub, עדיף ליצור קובץ `.instructions.md` נפרד (עם `applyTo` מתאים), ולחבר אותו באותה שיטה (symlink / import) מכל כלי AI רלוונטי.
