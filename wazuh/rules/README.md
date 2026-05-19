# Custom Detection Rules

Reglas de detección personalizadas desarrolladas durante los escenarios del lab.

Cada regla incluye:
- **ID** en el rango `100000+` (reservado para reglas custom)
- **Descripción** de qué detecta
- **Nivel** de severidad (1–15)
- **Contexto** del escenario donde se creó

---

## Convención de nombres

```
local_rules_YYYYMMDD_[nombre-escenario].xml
```

---

## Reglas disponibles

| Archivo | Escenario | TTP |
|---|---|---|
| *(próximamente)* | — | — |

---

## Cómo cargar una regla en Wazuh

```bash
# Copiar al directorio de reglas custom
sudo cp local_rules_*.xml /var/ossec/etc/rules/

# Verificar sintaxis
sudo /var/ossec/bin/wazuh-logtest

# Reiniciar manager
sudo systemctl restart wazuh-manager
```
