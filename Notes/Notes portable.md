JavaScript est né en 1995 , repris par Microsoft en 1996 et standardisé via la fondation européenne ECMA en 1997 pour éviter les problèmes notamment de compatibilité.

C'est à partir de la que naissent les SPAs avec des outils tels que flash ou applets java. Il y a vite des limitations car il faut par exemple à l'utilisateur de télécharger les plugins associés, et l'application est bloquées au sein de sa surcouche (ex JVM) ce qui rends difficile la communication avec le navigateur.

Le problème de JavaScript est qu'il ne gère pas la communication avec le backend. Microsoft travaille entre 1997-2002 sur XMLHttpRequest qui résout ce problème. C'est AJAX.

En 2006 arrive JQuery, une librairie JavaScript qui apporte une syntaxe fluide et simplifiée, une uniformité cross browser, des animations et une utilisation de Ajax plus simple.

En 2015, ECMA sort la recommandation ES6 qui apporte beaucoup de nouveautés. Par exemple la fonction fléchée qui conserve le contexte dans laquelle elle a été écrite. 

2009 arrive NodeJS, le JS hors navigateur avec NPM. 

2012: arrivé de grunt, task runner en JS

2012: Testacular, framework de tests unitaires. Aujourd'hui Karma.

2013: Browsersify. Utiliser module NodeJS dans le navigateur. 

2014: webpack, module bundler. 

### Quelques vocabulaires :

Bundling : rassembler du code issu de plusieurs fichiers en un seul afin de réduire les requêtes http.

Minification : supression de tous les espaces, commentaires etc ... non significatifs afin de réduire le poids.

Mangling : obfuscation du code réduction drastique. On change le nom des fonctions, des variables etc pour le rendre illisible. Raccourcis le nom de variable et réduit donc la taille du fichier. 

Tree Shaking : supression de tout le code inutilisé. (Secouer un arbre pour enlever les feuilles mortes)




Notes sur JavaScript : 

Le JavaScript est un language interprété. => Voir def , faiblement typé, orienté prototype, mono-thread, asynchrone (qui permet dordonnancer les tâches dans un certain ordre, différent du multi thread)

Event loop ![[Screenshot_2022-10-04-14-02-37-505_md.obsidian.png]]
Avec T tâche JavaScript et à droite le rendu du dom(60fps)

Conférence de Jake Archibald. 

WebAPI : les fonctionnalités utilisables depuis JavaScript dans le navigateur web, consensus entre les différents navigateurs. 
Exemple : setTimeout est une fonction de la webAPI du navigateur. La webAPI permet de faire du multithread. 
Exemple, on appelle setTimeout de la webAPI sur 5s. Au bout de 5s, la webAPI va rajouter une tâche dans la queue pour être ensuite rajouter dans la call stack. 
Document.getElementById par exemple permet de taper sur la webAPI pour récupérer des éléments sur le DOM. 

Pour la variable s'appelle document ? Car à la base le web est fait pour s'échanger des documents scientifiques entre université. C'est pour ça qu'on parle d'ailleurs de document HTML. 

Window permet de faire appelle au navigateur via la webAPI (ce qui prrmet de faire du webGL, des timers...)

### Librairies UI
Elles permettent, notamment, de simplifier la manipulation du DOM.

Une des premières librairies : JQuery.
Exemple de code :
![[Screenshot_2022-10-04-20-41-11-950_md.obsidian.png]]
JQuery apporte aussi l'interface fluide , c'est à dire enchaînement de méthodes sur un objet : 
![[Screenshot_2022-10-04-20-43-37-492_md.obsidian.png]]
Elle permettait aussi d'uniformiser le code quelque soit le navigateur. 

Les SPAs deviennent de plus en plus complexe (étendue des interactions, multiplicité des états), et JQuery n'apporte qu'un sucre syntaxique ce qui n'est pas suffisant. 

D'où l'apparition de framework (Angular) et de librairies (react, vueJS...).

2013: Facebook sort react et vise à simplifier l'interaction avec le DOM. Il décompose une application en composants, avec chacun ses données, ses interactions avec l'utilisateur, ses traitements et leur visuel.  

Un composant c'est des états (et props), une présentation et des traitements.

React doit détecter qu'un état change pour actualiser la page. On le prévient en appelant une fonction spécifique (setState).

Pour créer une copie d'un tableau "clients" contenu dans l'état :
this.state.clients.slice()
On peut ensuite modifier le tableau et changer l'état du tableau avec un setState.

Destructuring c'est changer :
const details = this.props.details;
const onDelete = this props.onDelete;
En:
const [details, onDelete] = this.props;

Composant fonctionnel :
Si un composant n'a pas de state, alors on peut le transformer en composant fonctionnel. En suivant les étapes suivantes :

- Changer la classe en fonction
- Le this n'existe plus dans la fonctionnalité on, donc on peut passe les props en paramètre
- Prendre la destructuration et la mettre en paramètre de la fonction 
- 
- Transformer la fonction en fonction fléchée
- Enlever le return car un seul élément 

![[Screenshot_2022-10-05-21-41-33-019_com.google.android.youtube.png]]

![[Screenshot_2022-10-05-21-40-13-936_com.google.android.youtube.png]]****

### Les hooks

Comment gérer ce qui relève du state dans un fonctionnal component et transformer donc une classe react qui gère un state en functionnal component qui gère toujours un state ?

Un des principal hooks est useState :
![[Screenshot_2022-10-05-22-08-30-113_com.google.android.youtube.png]]
useState, une fois appelé, créé une variable fait référence à l'état du composant. Il ne faut pas changer l'ordre d'appel d'un useState et donc il ne peut pas être utilisé dans une condition ou une boucle. Si on fait une mutation qui dépend d'un état précèdent, il vaut mieux utiliser un callback. Par contre avec le setState des hooks, il faut utiliser un nouvel objet contrairement au setState composant ou on pouvait faire de la fusion d'objet. 

On peut créer des hooks personnalisés en fonction de nos besoins. Si on veut extraire de la fonction le useState, il faut obligatoirement utiliser des hooks personnalisés.

Hook useEffect: 
Est utilisé pour creer des effets associés à des changé d'états. En premier paramètres, il prend une fonction qui va permettre de faire un traitement. Second paramètres, il prends les dépendances, soit les valeurs à observer pour effectuer le Hook. On peut enfin retourner à la fin de useEffect une fonction qui servira de fonction de nettoyage qui permettra de supprimer des éléments qui aurait pu été creer dans le useEffect (exemple web socket)

useMemo permet de mémoriser une valeur et useCallback permet de générer un callback qui ça être memoiser. 

Le hook useRef : permet de stocker une valeur et faire de faire référence à un objet dans le DOM. 

Hook useLayoutEffect

Hook useReducer 

Npm create-react-app permet de créer une application react déjà configurée, avec les imports qui vont bien et quelques lignes de commandes. 

Si l'on veut modifier la configuration react, par exemple modifier webpack, il faudra faire ce qu'on appelle un eject (npm eject). Attention il faudra commit au préalable et on ne pourra pas revenir en arrière.

### Parcel
Il faut installer via npm. Parcel-bundler.
Ensuite npx parcel index.html et démarre un serveur de développement.

Parcel permet aussi de builder, de faire du hot reload... Il permet de faire aussi le "fast refresh" qui permet de rafraîchir un composant sans perdre son état. Il faut par contre utiliser les Hooks.

### Contexte react :
Permet de résoudre le problème de passer des props à travers un arbre complexe de composants. Il faut utiliser themeContext.provider chez le parent et themeContext.consumer chez le(s) enfants.
L'enfant peut récupérer la valeur ou un callback 
Si on précise une valeur dans le provider qui est un objet, penser à utiliser la même référence ou useMemo ou useRef, sinon a chaque fois que le dom parent est rerendu, ça va rerendre les enfants.
Au lieu d'utiliser la syntaxe themeContext.consumer, on peut utiliser le hook useContect
Sous forme de classe, on peut attribuer l'objet de nom de variable contextType à notre contexte défini dans le parent. Problème : on ne peut alors définir qu'un objet pour le contexte. 

### Portale
Pour monter un élément dans une partie du dom spécifique, par exemple à la racine, on peut utiliser la méthode createPortale qui prends en premier paramètres l'élément et en deuxième paramètre le noeud du dom.
Ex: pour une modale, un message d'alerte ...

### react.children

Permet de récupérer un ensemble de méthodes permettant de manipuler les enfants et de récupérer certaines de leurs infos. 
Par contre on ne peut pas les modifier directement. Par contre on peut cloner (avec React.cloneElement) l'élément parent en changeant les propriétés des enfants. 

### gestion d'erreur 
Pour capturer des erreurs, on peut créer un composant "erreur boundarie" qui permet d'éviter à l'erreur de remonter.

Dans le composant, on peut utiliser la fonction componentDidCatch. Pour afficher un nouveau rendu, on peut utiliser la fonction getDerivedStateFromError. 

### props-type

Props-type est une librairie qui va permettre de mettre en place une validation des différentes propriétés qui sont reçues par React. 

