# Module 2 — Users & Permissions → Access Control Models

> Part of: DevOps Mastery Roadmap — Phase 1 (Linux + OS + Networking)
> Learning mode: Basic → Intermediate → Advanced, in one continuous ladder
> Tags: **[OS]** = Operating Systems theory · **[CN]** = Networking · **[SEC]** = Security · **[PERF]** = Performance · **[DS/ALGO]** = Data Structures & Algorithms · **[DM]** = Discrete Math / Formal Models · **[SE]** = Software Engineering

---

## 0. How to use this file
This is a **topic map**, not a tutorial. For every leaf node:
1. Learn the concept (article/docs/man page).
2. Run the related command(s) yourself on a real Linux box/VM (use a throwaway VM: you will break things on purpose).
3. Write one line in your own words explaining "why this exists."
4. Check it off.

**Prerequisite:** Module 1 (filesystem hierarchy, inodes, /proc, syscalls). Permissions are metadata stored in the inode, and every permission check happens inside a syscall, so those two ideas carry straight into this module.

---

## 1. Mindmap Overview

```
MODULE 2: USERS & PERMISSIONS → ACCESS CONTROL MODELS
│
├── 1. Identity Model: Users & Groups                  [OS: process/file ownership]
│   ├── User types
│   │   ├── root (UID 0) — the superuser
│   │   ├── System accounts (daemons, low UIDs, nologin shells)
│   │   └── Regular users (UID >= 1000 on most distros)
│   ├── UID / GID ranges (/etc/login.defs)
│   ├── Primary group vs supplementary groups
│   ├── Identity files
│   │   ├── /etc/passwd  (name, x, UID, GID, GECOS, home, shell)
│   │   ├── /etc/shadow  (password hash + aging fields)
│   │   ├── /etc/group   (group name, GID, members)
│   │   ├── /etc/gshadow (group passwords/admins)
│   │   └── /etc/skel    (template for new home directories)
│   └── Inspection commands: id, whoami, groups, who, w, last, lastlog, getent
│
├── 2. User & Group Administration
│   ├── Create/modify/delete: useradd, adduser, usermod, userdel
│   ├── Group management: groupadd, groupmod, groupdel, gpasswd, newgrp
│   ├── Passwords: passwd, chage (aging, expiry, warning, inactivity)
│   ├── Shell & account control: chsh, /sbin/nologin, /bin/false
│   ├── Locking/unlocking accounts (usermod -L/-U, passwd -l/-u)
│   ├── System vs interactive accounts (useradd -r, -M, -s)
│   └── Editing safely: vipw, vigr (locking so files don't corrupt)
│
├── 3. Password Storage & Authentication Stack         [SEC][DS/ALGO]
│   ├── /etc/shadow field layout ($id$salt$hash)
│   ├── Hash algorithms: MD5 ($1$), SHA-256 ($5$), SHA-512 ($6$), yescrypt ($y$)
│   ├── Salting, work factor, why fast hashes are bad for passwords
│   ├── PAM (Pluggable Authentication Modules)
│   │   ├── Module types: auth, account, password, session
│   │   ├── Control flags: required, requisite, sufficient, optional
│   │   ├── /etc/pam.d/ service files
│   │   └── Useful modules: pam_unix, pam_pwquality, pam_faillock, pam_limits
│   ├── nsswitch.conf — where the system looks up users/groups
│   └── Password policy & lockout (complexity, history, failed-attempt lockout)
│
├── 4. The Permission Model (DAC basics)               [OS: file access control]
│   ├── Reading `ls -l`: file type, owner/group/other triplets
│   ├── rwx meaning on files vs directories
│   │   ├── File: read contents / modify contents / execute
│   │   └── Directory: list names / create-delete-rename entries / traverse (cd, access)
│   ├── Octal and symbolic notation (chmod 640, chmod u+x,g-w)
│   ├── Changing ownership: chown, chgrp (and recursive -R caution)
│   ├── umask — default permission mask for new files/dirs
│   ├── The permission check order (owner → group → other; first match wins)
│   └── Where the bits live: the inode's mode field (stat command)
│
├── 5. Special Permission Bits                         [OS][SEC]
│   ├── setuid (4xxx) — run as file owner (e.g. /usr/bin/passwd)
│   ├── setgid (2xxx) — run as file group / inherit group on directories
│   ├── sticky bit (1xxx) — only owner can delete in shared dirs (/tmp)
│   ├── Reading them in ls -l (s, S, t, T)
│   ├── Auditing: find / -perm -4000, -2000, -1000
│   └── Why setuid root binaries are a classic attack surface
│
├── 6. Process Credentials                             [OS: process identity]
│   ├── Real UID/GID vs Effective UID/GID vs Saved set-user-ID
│   ├── File-system UID (fsuid)
│   ├── How setuid changes the effective UID on exec
│   ├── Supplementary group list of a process
│   ├── Syscalls: setuid, seteuid, setresuid, getuid, geteuid
│   └── Inspecting credentials: /proc/<pid>/status (Uid:, Gid:, Groups:)
│
├── 7. Privilege Escalation Tools: su & sudo
│   ├── su vs su - (login shell, environment reset)
│   ├── sudo fundamentals
│   │   ├── /etc/sudoers and /etc/sudoers.d/ drop-ins
│   │   ├── visudo (syntax-checked editing)
│   │   ├── User/Host/Runas/Command specification syntax
│   │   ├── Aliases (User_Alias, Cmnd_Alias, Host_Alias, Runas_Alias)
│   │   ├── NOPASSWD, secure_path, env_reset, requiretty
│   │   ├── sudo -l, sudo -u, sudo -i, sudo -s, sudoedit
│   │   └── Logging: sudo I/O logs, auth log / journal entries
│   ├── Least-privilege sudo rules (allow specific commands, not ALL)
│   └── Common sudo pitfalls (shell escapes, wildcard abuse, editable scripts)
│
├── 8. Beyond rwx: ACLs & Extended Attributes          [OS][SEC]
│   ├── POSIX ACLs
│   │   ├── getfacl, setfacl (-m, -x, -b, -R)
│   │   ├── The ACL mask entry and how it limits permissions
│   │   └── Default ACLs on directories (inheritance for new files)
│   ├── Filesystem attributes: chattr / lsattr
│   │   ├── i — immutable
│   │   └── a — append-only
│   ├── Extended attributes (xattr): getfattr, setfattr
│   └── Filesystem mount options affecting access (noexec, nosuid, nodev, ro)
│
├── 9. Access Control Models (Theory)                  [SEC][DM]
│   ├── Principle of least privilege, separation of duties, defense in depth
│   ├── The access control matrix: subjects × objects × rights
│   │   ├── ACL = column view (per object)
│   │   └── Capability list = row view (per subject)
│   ├── DAC — Discretionary Access Control (classic Unix owner-decides)
│   ├── MAC — Mandatory Access Control (system-wide policy)
│   ├── RBAC — Role-Based Access Control (map to IAM roles in Phase 4)
│   ├── ABAC — Attribute-Based Access Control
│   ├── Multi-level security models (Bell-LaPadula, Biba) — conceptual, lattice-based
│   └── Authentication vs Authorization vs Accounting (AAA)
│
├── 10. Linux Capabilities                             [OS][SEC]
│   ├── Why: splitting root's power into ~40 separate privileges
│   ├── Key capabilities: CAP_NET_BIND_SERVICE, CAP_CHOWN, CAP_DAC_OVERRIDE,
│   │   CAP_KILL, CAP_SETUID, CAP_SYS_ADMIN, CAP_NET_ADMIN, CAP_SYS_PTRACE
│   ├── Capability sets: permitted, effective, inheritable, bounding, ambient
│   ├── File capabilities: setcap, getcap
│   ├── Process capabilities: capsh --print, /proc/<pid>/status (CapEff etc.), getpcaps
│   ├── How execve combines file + process capabilities
│   └── Why containers drop capabilities (tie to Module 7 & Docker --cap-drop)
│
├── 11. Mandatory Access Control in Practice           [SEC][OS]
│   ├── SELinux
│   │   ├── Modes: enforcing, permissive, disabled
│   │   ├── Security contexts: user:role:type:level
│   │   ├── Type Enforcement and policy rules
│   │   ├── Tools: getenforce, setenforce, sestatus, ls -Z, ps -Z, id -Z
│   │   ├── Fixing labels: restorecon, chcon, semanage fcontext
│   │   ├── Booleans: getsebool, setsebool
│   │   └── Troubleshooting denials: ausearch, audit2why, audit2allow
│   ├── AppArmor
│   │   ├── Path-based profiles, enforce vs complain mode
│   │   └── Tools: aa-status, aa-enforce, aa-complain, aa-genprof
│   └── SELinux vs AppArmor comparison (model, default distros, complexity)
│
├── 12. Centralized Identity (Awareness Level)         [CN][SEC]
│   ├── Why local /etc/passwd doesn't scale beyond a few servers
│   ├── LDAP (directory protocol over the network)
│   ├── Kerberos (ticket-based authentication, KDC)
│   ├── SSSD and nsswitch integration
│   └── How this connects to cloud IAM and SSO in Phase 4
│
├── 13. Auditing & Hardening Habits                    [SEC]
│   ├── Log locations: /var/log/auth.log (Debian) or /var/log/secure (RHEL), journalctl
│   ├── auditd basics: auditctl, ausearch, aureport, /etc/audit/rules.d/
│   ├── Hunting risky files: world-writable, unowned, SUID/SGID, empty passwords
│   ├── Locking down root: disable direct root login, sudo-only administration
│   ├── Account hygiene: expiring accounts, removing unused users, checking UID 0 duplicates
│   └── Failed-login defence: pam_faillock / fail2ban (awareness; SSH hardening is Module 9)
│
├── 14. Tie-Backs to Containers & Orchestration        [OS][SEC][SE]
│   ├── Dockerfile USER instruction and running as non-root
│   ├── Container UID mapping and user namespaces (preview of Module 7)
│   ├── Kubernetes securityContext: runAsUser, runAsNonRoot, capabilities, readOnlyRootFilesystem
│   └── CI/CD runners and service accounts as least-privilege identities
│
└── 15. Module 2 Capstone Checkpoint
    ├── Task: Build a multi-user shared project directory (setgid + sticky bit + ACLs) where team members can collaborate but not delete each other's files
    ├── Task: Write a sudoers drop-in giving one user permission to restart exactly one service and nothing else
    ├── Task: Audit a VM for all SUID/SGID binaries and world-writable files, and justify each SUID binary you find
    ├── Task: Give a non-root web server permission to bind port 80 using file capabilities instead of root
    └── Task: Put a service into SELinux or AppArmor complain mode, trigger a denial, and read/explain the log entry
```

---

## 2. Detailed Topic Table (Basic → Intermediate → Advanced)

| # | Topic | Level | Tag | Key Commands / Files |
|---|-------|-------|-----|----------------------|
| 1 | Users, groups, UID/GID, root vs regular vs system accounts | Basic | [OS] | `id, whoami, groups, getent passwd` |
| 2 | Identity files (passwd, shadow, group) | Basic | [OS] | `/etc/passwd`, `/etc/shadow`, `/etc/group` |
| 3 | Creating and managing users/groups | Basic | — | `useradd, usermod, userdel, groupadd, gpasswd` |
| 4 | Password aging and account locking | Basic/Intermediate | [SEC] | `passwd, chage, usermod -L` |
| 5 | Reading permissions and octal/symbolic chmod | Basic | [OS] | `ls -l, chmod 640, chmod u+x` |
| 6 | Ownership changes | Basic | [OS] | `chown, chgrp` |
| 7 | rwx semantics on files vs directories | Basic/Intermediate | [OS] | `ls -ld, stat` |
| 8 | umask and default permissions | Intermediate | [OS] | `umask` |
| 9 | Permission bits live in the inode | Intermediate | [OS][DS/ALGO] | `stat, ls -i` |
| 10 | setuid, setgid, sticky bit | Intermediate | [OS][SEC] | `chmod 4755, 2775, 1777` |
| 11 | Auditing special-permission files | Intermediate | [SEC] | `find / -perm -4000 2>/dev/null` |
| 12 | su vs su - vs sudo | Basic/Intermediate | [SEC] | `su -, sudo -i, sudo -l` |
| 13 | Writing safe sudoers rules | Intermediate/Advanced | [SEC] | `visudo, /etc/sudoers.d/` |
| 14 | Password hashing, salting, hash algorithms | Intermediate | [SEC][DS/ALGO] | `/etc/shadow`, `mkpasswd`, `openssl passwd` |
| 15 | PAM architecture and configuration | Advanced | [SEC][SE] | `/etc/pam.d/*`, `pam_faillock` |
| 16 | nsswitch and user lookup order | Intermediate | [CN] | `/etc/nsswitch.conf, getent` |
| 17 | Real vs effective vs saved UID | Advanced | [OS] | `/proc/<pid>/status`, `ps -o ruid,euid` |
| 18 | POSIX ACLs and mask | Advanced | [OS][SEC] | `getfacl, setfacl` |
| 19 | chattr immutable/append-only, xattrs | Intermediate/Advanced | [OS][SEC] | `chattr +i, lsattr, getfattr` |
| 20 | Mount options: noexec, nosuid, nodev | Intermediate | [OS][SEC] | `mount, /etc/fstab` |
| 21 | Access control matrix, ACL vs capability lists | Advanced | [SEC][DM] | conceptual |
| 22 | DAC vs MAC vs RBAC vs ABAC | Advanced | [SEC] | conceptual |
| 23 | Bell-LaPadula / Biba (lattice models) | Advanced | [SEC][DM] | conceptual |
| 24 | Linux capabilities and capability sets | Advanced | [OS][SEC] | `getcap, setcap, capsh --print` |
| 25 | SELinux contexts, modes, booleans, troubleshooting | Advanced | [SEC][OS] | `sestatus, ls -Z, restorecon, audit2why` |
| 26 | AppArmor profiles and modes | Advanced | [SEC][OS] | `aa-status, aa-complain` |
| 27 | LDAP / Kerberos / SSSD (awareness) | Advanced | [CN][SEC] | `sssd, getent, klist` |
| 28 | auditd and log-based accountability | Advanced | [SEC] | `auditctl, ausearch, aureport` |
| 29 | Account hygiene and hardening checklist | Intermediate/Advanced | [SEC] | `awk -F: '$3==0' /etc/passwd` |
| 30 | Non-root containers and K8s securityContext (preview) | Advanced | [OS][SEC][SE] | `USER` in Dockerfile, `runAsNonRoot` |

---

## 3. Concept Deep-Dive Questions (fill in as you learn)

### 3.1 Identity & Authentication
- [ ] Why does /etc/passwd contain an `x` in the password field, and where did the hash go?
- [ ] Why is a salted, slow hash (SHA-512/yescrypt) safer than plain MD5 for passwords? **[SEC][DS/ALGO]**
- [ ] What is the difference between the `auth`, `account`, `password` and `session` PAM module types?
- [ ] What decides whether the system checks local files or LDAP first for a username?

### 3.2 Permission Semantics
- [ ] Why does deleting a file depend on the *directory's* write permission and not the file's?
- [ ] What does `x` on a directory mean, and why can you have `r` without `x` and still be locked out?
- [ ] Where exactly are permission bits stored, and which syscall checks them? **[OS]**
- [ ] How does umask 022 turn into 644 for a new file and 755 for a new directory?

### 3.3 Special Bits & Process Identity
- [ ] How does a normal user change their own password when /etc/shadow is root-only? (Trace real vs effective UID.) **[OS]**
- [ ] Why is the sticky bit needed on /tmp, and what would happen without it?
- [ ] Why do setuid shell scripts get ignored on Linux?
- [ ] What is the saved set-user-ID for, and when would a program use it?

### 3.4 sudo & Least Privilege
- [ ] Why is `user ALL=(ALL) NOPASSWD: ALL` dangerous even on a "trusted" machine?
- [ ] How can allowing `sudo vim` or `sudo less` turn into a full root shell?
- [ ] What does `secure_path` protect against?

### 3.5 Models & Capabilities
- [ ] In an access control matrix, what is the difference between an ACL and a capability list? **[SEC][DM]**
- [ ] Why can DAC never stop a compromised process from leaking its owner's own files, and how does MAC fix that? **[SEC]**
- [ ] Which single capability lets a process bind to port 80, and why is that safer than running as root? **[OS][SEC]**
- [ ] Why is CAP_SYS_ADMIN called "the new root"?
- [ ] What is the difference between SELinux's label-based model and AppArmor's path-based model?

### 3.6 Tie-Back Questions
- [ ] Which Linux permission concepts appear again in Kubernetes securityContext fields?
- [ ] How does the RBAC model here compare to AWS IAM roles you'll meet in Phase 4?

---

## 4. Capstone Checklist
- [ ] Built a shared team directory using setgid + sticky bit + default ACLs, and proved the behaviour with two test users
- [ ] Wrote a least-privilege sudoers drop-in (one user, one command) and validated it with `visudo -c`
- [ ] Audited SUID/SGID and world-writable files and documented why each SUID binary exists
- [ ] Bound a non-root service to port 80 using file capabilities, and verified with `getcap` and `/proc/<pid>/status`
- [ ] Triggered and interpreted an SELinux or AppArmor denial in complain mode
- [ ] Traced real vs effective UID of `passwd` while it runs, using `/proc/<pid>/status`
- [ ] One-paragraph summary, in your own words: "When a process tries to open a file, what checks does Linux run, in what order, and which of those checks can override the plain rwx bits?"

---

## 5. Portability Note
This file is self-contained and reusable: upload it into any fresh Claude conversation that has a topic-map teaching skill installed and ask it to teach Module 2 from this file, one section at a time, to reproduce this curriculum with consistent depth regardless of prior chat history.
