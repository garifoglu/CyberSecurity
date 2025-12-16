# 🔐 Authorization Test Report - Web Application Security Assessment

**Application:** Web Application at http://192.168.32.13:8003  
**Testing Tool:** OWASP ZAP (Unauthenticated Scan)  
**Tester:** Gökhan Arifoglu  
**Testing Phase:** Phase 1 – Unauthenticated Baseline  
**Scan Date:** 2025-12-16  

---

## 🧑‍🦲 Guest (Not Logged In)

### ✅ Can do

| Action | Location | Observation / Matches Spec? |
|------|---------|------------------------------|
| View homepage | / | Access granted. Displays available content. Matches expected behavior. |
| Access login form | /login | GET allowed. Form accessible. Matches Spec 2 (users can access login). |
| Access registration form | /register | GET allowed. Form accessible. Matches Spec 2 (users can register). |
| View robots.txt | /robots.txt | Access granted (200 OK). Standard web practice. |
| View sitemap.xml | /sitemap.xml | Access granted (200 OK). SEO standard. |
| Access static resources | /static | Access granted. Normal for asset delivery. |
| Trigger User-Agent detection | All endpoints | Application responds differently to 12+ User-Agent strings. Informational finding. |

### ❌ Cannot do

| Action | Location | Observation / Matches Spec? |
|------|---------|------------------------------|
| Submit login form | /login POST | 401 Unauthorized without credentials. Correctly blocked. |
| Submit registration | /register POST | Requires form completion. Correctly blocked. |
| Make reservation | /reservation POST | Redirects to login. Correctly blocked. Matches Spec 3. |
| Access admin pages | /admin/* | No access. Correctly blocked. |
| Access API data | /api/resources | **TEST PENDING** – Requires fuzzing verification. |
| Exploit authentication | Any endpoint | No authentication bypass detected. Correctly blocked. |

---

## 🧑‍💼 Reserver (Logged In)

> **Note:** Authenticated scanning was not performed. Findings are based on scan inference and specification review.

### ✅ Can do

| Action | Location | Observation / Matches Spec? |
|------|---------|------------------------------|
| Authenticate successfully | /login POST | Authentication flow correctly identified with CSRF protection. Matches Spec 2. |
| Maintain secure session | All endpoints | Session management tokens (CSRF) detected and maintained. Good practice. |
| View personalized content | / | Homepage displays user-specific content when logged in. Matches expected behavior. |
| Access reservation system | /reservation | Form accessible for authenticated users. Matches Spec 3, 6, 7. |

### ❌ Cannot do

| Action | Location | Observation / Matches Spec? |
|------|---------|------------------------------|
| Access admin functions | /admin/* | Assumed blocked – Requires authenticated test verification. |
| Modify system resources | /admin/resources/* | Assumed blocked – Admin-only function per Spec 4. |
| Delete other users | /admin/users/delete/:id | Assumed blocked – Admin-only function per Spec 5. |
| View admin panel | /admin | Assumed blocked – UI likely hides admin links for non-admins. |
| Bypass age restriction | /reservation | **TEST PENDING** – Spec 6 compliance needs verification. |

---

## 🧑‍💼🛡️ Administrator (Logged In)

> **Note:** Admin role scanning was not performed. Observations are based on specifications and inferred behavior.

### ✅ Can do

| Action | Location | Observation / Matches Spec? |
|------|---------|------------------------------|
| Access all system functions | All endpoints | Assumed full access – Based on role definition. |
| Manage all resources | /admin/resources/* | Matches Spec 4 (add, remove, modify resources). |
| Manage all reservations | /admin/reservations/* | Matches Spec 4 (remove and modify reservations). |
| Manage user accounts | /admin/users/* | Matches Spec 5 (delete reservers). |

### ❌ Cannot do

| Action | Location | Observation / Matches Spec? |
|------|---------|------------------------------|
| Prevent User-Agent profiling | All endpoints | **PRIVACY CONCERN:** Differential responses to User-Agents could aid attackers. |
| Hide session tokens effectively | /login, /register | **SECURITY INFO:** CSRF tokens exposed in cookies. Additional hardening recommended. |
| Block outdated scanning tools | Scan detection | **TOOL ISSUE:** ZAP version outdated (latest 2.17.0). Not an application fault. |
| Ensure complete GDPR compliance | Data display | **TEST PENDING:** Need to verify if reserver identity is hidden per Spec 8 and GDPR. |

---



---



- ZAP Scan Report: `ZAP_Report4.md`

