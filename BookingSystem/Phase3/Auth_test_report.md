# Authorization Testing

---

## 🧑‍🦲 Guest

### ✅ Can Do
| Capability |
|-----------|
| Can access the main page `/` |
| Can register `/register` |
| Can see other reservations |
| Can access `/api/reservations` |
| ⚠️ Can access `/api/users` (Gobuster) |
| ⚠️ `/resources` Shouldn't be visible |
| ⚠️ `/api/resources` is visible (Gobuster) |
| ⚠️ `/api/reservations/{id}` reserver_token visible |

### ❌ Cannot Do
| Capability |
|-----------|
| Cannot login `/login` |
| Cannot add a resource `/resource` |
| Cannot add reservation `/reservation` |
| Cannot adjust existing reservations `/reservation?id={id}` |

---

## 🧑‍💼 Reserver

### ✅ Can Do
| Capability |
|-----------|
| Can access main page `/` |
| Can login `/login` |
| Can adjust own reservation `/resources` or `/reservation` |
| ⚠️ Can access `/api/reservations` (Gobuster) |
| ⚠️ Can access `/api/resources` (Gobuster) |
| ⚠️ Can access `/api/users` (Gobuster) |

### ❌ Cannot Do
| Capability |
|-----------|
| Cannot adjust others' `/reservations` |
| Cannot update or delete own reservations |
| Cannot edit or delete users |
| Cannot reach added resources |

---

## 🧑‍💼🛡️ Administrator

### ✅ Can Do
| Capability |
|-----------|
| Can access main page `/` |
| Can register and login `/register` - `/login` |
| Can add resources `/resources` |
| Can add reservations `/reservation` |
| Can see reservations and names `/` |
| Can delete and update all reservations `/reservations` |
| ⚠️ Can access `/api/users` |
| ⚠️ Can access `/api/resources` |
| ⚠️ Can access `/api/reservations` |
| ⚠️ Can access `/api/reservations/{id}` |

### ❌ Cannot Do
| Capability |
|-----------|
| Cannot access `/admin` |
| Cannot delete users |
| Cannot add new user |
| Cannot edit users |
| Cannot update or delete own reservations (API) |

---
