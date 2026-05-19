# Detection — SSH Brute Force

---

## Alerta generada en Wazuh

| Campo | Valor |
|---|---|
| **Rule ID** | 5763 |
| **Nivel** | 10 |
| **Descripción** | sshd: brute force trying to get access to the system |
| **Grupo** | authentication_failures, sshd |
| **MITRE** | T1110 |

---

## Log raw que disparó la regla

```
Dec 18 10:23:45 target-lin sshd[1234]: Failed password for ubuntu from attacker-ip port 54321 ssh2
Dec 18 10:23:46 target-lin sshd[1234]: Failed password for ubuntu from attacker-ip port 54322 ssh2
Dec 18 10:23:47 target-lin sshd[1234]: Failed password for ubuntu from attacker-ip port 54323 ssh2
...
```

---

## Regla de Wazuh que disparó

```xml
<rule id="5763" level="10" frequency="8" timeframe="120">
  <if_matched_sid>5760</if_matched_sid>
  <description>sshd: brute force trying to get access to the system.</description>
  <same_source_ip/>
  <mitre>
    <id>T1110</id>
  </mitre>
  <group>authentication_failures,pci_dss_11.4,gdpr_IV_35.7.d,</group>
</rule>
```

> Dispara cuando detecta 8+ intentos fallidos de la misma IP en 120 segundos.

---

## Análisis

*(completar tras ejecutar el escenario — capturas en /screenshots)*

---

## ¿Se pudo mejorar la detección?

*(notas sobre ajuste de reglas o umbrales)*
