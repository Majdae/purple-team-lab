# Purple Team Lab: Active Directory, Sysmon, Wazuh & MITRE ATT&CK

Laboratoire virtuel isolé pour simuler des techniques d'attaque Windows
et évaluer les capacités de détection d'un SOC.

> Projet de fin d'année, ENSIASD (Sécurité IT et Confiance Numérique), 2026/2027.

## Objectif
Mesurer ce qu'un SIEM détecte réellement, identifier les lacunes de
détection et proposer des améliorations des règles.

## Architecture
- **DC1**: contrôleur de domaine Active Directory (Windows Server)
- **PC1**: poste Windows 10/11 ciblé par les scénarios (Sysmon + agent Wazuh)
- **Wazuh Server**: SIEM/XDR hébergé sur une VM Linux
- **Kali Linux**: machine d'attaque (optionnelle)
- **VirtualBox**: réseau isolé, snapshots restaurés après chaque simulation

## Flux de collecte des logs
1. Les événements Windows et Sysmon sont enregistrés localement sur PC1 / DC1.
2. L'agent Wazuh (port 1514) les transmet au serveur Wazuh.
3. Le moteur de règles analyse les logs en temps réel et génère des alertes
   visibles dans le dashboard.

## Méthodologie (cycle Purple Team itératif)
Scénario MITRE ATT&CK → Simulation contrôlée → Collecte des logs →
Analyse Wazuh → Évaluation et lacunes → Amélioration des règles → Validation

## Scénarios
| Technique | ID MITRE | Trace principale | Statut |
|---|---|---|---|
| [Modify Registry](scenarios/T1112-modify-registry.md) | T1112 | Sysmon 12/13 | Terminé |
| [Registry Run Keys](scenarios/T1547.001-registry-run-key.md) | T1547.001 | Sysmon 13 | Terminé |
| [Remote Desktop Protocol](scenarios/T1021.001-rdp.md) | T1021.001 | Event 4624 (type 10) | Terminé |
| [Scheduled Task](scenarios/T1053.005-scheduled-task.md) | T1053.005 | Event 4698 / Sysmon 1 | Terminé |
| [PowerShell](scenarios/T1059.001-powershell.md) | T1059.001 | Sysmon 1 | En cours |

Synthèse complète : [results/detection-matrix.md](results/detection-matrix.md)

## Lacunes identifiées
- Volume de logs natifs très bruité, à filtrer avec Sysmon.
- PowerShell encodé/obfusqué : nécessite le Script Block Logging (Event ID 4104).
- RDP : manque de règles personnalisées.

## Amélioration réalisée
Une règle Wazuh personnalisée a été conçue pour lever une alerte de sévérité
accrue lors de la création d'une tâche planifiée ou d'une modification de
registre suspecte.

## Limites
Environnement restreint à un nombre limité de nœuds et de scénarios, en raison
des contraintes de ressources matérielles.

## Avertissement
Projet à but éducatif. Toutes les simulations ont été exécutées uniquement
dans un environnement virtuel isolé.

## Auteure
Majda El-Gtay, élève ingénieure en cybersécurité (ENSIASD)
[LinkedIn](https://linkedin.com/in/majda-el-gtay) · [GitHub](https://github.com/Majdae)