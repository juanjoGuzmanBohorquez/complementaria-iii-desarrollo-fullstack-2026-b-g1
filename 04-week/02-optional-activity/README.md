📊 Smart Attendance Management System - CORHUILA

📌 Overview

This mobile-web application is designed so that both teachers and students can easily track class attendance in real-time. Teachers can log into the system to manage their assigned subjects and record student attendance digitally. Meanwhile, students can monitor their accumulated absences and overall academic status for each course. Furthermore, the system triggers proactive warning alerts to prevent students from exceeding the critical 30% absence limit, helping them avoid failing the subject. To fetch class and student records dynamically, the application consumes a public REST API (JSONPlaceholder) using JavaScript's native fetch() method. Finally, the user interface robustly handles all three application states: displaying a loading spinner during data retrieval, rendering the student list upon success, and showing an error message with a retry option if the network request fails.

🚀 Key Features

👨‍🏫 Teacher View: Class list management and digital attendance logging.

👨‍🎓 Student View: Attendance tracking with dynamic progress bars.

⚠️ Smart Alerts: Prevention notifications at 20%, 25%, and critical warning at 30%.

🔄 API Integration: Asynchronous data fetching with complete UI state management (Loading, Success, Error).
