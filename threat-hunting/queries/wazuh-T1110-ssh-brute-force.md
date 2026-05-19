# Query: SSH Brute Force Hunting

**Plataforma:** Wazuh / OpenSearch Dashboards  
**MITRE:** T1110.001 — Brute Force: Password Guessing  
**Objetivo:** Identificar fuentes de brute force SSH activas o históricas

---

## Query — OpenSearch (KQL)

```
rule.id: 5760 OR rule.id: 5763 AND agent.name: *
```

Filtra por las últimas 24h y agrupa por `data.srcip` para ver las IPs con más intentos.

---

## Query — Wazuh API

```bash
# Top IPs con más intentos fallidos SSH
curl -k -u admin:admin \
  "https://wazuh-manager:55000/security/events" \
  -G --data-urlencode "q=rule.id=5763" \
  | python3 -m json.tool
```

---

## Query — auth.log directo

```bash
# Intentos fallidos agrupados por IP
grep "Failed password" /var/log/auth.log \
  | awk '{print $11}' \
  | sort | uniq -c | sort -rn | head -20

# Verificar si alguna IP tuvo éxito después de fallos
grep -E "(Failed|Accepted) password" /var/log/auth.log \
  | grep <suspicious-ip>
```

---

## Interpretación

- Más de 10 intentos desde la misma IP en < 2 min = brute force
- Si aparece `Accepted password` después de múltiples fallos = credenciales comprometidas
- Intentos en horario inusual (madrugada) = mayor riesgo

---

## Falsos positivos conocidos

- Scripts de backup que usan SSH con auth key incorrecta
- Herramientas de monitoreo mal configuradas
- Administradores que olvidaron actualizar credenciales en scripts
