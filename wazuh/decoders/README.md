# Custom Decoders

Decoders personalizados para parsear logs de herramientas o formatos no soportados por defecto en Wazuh.

---

## Convención de nombres

```
local_decoder_[nombre-herramienta].xml
```

---

## Decoders disponibles

| Archivo | Fuente de log | Descripción |
|---|---|---|
| *(próximamente)* | — | — |

---

## Cómo cargar un decoder en Wazuh

```bash
sudo cp local_decoder_*.xml /var/ossec/etc/decoders/
sudo systemctl restart wazuh-manager
```

## Referencias
- [Wazuh Decoder Syntax](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/decoders.html)
