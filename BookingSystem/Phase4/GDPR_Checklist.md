# GDPR Compliance Checklist – Web-based Booking System

| **Section Title**                           | **Question**                                                                                |  **Result**  |
| ------------------------------------------- | ------------------------------------------------------------------------------------------- | :----------: |
| **Personal data mapping and minimization**  | Have all personal data collected and processed been identified?                             |    ✅ YES    |
|                                             | Have you ensured that only necessary personal data is collected (data minimization)?        |    ✅ YES    |
|                                             | Is user age recorded to verify that the booker is over 15 years old?                        |    ✅ YES    |
| **User registration and management**        | Does the registration form include GDPR-compliant consent for data processing?              |    ❌ NO    |
|                                             | Can users view, edit, and delete their own personal data?                                   |    ✅ YES    |
|                                             | Is there a mechanism for the administrator to delete a reserver (right to be forgotten)?    |    ✅ YES    |
|                                             | Is underage registration (under 15 years) and booking functionality restricted?             |    ✅ YES    |
| **Booking visibility**                      | Are bookings visible to non-logged-in users only at resource level (without personal data)? |    ✅ YES    |
|                                             | Is personal data of bookers hidden from unauthorized users?                                 |    ❌ NO    |
| **Access control and authorization**        | Can only administrators add, modify, and delete resources and bookings?                     |    ✅ YES    |
|                                             | Is role-based access control implemented (e.g., user vs administrator)?                     |    ✅ YES    |
|                                             | Are administrator privileges limited and not exposed for unauthorized use?                  |    ❌ NO    |
| **Privacy by Design principles**            | Is Privacy by Default implemented (minimum data collected by default)?                      |    ✅ YES    |
|                                             | Are logs implemented without storing excessive personal data?                               |    ✅ YES    |
|                                             | Are forms and system components designed with data protection in mind?                      |    ❌ NO    |
| **Data security**                           | Are CSRF, XSS, and SQL injection protections implemented?                                   |    ❌ NO    |
|                                             | Are passwords securely hashed using strong algorithms (e.g., bcrypt, Argon2)?               |    ✅ YES    |
|                                             | Are data backup and recovery processes GDPR-compliant?                                      |    ⚠️ SOS |
|                                             | Is personal data stored in data centers located within the EU?                              |    ⚠️ SOS |
| **Data anonymization and pseudonymization** | Is pseudonymization used where appropriate to protect personal data?                        |    ❌ NO    |
| **Data subject rights**                     | Can users download or request all personal data related to them?                            |    ❌ NO    |
|                                             | Is there an interface or process for users to request deletion of their personal data?      |    ❌ NO    |
|                                             | Can users withdraw their consent for data processing?                                       |    ❌ NO    |
| **Documentation and communication**         | Is a privacy policy available during registration and easily accessible?                    |    ❌ NO    |
|                                             | Are administrators and developers provided with documented data protection practices?       |    ❌ NO    |
|                                             | Is there a documented data breach response process?                                         |    ❌ NO    |

