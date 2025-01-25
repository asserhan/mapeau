
# mapeau
# Exercice 2 : Gestion de Stock - Documentation Technique

## 📋 Objectif du Projet
Système de gestion de stock multi-magasin avec suivi de produits par code-barres

## 🏗️ Structure de Données

### Collections
- **stores**: Informations des magasins
- **products**: Détails des produits
- **inventory**: Gestion des stocks et réservations

## 🔑 Caractéristiques Principales
- Identifiant unique par code-barres
- Support multi-magasin
- Gestion des dates d'expiration
- Système de réservation intégré


## 🛠️ Opérations Supportées
- Ajout/suppression de produits
- Mise à jour du stock
- Création de réservations
- Suivi des expiration

## 📝 Notes Techniques
- Un produit = Un code-barres
- Gestion flexible des stocks
- Traçabilité complète

## 🚀 Prérequis
- Format NoSQL
- Système de gestion de stock modulaire

# Exercice 2 : Transformations Matricielles et Rotation

## 📋 Objectif du Projet

- Multiplication matricielle
- Matrice de rotation 3D
- Transformation dans l'espace RGB

## Partie 1 : Multiplication Matricielle

```
[[(1*10 + 2*13 + 3*16), (1*11 + 2*14 + 3*17)],
 [(4*10 + 5*13 + 6*16), (4*11 + 5*14 + 6*17)]]

= [[1*10 + 2*13 + 3*16, 1*11 + 2*14 + 3*17],
   [4*10 + 5*13 + 6*16, 4*11 + 5*14 + 6*17]]

= [[10 + 26 + 48, 11 + 28 + 51],
   [40 + 65 + 96, 44 + 70 + 102]]

= [[84, 90],
   [201, 216]]
```

## Partie 2 : Rotation 3D

# Droite D1

Points : (0,0,0) et (255,255,255)
Vecteur directeur : (1,1,1)

# Matrice de Rotation

Méthode : Formule de Rodrigues
Transformation : Rotation autour de l'axe (1,1,1)

Matrice de rotation de Rodrigues
Formule : R = cos(θ)I + sin(θ)[u]× + (1-cos(θ))(u')(u')^T

Vecteur : u = (1, 1, 1)
Vecteur unitaire : u' = u / ||u|| = (1/√3, 1/√3, 1/√3)
I : est la matrice identité

Matrice antisymétrique [u]× :

```
[u]× = [  0  -1/√3  1/√3  ]
       [ 1/√3   0  -1/√3  ]
       [-1/√3  1/√3   0   ]
```

Matrice produit externe (u')(u')^T :

```
[u'][u']^T = [ 1/3   1/3   1/3  ]
             [ 1/3   1/3   1/3  ]
             [ 1/3   1/3   1/3  ]
```

Construction finale (pour θ = π/2)

cos(θ) = 0
sin(θ) = 1

Matrice de rotation :

```
R = 0 * I + 1 * [u]× + (1-0)*(u')(u')^T

   = [  0  -1/√3  1/√3  ] + [ 1/3   1/3   1/3  ]
     [ 1/√3   0  -1/√3  ]   [ 1/3   1/3   1/3  ]
     [-1/√3  1/√3   0   ]   [ 1/3   1/3   1/3  ]
```
# Implémentation Python
```
import numpy as np

def rotation_matrix(axis, theta):
    # Normalisation de l'axe
    axis = np.asarray(axis)
    axis = axis / np.linalg.norm(axis)
    
    # Matrice de rotation de Rodrigues
    a = np.cos(theta)
    b = np.sin(theta)
    c = 1 - np.cos(theta)
    
    x, y, z = axis
    
    return np.array([
        [a + x*x*c, x*y*c - z*b, x*z*c + y*b],
        [y*x*c + z*b, a + y*y*c, y*z*c - x*b],
        [z*x*c - y*b, z*y*c + x*b, a + z*z*c]
    ])
```
# Bonus : Transformation de l'Espace RGB

## Objectif
Projection orthogonale maintenant C1 dans l'axe orthogonal à D1

# Type de Transformation
Projection Orthogonale
Conserve l'appartenance au cube RGB

# Équations
Vectorielle

Projection de C1 sur l'axe orthogonal
P = (v · x / ||v||²) v
```
P = I - (vv^T / ||v||²)
```
I est la matrice identité
u est le vecteur directeur de la droite de rotation

# Implémentation Python

```
def orthogonal_projection(point, axis):
    # Projection sur l'axe orthogonal
    return point - np.dot(point, axis) * axis / np.dot(axis, axis)
```

>>>>>>> 
