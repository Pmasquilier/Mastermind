
  
Composant pur définition  
, 2 manières de les créer :  
Extends React.PureComponent  
React.momo(maFctComponent)  
À utiliser pour des gros composants à logique complexe  
  
Pour un pure component, À chaque fois que l'on fait une mutation, un setState, il ne faut pas muter l'état précédent mais envoyer un nouvel objet representant notre nouvel état, grâce au spread operator par exemple.  
Revoir chapitre 10 grafikart  
  
On peut utiliser les ref pour accéder à une propriété d'un objet dans le dom  
Constructeur :  
This.input = React.createRef()  
Dans le render() : input type ="text" ref={this.input}  
On accède ensuite à la valeur : this.input.current.value  
On peut utiliser forwardref (qui est une fonction d'ordre supérieure) pou faire passer des références à des enfants  
  
Télécharger extension react dev tool  
  
  
  
  
Si on ne veut pas créer de tag racine dans react, qui est pourtant obligatoire, on peut créer un tag fragment. !  
![[Screenshot_2022-10-01-10-40-56-750-edit_com.google.android.youtube.jpg]]  
Une class React doit extends React.Component  
  
fonction componentdidMount et componentwillunmount : se renseigner sur les cycles de vie react  
  
Se renseigner sur this.tick.bind(this)  
  
synteticEvent est une classe React qui englobe les évènements classiques  
  
Composant pur définition  
, 2 manières de les créer :  
Extends React.PureComponent  
React.momo(maFctComponent)  
À utiliser pour des gros composants à logique complexe  
  
Pour un pure component, À chaque fois que l'on fait une mutation, un setState, il ne faut pas muter l'état précédent mais envoyer un nouvel objet representant notre nouvel état, grâce au spread operator par exemple.  
Revoir chapitre 10 grafikart  
  
On peut utiliser les ref pour accéder à une propriété d'un objet dans le dom  
Constructeur :  
This.input = React.createRef()  
Dans le render() : input type ="text" ref={this.input}  
On accède ensuite à la valeur : this.input.current.value  
On peut utiliser forwardref (qui est une fonction d'ordre supérieure) pou faire passer des références à des enfants  
  
Télécharger extension react dev tool  
  
  
  
  
LinkedIn  
Résumé : rajouter un petit emoji et une phrase qui me caractérise, par exemple l'ambl'ambl'ambitionje développé un code de qualité. Une phrase qui cible.  
  
Bannière : bulle, technologie, start-up, crypto