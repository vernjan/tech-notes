# PAM (Pluggable Authentication Modules)

- Instead of every application (like SSH, login, su, or sudo) having to write its own code to check passwords or verify users, they all
  outsource that job to PAM.
- PAM sits between applications and authentication providers (like your local password file, an LDAP server, or a fingerprint scanner).
- Configured in `/etc/pam.d/`
