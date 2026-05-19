# Network Setup

Documentación del entorno de laboratorio: configuración de red, VMs y herramientas base.

---

## Topología

| Hostname | OS | Rol | VLAN |
|---|---|---|---|
| `kali-attacker` | Kali Linux Rolling | Attacker — Red Team | lab-vlan |
| `target-win` | Windows 10 Eval | Víctima Windows + Wazuh Agent | lab-vlan |
| `target-lin` | Ubuntu Desktop 22.04 | Víctima Linux + Wazuh Agent | lab-vlan |
| `wazuh-manager` | Ubuntu Server 22.04 | SIEM / SOC Core | lab-vlan |

Todas las VMs corren en red aislada (host-only / NAT interno) sin acceso directo a internet desde las víctimas.

---

## Hipervisor

- **Plataforma:** VirtualBox / VMware Workstation
- **Red:** Host-only adapter (aislado) para tráfico de lab
- **Snapshots:** Cada VM tiene snapshot limpio pre-ataque para restaurar entre escenarios

---

## Wazuh Manager — Setup

```bash
# Instalación via script oficial
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash ./wazuh-install.sh -a

# Verificar servicio
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-dashboard
```

Dashboard: `https://wazuh-manager:443`

---

## Wazuh Agents

### Linux (Ubuntu Desktop)
```bash
# Descargar e instalar agente
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.0-1_amd64.deb
sudo WAZUH_MANAGER='wazuh-manager' dpkg -i ./wazuh-agent_4.7.0-1_amd64.deb
sudo systemctl enable wazuh-agent && sudo systemctl start wazuh-agent
```

### Windows (PowerShell como Admin)
```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.0-1.msi -OutFile wazuh-agent.msi
msiexec.exe /i wazuh-agent.msi /q WAZUH_MANAGER="wazuh-manager"
NET START WazuhSvc
```

---

## Herramientas adicionales instaladas

### En víctima Windows
- [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) con config SwiftOnSecurity
- PowerShell Script Block Logging habilitado

### En víctima Linux
- `auditd` configurado
- `osquery` instalado

---

## Referencias
- [Wazuh Installation Guide](https://documentation.wazuh.com/current/installation-guide/index.html)
- [Sysmon Config - SwiftOnSecurity](https://github.com/SwiftOnSecurity/sysmon-config)
