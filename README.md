# ML-2-test
New randomforest ML pipeline specifically designed to predict whether students form a specific will withdraw/dropout.

Trained on 1130 students records. ML-test2 has better NaN handling with generic functions that handle filtering and filling. Also includes missing flag generator function which was really handy as this data was alot less consistent.

Uses 12(raw) + 7(extracted) Features extracted from schools general faculty report:
    numeric_features = ['Past Units Incomplete', 'attendance_converted', 'days_since_last_online']
    string_features = ['Student Group Code', 'Passed Last Unit', 'Manager', 'Teachers', 'Course Code', 'Course Title', 'RAG Rating', 'Location', 'Faculty' ]

engineered features:
- attendance_converted(int)
- Attendance_mising(int)
- Credit Ratio(int)
- Current Missing(int)
- Target Mising(int)
- last_online_missing(int)
- days_since_last_online(int)

Check .md file for exact model stats, in general it works pretty well! prototyping the pipelines general workflow was really handy, the added functions also are very convinient and worth stealing for future projects.
