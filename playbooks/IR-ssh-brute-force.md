# IR Playbook — SSH Brute Force

**Trigger:** Wazuh rule 5763 — nivel 10+  
**MITRE:** T1110.001  
**Tiempo estimado de respuesta:** 15–30 min

---

## Fase 1 — Identificación

- [ ] Confirmar alerta en Wazuh dashboard
- [ ] Identificar IP origen del ataque
- [ ] Determinar usuario/s objetivo
- [ ] Verificar si hubo autenticación exitosa (`Accepted password` en auth.log)

```bash
# Buscar autenticaciones exitosas desde la IP atacante
grep "Accepted" /var/log/auth.log | grep <attacker-ip>

# Ver todos los intentos fallidos
grep "Failed password" /var/log/auth.log | grep <attacker-ip> | wc -l
```

---

## Fase 2 — Contención

- [ ] Bloquear IP atacante

```bash
sudo iptables -A INPUT -s <attacker-ip> -j DROP
# O con ufw:
sudo ufw deny from <attacker-ip>
```

- [ ] Si hubo acceso exitoso: aislar el sistema inmediatamente
- [ ] Preservar logs antes de cualquier acción adicional

---

## Fase 3 — Erradicación

- [ ] Verificar no hay sesiones activas del atacante (`who`, `w`, `last`)
- [ ] Revisar crontabs y servicios por backdoors
- [ ] Cambiar contraseñas de cuentas objetivo
- [ ] Considerar deshabilitar autenticación por password en SSH

```bash
# /etc/ssh/sshd_config
PasswordAuthentication no
PermitRootLogin no
```

---

## Fase 4 — Recuperación

- [ ] Restaurar desde snapshot limpio si hubo compromiso
- [ ] Verificar integridad de archivos críticos (Wazuh FIM)
- [ ] Confirmar que el servicio SSH responde correctamente

---

## Fase 5 — Lecciones aprendidas

- [ ] Documentar timeline completo
- [ ] Ajustar umbrales de regla si hubo falsos positivos
- [ ] Evaluar implementar fail2ban o MFA
