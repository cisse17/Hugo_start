---
title: "Python"
date: 2023-11-26T13:03:35+01:00
tags: ['cours de Python']
featured_image: "/images/python.jpg"
description: "Cours de python "
type: page
menu: main
---

## Exemple web scraping avec python


### SCRAPING    => installer requests et beautifulsoup4 (bs4) version 4

Le scraping ou web scraping est une technique qui permet de récolter des données
en masse en mode automatique sur une page ou un site web.
Cette approche permet donc de trouver des contacts rapidement et sans efforts manuels.

Requests  permet de faire une requete http pr recuperer les données à partir d'un url mais cet exemple on travaille sur un fichier local recette.html

```
from bs4 import BeautifulSoup
f = open("recette.html", "r")
html_content = f.read()
f.close()
soup = BeautifulSoup(html_content, "html.parser") #en premier ilfaut recuperer le contenu de la page html

titre_h1 = soup.find("h1")  #on lui demande de trouver le h1
#Extraire LA DESCRIPTION page
paragraphe_description = soup.find("p", class_="description")
#Extraire la src de l'image
div_info = soup.find("div", class_="info")
src_img = div_info.find("img")


print("Titre de la page html : " + titre_h1.text)  #et de ns recuperer le texte
print("Paragrahe de description : ", paragraphe_description.text)
print("La source de l'image est : ", src_img["src"])

```

# Consigne exercice avec les filtre en python 
 - afficher uniquement les pizzas vegetariennes
 - afficher les pizzas non vegetariennes
 - que les pizzas qui ont de la tomate
 - Que les pizzas qui coutent moins de 10 euros
- Demander ingredient utilisateur
- calculer le prix
- demander plusieurs pizzas personnalisees
- Amelioration de la pizza personnalisée de maniere automatique(au ieu de mettre 1,ou 2 sur PizzaPersonnalisee(1),  PizzaPersonnalisee(2))

```
class Pizza:
    def __init__(self, nom, prix, ingredients, vegetarienne = False):
        self.nom = nom
        self.prix = prix
        self.ingredients = ingredients
        self.vegetarienne = vegetarienne


    def Afficher(self):
        vege_str = ""
        if self.vegetarienne:
            vege_str = "- VEGETARIENNE"
        print(f"PIZZA : {self.nom}: {self.prix}£ " + vege_str)
        print(", ".join(self.ingredients))
        print()


class PizzaPersonnalisee(Pizza):
    PRIX_DE_BASE = 7
    PRIX_PAR_INGREDIENT = 1.2
    dernier_numero = 0

    def __init__(self):     #, numero
        PizzaPersonnalisee.dernier_numero += 1      #incrementer 1    attention pr utiliser la variable de classe il faut bien passer par le nom de la class com PizzaPersonnalisee.dernier_numero. avec le self.dernier_numero ça peut marcher mais pas preferable attention
        self.numero = PizzaPersonnalisee.dernier_numero
        super().__init__(f"Personnalisée {str(self.numero)}", 0, [])  # () parenthése vide pr ingredients . mais attention la suite pr initialiser avec une liste pr pouvoir ajouter les ingredients donc modifier par []
        #self.demander_ingredients_utilisateurs()
        self.calculer_le_prix()

    def demander_ingredients_utilisateurs(self):
        print()
        #"Ingredients pour la pizza personnalisee 1"
        print(f"Ingredients pour la pizza personnalisee {self.numero}")

        while True:
            ingredient = input("Ajouter un ingredient (ou ENTER pour terminer) : ")
            if ingredient == "":
                return
            self.ingredients.append(ingredient)
            print(f"vous avez {len(self.ingredients)} ingredient(s) : {', '.join(self.ingredients)} ")


    def calculer_le_prix(self):
        self.prix = self.PRIX_DE_BASE + len(self.ingredients) * self.PRIX_PAR_INGREDIENT


liste_pizzas = [
    Pizza("4 frommage", 8.5, ("brie", "emmental", "compté", "parmésan"), True),
    Pizza("Pepperoni", 9.5, ("Jambon", "pepperoni", "tomate")),
    Pizza("Indienne", 13, ("champignons", "onion", "emmental", "poulet")),
    Pizza("Vegetarienne", 9, ("tomate", "poivrons", "onion", "champignons", "poivrons"), True),
    PizzaPersonnalisee(),
    PizzaPersonnalisee()
    #PizzaPersonnalisee(1),
    #PizzaPersonnalisee(2)
    ]

#---Trier---- on pouvez le faire aussi a l'interieur de notre class
def tri(e):
    return e.nom
        #e.prix
        #len(e.ingredients)
```