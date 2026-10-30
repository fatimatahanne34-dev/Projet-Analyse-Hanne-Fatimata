# Rapport d'analyse des journaux de pare-feu

## 1. Résumé de l'analyse
Cette analyse s'est penchée sur une semaine d'historique des connexions réseau et des journaux de pare-feu (`logs_reseau.csv`) d'une entreprise comportant des postes informatiques, des serveurs et des objets connectés. Après un nettoyage rigoureux des données (suppression des doublons, uniformisation des protocoles et gestion des valeurs manquantes), plusieurs indicateurs clés ont été calculés et consignés dans le fichier `resultats.json`. L'examen des flux met en lumière des activités anormales nécessitant une intervention rapide de la sécurité.

## 2. Comportements suspects observés
* **Comportement 1 (Scan de ports) :** Une adresse IP source spécifique a été identifiée comme ayant contacté le plus grand nombre de ports distincts (`ip_scanner`). Ce comportement est typique d'une phase de reconnaissance ou d'un scan de vulnérabilités mené par un acteur malveillant pour cartographier le réseau de l'entreprise.
* **Comportement 2 (Exfiltration potentielle de données) :** Une autre adresse IP source génère un volume anormalement élevé d'octets envoyés (`bytes_sent`), surpassant largement la moyenne des autres appareils (`ip_exfiltration`). Cela suggère une fuite de données massive ou un transfert non autorisé vers l'extérieur.

## 3. Recommandations de sécurité
1. **Segmentation du réseau IoT :** Isoler les objets connectés (caméras, capteurs) sur un VLAN dédié et étanche pour empêcher qu'un équipement compromis ne serve de passerelle vers les serveurs critiques de l'entreprise.
2. **Durcissement des règles de pare-feu :** Bloquer immédiatement les flux provenant de l'adresse IP effectuant le scan de ports et restreindre les connexions sortantes non autorisées pour contrer tout risque d'exfiltration.
3. **Fermeture des services non sécurisés :** Désactiver l'utilisation de protocoles et de ports obsolètes ou non chiffrés (tels que Telnet) au profit d'alternatives sécurisées (SSH).
4.