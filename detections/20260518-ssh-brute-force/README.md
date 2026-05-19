# 01 · SSH Brute Force Detection

| Campo | Valor |
|---|---|
| **Fecha** | 2026-05-18 |
| **MITRE ATT&CK** | T1110.001 — Brute Force: Password Guessing |
| **Severidad** | Media |
| **Herramienta atacante** | Hydra |
| **Objetivo** | SSH service (target-lin) |
| **Detectado por** | Wazuh rule 5763 |
| **Estado** | 🔄 En progreso |

---

## Objetivo

Simular un ataque de fuerza bruta contra SSH y verificar que Wazuh lo detecta correctamente, analizar el log que dispara la alerta y documentar la respuesta sugerida.

---

## Setup

- Wazuh Agent activo en `target-lin`
- SSH habilitado en `target-lin`
- `hydra` disponible en `kali-attacker`
- Wordlist: `/usr/share/wordlists/rockyou.txt`

---

## Ataque

Ver [`attack.md`](./attack.md)

---

## Detección

Ver [`detection.md`](./detection.md)

---

## Análisis forense

*(por completar tras ejecutar el escenario)*

---

## Respuesta sugerida

1. Bloquear IP atacante vía `iptables` o en el firewall perimetral
2. Verificar si hubo autenticación exitosa posterior al brute force
3. Revisar `auth.log` completo del período
4. Rotar credenciales SSH si aplica
5. Considerar fail2ban o MFA para SSH

---

## Lecciones aprendidas

*(por completar)*
