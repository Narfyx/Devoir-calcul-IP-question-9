# Devoir-calcul-IP-question-9

## Question:
Comment savoir si les IP noeuds suivant peuvent communiquer :
Imprimante 192.168.5.125/23PC  192.168.6.12
Donner une méthode basé sur le calcul binaire et une autre basé sur https://cric.grenoble.cnrs.fr/Administrateurs/Outils/CalculMasque/ en déterminant pour un des noeuds sa plage d'adresse réseau

## Méthode 1 : Basée sur le calcul binaire
Pour déterminer si deux adresses IP peuvent communiquer directement sur le même réseau, nous devons comparer leurs **adresses réseau** respectives. Pour cela, nous utilisons l'**adresse IP** et le **masque de sous-réseau** pour chaque nœud et effectuons un **"AND" binaire** entre l'adresse IP et le masque de sous-réseau.

#### Étape 1 : Convertir les adresses IP et le masque en binaire

1. **Imprimante** : Adresse IP : **192.168.5.125**, Masque : **/23** (soit 255.255.254.0 en notation décimale).
    
    IP de l'imprimante : 192.168.5.125
```rust
192   -> 11000000
168   -> 10101000
5     -> 00000101
125   -> 01111101
```
**Résultat** : 11000000.10101000.00000101.01111101

	Masque : /23 (255.255.254.0)
```rust
255   -> 11111111
255   -> 11111111
254   -> 11111110
0     -> 00000000
```
**Résultat** : 11111111.11111111.11111110.00000000.

Calcul de l'adresse réseau de l'imprimante (AND binaire entre l'adresse IP et le masque) :
```rust
11000000.10101000.00000101.01111101
AND
11111111.11111111.11111110.00000000
-----------------------------------
11000000.10101000.00000100.00000000
```
L'adresse réseau de l'imprimante est **192.168.4.0**.

**PC** : Adresse IP : **192.168.6.12**, même masque de sous-réseau **/23** (255.255.254.0).
- IP du PC : 192.168.6.12
```rust
192   -> 11000000
168   -> 10101000
6     -> 00000110
12    -> 00001100
```
    
**Résultat**: 11000000.10101000.00000110.00001100
- Masque : 255.255.254.0 (même masque que l'imprimante)
- Calcul de l'adresse réseau du PC :
```rust
11000000.10101000.00000110.00001100
AND
11111111.11111111.11111110.00000000
-----------------------------------
11000000.10101000.00000100.00000000
```
L'adresse réseau du PC est **192.168.4.0**.

#### Étape 2 : Comparer les adresses réseau

- L'adresse réseau de l'imprimante est **192.168.4.0**.
- L'adresse réseau du PC est **192.168.4.0**.

Comme les deux appareils appartiennent à la même adresse réseau, **ils peuvent communiquer directement**.

### Méthode 2 : Utilisation de l'outil en ligne

1. **L'outil en ligne** : [CalculMasque de CRIC Grenoble](https://cric.grenoble.cnrs.fr/Administrateurs/Outils/CalculMasque/).
    
2. **Entrer l'adresse IP de l'imprimante** : 192.168.5.125 avec le masque de sous-réseau **/23**.
    
3. **Obtenir la plage d'adresses réseau** :
    
    - Adresse réseau : **192.168.4.0**
    - Adresse de diffusion (broadcast) : **192.168.5.255**
    - Plage d'adresses : **192.168.4.1 à 192.168.5.254**
4. **Vérifier pour le PC** : L'adresse du PC **192.168.6.12** n'appartient pas à cette plage d'adresses (192.168.4.1 à 192.168.5.254).

#### Conclusion :

Via l'outil, le PC **192.168.6.12** n'appartient pas à la même plage d'adresses, mais via le calcul binaire, il appartient au même réseau. Cela pourrait signifier que la configuration pourrait permettre la communication si la plage d'adresses est vue sur un réseau plus large (ex. : configuration de routeurs ou sous-réseaux).
