---
jupyter:
  jupytext:
    text_representation:
      extension: .Rmd
      format_name: rmarkdown
      format_version: '1.2'
      jupytext_version: 1.6.0
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
title: "Les classes en Python"
date: 2020-07-09T15:00:00Z
draft: false
weight: 70
output: 
  html_document:
    keep_md: true
    self_contained: true    
slug: "rappelsclasses"
---

**Ce TP est optionnel**


On dit que Python est un __langage orienté objet__  

Mmmh, certes... ça veut dire quoi ? 

En résumé, le langage python se base sur des objets et définit pour eux des actions. 

Chaque objet a des caractéristiques (une taille, un nom, un format etc), peut réaliser des actions etc. 

Un objet dans le monde réel, ça peut-être comme une voiture, une personne ou encore une page d'un livre. Il possède une structure interne et un comportement, et il sait interagir avec ses pairs. 

Pour Python, c'est un peu pareil : un code c'est ni plus ni moins que de représenter ces objets et leurs relations entre eux 



<!-- #region -->

# La définition d'un objet

Pour définir un objet, il faut lui donner des caractéristiques et des actions, ce qu'il est, ce qu'il peut faire.


Avec une liste, on peut ajouter des éléments par exemple avec l'action .append(). On peut créer autant d'objets "liste" qu'on le souhaite. 


__Une classe regroupe des fonctions et des attributs qui définissent un objet. __
Un objet est une instance d'une classe, c'est-à-dire un exemplaire issu de la classe. L'objet avec un comportement et un état, tous deux définis par la classe. On peut créer autant d'objets que l'on désire avec une classe donnée.

Ici nous allons essayer de créer une classe chat, avec des attributs pour caractériser le chat et des actions, pour voir ce qu'il peut faire avec un objet de la classe chat


# Exemple : la Classe chat()

## Les attributs de la classe chat

### Classe chat version 1 - premiers attribus

On veut pouvoir créer un objet chat() qui nous permettra à terme de créer une colonie de chats (on sait
jamais ca peut servir ...).
Pour commencer, on va définir un chat avec des attributs de base : une couleur et un nom.
<!-- #endregion -->


```python
class chat: # Définition de notre classe chat
    """Classe définissant un chat caractérisé par :
    - son nom
    - sa couleur """
    
    def __init__(self): # Notre méthode constructeur - 
        # self c'est notre objet qu'on est en train de créer
        """Pour l'instant, on ne va définir que deux attributs - nom et couleur """
        self.couleur = "Noir"   
        self.nom = "Aucun nom"
```


```python
mon_chat = chat()

print(type(mon_chat), mon_chat.couleur ,",", mon_chat.nom) 
# on nous dit bien que Mon chat est défini à partir de la classe chat 
# c'est ce que nous apprend la fonction type
# pour l'instant il n'a pas de nom
```

```
## <class '__main__.chat'> Noir , Aucun nom
```

### Classe chat version 2 - autres attributs

Avec un nom et une couleur, on ne va pas loin. On peut continuer à définir des attributs pour la classe chat
de la même façon que précédemment.


```python
class chat: # Définition de notre classe chat
    """Classe définissant un chat caractérisé par :
    - sa couleur
    - son âge
    - son caractère
    - son poids
    - son maitre
    - son nom """

    
    def __init__(self): # Notre méthode constructeur - 
        #self c'est notre objet qu'on est en train de créer
        self.couleur = "Noir"    
        self.age = 10
        self.caractere = "Joueur"
        self.poids = 3
        self.maitre = "Jeanne"
        self.nom = "Aucun nom"
```


```python
help(chat) 
# si on veut savoir ce que fait la classe "chat" on appelle l'aide
```

```
## Help on class chat in module __main__:
## 
## class chat(builtins.object)
##  |  Classe définissant un chat caractérisé par :
##  |  - sa couleur
##  |  - son âge
##  |  - son caractère
##  |  - son poids
##  |  - son maitre
##  |  - son nom
##  |  
##  |  Methods defined here:
##  |  
##  |  __init__(self)
##  |      Initialize self.  See help(type(self)) for accurate signature.
##  |  
##  |  ----------------------------------------------------------------------
##  |  Data descriptors defined here:
##  |  
##  |  __dict__
##  |      dictionary for instance variables (if defined)
##  |  
##  |  __weakref__
##  |      list of weak references to the object (if defined)
```


```python
mon_chat = chat()
print("L'âge du chat est", mon_chat.age,"ans") 
# on avait défini l'attribut age de la classe chat comme étant égal à 10
#, si on demande l'attribut age de notre Martin on obtient 10
```

```
## L'âge du chat est 10 ans
```

Par défaut, les attributs de la classe Chat seront toujours les m^emes à chaque création de chat à partir
de la classe Chat.

Mais une fois qu'une instance de classe est créée (ici mon chat est une instance de classe) on peut décider
de changer la valeur de ses attributs.

#### Un nouveau poids


```python
# si on veut changer le poids de mon chat, parce qu'il a un peu grossi après les fêtes
mon_chat.poids = 3.5
mon_chat.poids # maintenant le poids est 3.5
```

```
## 3.5
```

#### Un nouveau nom


```python
# on veut aussi lui donner un nom 
mon_chat.nom = "Martin"
mon_chat.nom
```

```
## 'Martin'
```

#### Une autre instance de la classe Chat

On peut aussi créer d'autres objets chat à partir de la classe chat : 


```python
# on appelle la classe
l_autre_chat = chat()
# on change les attributs qui nous intéressent
l_autre_chat.nom = "Ginette"
l_autre_chat.maitre = "Roger"
# les attributs inchangés donnent la même chose 
# que ceux définis par défaut pour la classe
print(l_autre_chat.couleur)
```

```
## Noir
```

## Les méthodes de la classe chat

Les attributs sont des variables propres à notre objet, qui servent à le caractériser. 

Les méthodes sont plutôt des actions, comme nous l'avons vu dans la partie précédente, agissant sur l'objet. 

Par exemple, la méthode append de la classe list permet d'ajouter un élément dans l'objet list manipulé.

### Classe chat version 3 - première méthode

On peut définir une première méthode : nourrir


```python
class chat: # Définition de notre classe chat
    """Classe définissant un chat caractérisé par :
    - sa couleur
    - son âge
    - son caractère
    - son poids
    - son maitre
    - son nom 
    
    L'objet chat a une méthode : nourrir """

    
    def __init__(self): # Notre méthode constructeur - 
        #self c'est notre objet qu'on est en train de créer
        self.couleur = "Noir"    
        self.age = 10
        self.caractere = "Joueur"
        self.poids = 3
        self.maitre = "Jeanne"
        self.nom = "Aucun nom"
        
        """Par défaut, notre ventre est vide"""
        self.ventre = ""
        
    def nourrir(self, nourriture):
        """Méthode permettant de donner à manger au chat.
        Si le ventre n'est pas vide, on met une virgule avant de rajouter
        la nourriture"""       
        if self.ventre != "":
            self.ventre += ","
        self.ventre += nourriture
```


```python
mon_chat = chat()
mon_chat.nom = "Martin"
mon_chat.ventre # On n'a rien donné à Martin, son ventre est vide
```

```
## ''
```


```python
# on appelle la méthode "nourrir" de la classe chat, 
# on lui donne un élément, ici des croquettes
mon_chat.nourrir('Croquettes')
print("Le contenu du ventre de martin : ",mon_chat.ventre)
```

```
## Le contenu du ventre de martin :  Croquettes
```


```python
mon_chat.nourrir('Saumon')
print("Le contenu du ventre de martin : ",mon_chat.ventre)
```

```
## Le contenu du ventre de martin :  Croquettes,Saumon
```

### Classe chat version 4 - autre méthode

Avec un chat, on peut imaginer plein de méthodes. Ici on va définir une action "nourrir" et une autre action
"litiere", qui consiste à vider l'estomac du chat.


```python

class chat: # Définition de notre classe Personne
    """Classe définissant un chat caractérisé par :
    - sa couleur
    - son âge
    - son caractère
    - son poids
    - son maitre
    - son nom 
    
    L'objet chat a deux méthodes : nourrir et litiere """

    
    def __init__(self): # Notre méthode constructeur - 
        #self c'est notre objet qu'on est en train de créer
        self.nom = ""
        self.couleur = "Roux"    
        self.age = 10
        self.caractere = "Joueur"
        self.poids = 3
        self.maitre = "Jeanne"
        """Par défaut, notre ventre est vide"""
        self.ventre = ""
        
    def nourrir(self, nourriture):
        """Méthode permettant de donner à manger au chat.
        Si le ventre n'est pas vide, on met une virgule avant de rajouter
        la nourriture"""       
        if self.ventre != "":
            self.ventre += ","
        self.ventre += nourriture

    def litiere(self) : 
        """ Méthode permettant au chat d'aller à sa litière : 
        en conséquence son ventre est vide """       
        self.ventre = ""
        print(self.nom,"a le ventre vide")
```


```python
# on définit Martin le chat
mon_chat = chat()
mon_chat.nom = "Martin"
# on le nourrit avec des croquettes
mon_chat.nourrir('croquettes')
print("Le contenu du ventre de martin", mon_chat.ventre)


# Il va dans sa litiere
```

```
## Le contenu du ventre de martin croquettes
```

```python
mon_chat.litiere()
```

```
## Martin a le ventre vide
```


```python
help(mon_chat.nourrir)
```

```
## Help on method nourrir in module __main__:
## 
## nourrir(nourriture) method of __main__.chat instance
##     Méthode permettant de donner à manger au chat.
##     Si le ventre n'est pas vide, on met une virgule avant de rajouter
##     la nourriture
```

```python
help(mon_chat.litiere)
```

```
## Help on method litiere in module __main__:
## 
## litiere() method of __main__.chat instance
##     Méthode permettant au chat d'aller à sa litière : 
##     en conséquence son ventre est vide
```

<!-- #region -->

### ___facultatif___ Les méthodes spéciales 

Si on reprend notre classe chat, il y a en réalité des méthodes spéciales que nous n'avons pas définies mais
qui sont implicites.


Python comprend seul ce que doivent faire ces méthodes. Il a une idée préconcue de ce qu'elles doivent
effectuer comme opération. Si vous ne redéfinissez par une méthode spéciale pour qu'elle fasse ce que vous
souhaitez, ca peut donner des resultats inattendus.

Elles servent à plusieurs choses : 

- à initialiser l'objet instancié : \_\_init\_\_
- à modifier son affichage : \_\_repr\_\_

<!-- #endregion -->


```python
# pour avoir la valeur de l'attribut "nom"

print(mon_chat.__getattribute__("nom"))
# on aurait aussi pu faire plus simple :
```

```
## Martin
```

```python
print(mon_chat.nom)
```

```
## Martin
```

~~~python
# si l'attribut n'existe pas : on a une erreur
# Python recherche l'attribut et, s'il ne le trouve pas dans l'objet et si une méthode __getattr__ est spécifiée, 
# il va l'appeler en lui passant en paramètre le nom de l'attribut recherché, sous la forme d'une chaîne de caractères.

print(mon_chat.origine)
~~~

```
## Error in py_call_impl(callable, dots$args, dots$keywords): AttributeError: 'chat' object has no attribute 'origine'
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```


Mais on peut modifier les méthodes spéciales de notre classe chat pour éviter d'avoir des erreurs d'attributs. On va aussi en profiter pour modifier la représentation de l'instance chat qui pour l'instant donne  <\__main\__.chat object at 0x0000000005AB4C50>

### Classe chat version 5 - méthode spéciale


```python

class chat: # Définition de notre classe Personne
    """Classe définissant un chat caractérisé par :
    - sa couleur
    - son âge
    - son caractère
    - son poids
    - son maitre
    - son nom 
    
    L'objet chat a deux méthodes : nourrir et litiere """

    
    def __init__(self): # Notre méthode constructeur - 
        #self c'est notre objet qu'on est en train de créer
        self.nom = ""
        self.couleur = "Roux"    
        self.age = 10
        self.caractere = "Joueur"
        self.poids = 3
        self.maitre = "Jeanne"
        """Par défaut, notre ventre est vide"""
        self.ventre = ""
        
    def nourrir(self, nourriture):
        """Méthode permettant de donner à manger au chat.
        Si le ventre n'est pas vide, on met une virgule avant de rajouter
        la nourriture"""       
        if self.ventre != "":
            self.ventre += ","
        self.ventre += nourriture

    def litiere(self) : 
        """ Méthode permettant au chat d'aller à sa litière : 
        en conséquence son ventre est vide """       
        self.ventre = ""
        print(self.nom,"a le ventre vide")
    
    def __getattribute__(self, key):
            return print(key,"n'est pas un attribut de la classe chat")   
            
    def __repr__(self):
            return "Je suis une instance de la classe chat"
```


```python
# j'ai gardé l'exemple chat défini selon la classe version 4
# Martin, le chat
# on a vu précédemment qu'il n'avait pas d'attribut origine
# et que cela levait une erreur AttributeError
print(mon_chat.nom)


# on va définir un nouveau chat avec la version 5
# on appelle à nouveau un attribut qui n'existe pas "origine"
# on a bien le message défini par la méthode spéciale _gettattribute
```

```
## Martin
```

```python
mon_chat_nouvelle_version = chat()
mon_chat_nouvelle_version.origine

# Maintenant on a aussi une définition de l'objet plus clair
```

```
## origine n'est pas un attribut de la classe chat
```

```python
print(mon_chat)
```

```
## <__main__.chat object at 0x7f7296838fd0>
```

```python
print(mon_chat_nouvelle_version)
```

```
## Je suis une instance de la classe chat
```

------ 

### Conclusion sur les classes : ce qu'on retient

- Les méthodes se définissent comme des fonctions, sauf qu'elles se trouvent dans le corps de la classe.

- On définit les attributs d'une instance dans le constructeur de sa classe, en suivant cette syntaxe : self.nom_attribut = valeur.

- _facultatif_ : Les méthodes d'instance prennent en premier paramètre "self", l'instance de l'objet manipulé.

- _facultatif_ : On construit une instance de classe en appelant son constructeur, une méthode d'instance appelée __init__.
