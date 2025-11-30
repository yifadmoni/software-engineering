graph TD
    subgraph "רכב / נהג"
        A[הגעה לשער הכניסה]
        I[לקיחת כרטיס וכניסה לחניון]
    end

    subgraph "תחנת כניסה (חומרה - מצלמה, חיישנים, שער)"
        B[זיהוי נוכחות רכב וצילום לוחית רישוי]
        H[הדפסת כרטיס חניה ופתיחת שער]
        J[זיהוי מעבר רכב מלא ע''י חיישנים]
        K[סגירת שער אוטומטית]
    end

    subgraph "תחנת כניסה (בקר מקומי)"
        C[עיבוד תמונה וחילוץ מספר לוחית רישוי]
        D[שליחת בקשת כניסה למחשב המרכזי]
        G{האם התקבל אישור?}
        G -- כן --> H
        G -- לא --> L[הצגת הודעת 'חניון מלא' על המסך]
    end

    subgraph "מחשב מרכזי (שרת)"
        E{בדיקת תפוסה: האם יש מקום פנוי?}
        E -- כן (יש מקום) --> F[יצירת רשומת כניסה, עדכון מונה תפוסה (+1), ושליחת אישור]
        E -- לא (חניון מלא) --> M[שליחת הודעת דחייה 'חניון מלא']
    end

    %% זרימת התהליך
    A --> B
    B --> C
    C --> D
    D --> E
    F --> G
    M --> G
    I --> J
    J --> K

    %% סיום תהליכים
    K --> N((סיום תהליך כניסה מוצלח))
    L --> O((סיום - כניסה נדחתה))

    %% עיצוב הצמתים
    classDef startEnd fill:#f9f,stroke:#333,stroke-width:2px;
    classDef process fill:#d4edda,stroke:#28a745,stroke-width:1px;
    classDef decision fill:#fff3cd,stroke:#ffc107,stroke-width:1px;

    class A,N,O startEnd;
    class B,C,D,F,H,I,J,K,L,M process;
    class E,G decision;

    %% עיצוב ה-Subgraphs
    style "רכב / נהג" fill:#e9ecef,stroke:#6c757d
    style "תחנת כניסה (חומרה - מצלמה, חיישנים, שער)" fill:#e2e6ea,stroke:#6c757d
    style "תחנת כניסה (בקר מקומי)" fill:#dee2e6,stroke:#6c757d
    style "מחשב מרכזי (שרת)" fill:#ced4da,stroke:#6c757d
