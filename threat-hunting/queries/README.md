# Threat Hunting Queries

Queries reutilizables para threat hunting en Wazuh / Kibana / OpenSearch.

---

## Convención de nombres

```
[plataforma]-[tecnica]-[descripcion].md
```

Ejemplos: `wazuh-T1110-ssh-brute-force.md`, `kql-T1059-powershell-exec.md`

---

## Queries disponibles

| Archivo | Plataforma | TTP | Descripción |
|---|---|---|---|
| *(próximamente)* | — | — | — |

---

## Template de query

```markdown
## Query: [Nombre]
**Plataforma:** Wazuh / KQL / OpenSearch DSL
**MITRE:** T[ID] — [Nombre]
**Objetivo:** Detectar [comportamiento]

### Query
[query aquí]

### Interpretación
[qué significa cada campo]

### Falsos positivos conocidos
[qué puede generar ruido]
```
