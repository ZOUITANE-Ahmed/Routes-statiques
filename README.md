# Routes-statiques

Le routage statique est une méthode utilisée pour configurer manuellement les routes dans une table de routage. Voici une description détaillée de chaque type de route statique mentionné :  

---

### **1. Routes statiques connectées**  
Les routes statiques connectées pointent directement vers une interface de sortie. Cela signifie que le routeur envoie le trafic directement via une interface spécifiée sans avoir besoin de résoudre une autre adresse IP.  

**Exemple de configuration :**  
```  
ip route 192.168.1.0 255.255.255.0 FastEthernet0/0  
```  
Ici, la route spécifie le réseau 192.168.1.0/24 qui est directement accessible via l'interface FastEthernet0/0.

---

### **2. Routes statiques récursives**  
Une route statique récursive spécifie une adresse IP de prochain saut (next hop) plutôt qu'une interface. Le routeur doit effectuer une résolution pour déterminer par quelle interface envoyer les paquets en se basant sur l'adresse IP du prochain saut.  

**Exemple de configuration :**  
```  
ip route 192.168.2.0 255.255.255.0 10.1.1.1  
```  
Le routeur enverra les paquets vers l'adresse IP 10.1.1.1, et une résolution supplémentaire sera effectuée pour déterminer l'interface utilisée.

---

### **3. Routes statiques flottantes**  
Les routes statiques flottantes sont des routes de secours utilisées en cas de défaillance de la route principale. Elles sont configurées avec une **métrique administrative plus élevée**, ce qui signifie qu'elles ne seront utilisées que si les routes principales échouent.  

**Exemple de configuration :**  
```  
ip route 192.168.3.0 255.255.255.0 10.1.1.2 200  
```  
Ici, la métrique administrative (200) est plus élevée que celle par défaut (1), ce qui rend cette route secondaire.

---

### **4. Routes statiques récapitulatives**  
Les routes statiques récapitulatives sont utilisées pour regrouper plusieurs routes en une seule, ce qui réduit la taille de la table de routage. Cela est particulièrement utile dans les environnements complexes avec de nombreux sous-réseaux.  

**Exemple de configuration :**  
```  
ip route 192.168.0.0 255.255.252.0 FastEthernet0/1  
```  
Cette route récapitule les réseaux 192.168.0.0/24, 192.168.1.0/24, 192.168.2.0/24, et 192.168.3.0/24.

---

### **5. Routes statiques par défaut**  
Une route statique par défaut est utilisée pour envoyer tout trafic qui ne correspond pas à une entrée spécifique dans la table de routage. Elle agit comme un "catch-all".  

**Exemple de configuration :**  
```  
ip route 0.0.0.0 0.0.0.0 10.1.1.1  
```  
Tout trafic pour lequel il n'y a pas de route spécifique sera dirigé vers 10.1.1.1.  

---

### **Résumé**  
- **Connectées** : Basées sur une interface locale.  
- **Récursives** : Nécessitent un prochain saut.  
- **Flottantes** : Routes de secours.  
- **Récapitulatives** : Groupent plusieurs routes.  
- **Par défaut** : Destination par défaut pour le trafic inconnu.  
