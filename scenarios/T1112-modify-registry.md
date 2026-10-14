# T1112: Modify Registry

**Machine cible :** PC1

## Objectif
Modifier la base de registre pour altérer la configuration de sécurité
ou désactiver des contrôles.

## Action réalisée
Exécution d'une commande de modification du registre via `reg add` ou PowerShell.

## Traces générées
- Sysmon Event ID 12 (Registry object added/deleted)
- Sysmon Event ID 13 (Registry value set)

## Résultat Wazuh
Événement remonté, niveau d'alerte qualifié.

## Niveau de détection
Bon

## Amélioration
Règle Wazuh personnalisée pour les modifications de registre suspectes.