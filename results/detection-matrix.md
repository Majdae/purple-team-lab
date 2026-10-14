# Matrice de détection

| Scénario / Technique | Trace locale (Sysmon / Windows) | Remontée Wazuh | Niveau de détection |
|---|---|---|---|
| Modify Registry (T1112) | Oui (Sysmon 12/13) | Oui | Bon |
| Registry Run Key (T1547.001) | Oui (Sysmon 13) | Oui | Bon |
| RDP, Logon Type 10 (T1021.001) | Oui (Event 4624) | Oui | Moyen (manque de règles personnalisées) |
| Scheduled Task (T1053.005) | Oui (Event 4698 / Sysmon 1) | Oui | Bon |
| PowerShell (T1059.001) | Oui (Sysmon 1) | En cours d'ajustement | À optimiser |

## Lacunes
- Volumétrie : les journaux natifs génèrent beaucoup de bruit.
- PowerShell encodé/obfusqué : activer le Script Block Logging (Event 4104).

## Perspectives
Étendre le nombre de nœuds et de scénarios (limité ici par les ressources
matérielles de la virtualisation).