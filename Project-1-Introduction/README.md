# Projet 1 - Introduction

Le projet est créé avec vite en typescript.

## Installation de Three.js

Three.js :

`npm install three --save-dev`

Les types typescript :

`npm install @types/three --save-dev`

Ces deux dépôts ne sont pas maintenus par le même organisme, donc il peut y avoir un décalage lors des mises à jour, vérifier la version des dépôts dans `package.json`

```json
{
    ...
    "devDependencies": {
        "@types/three": "^0.176.0",
        "three": "^0.176.0",
        ...
    },
    ...
}
```

## Modules supplémentaire

Plusieurs modules supplémentaires sont utilisables avec Three.js, mais sont importable d'une manière spécifique, car ils sont situés dans le dossier `node_modules/three/examples`, il existe un `export` spécifique pour utiliser `addons` au lieu de `examples/jsm`.

Par exemple, pour ajouter le contrôle de l'objet avec la souris :

```js
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
// ou
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'

new OrbitControls(camera, renderer.domElement)
```

## Statistiques de développement

Il est toujours intéressant d'avoir des données de statistique pendant le développement, avec `stats.module` on peut avoir 3 types de statistique, FPS, MS (entre chaque frame) et MB. L'affichage est par défaut en haut à gauche :

```js
import Stats from 'three/addons/libs/stats.module.js'

const stats = new Stats()
document.body.appendChild(stats.dom)

// Utilisation de manière global dans une boucle d'animation
stats.update()

// utilisation sur un morceau de code
stats.begin()
cube.rotation.x += 0.01
cube.rotation.y += 0.01
stats.end()
```

On peut ajouter une valeur pour définir quel est l'affichage par défaut :

```js
stats.showPanel(0) // 0: fps, 1: ms, 2: memory
```

## Bibliothèques tierces

Il existe tout un tas de bibliothèques tierces qui peuvent être utilisé avec Three.js, une populaire avec un historique connu est `Dat GUI` :

- `npm install dat.gui@latest --save-dev`
- `npm install @types/dat.gui@latest --save-dev`

Documentation du projet -> [API Documentation](https://github.com/dataarts/dat.gui/blob/master/API.md)

On peut ajouter de l'interaction avec cette interface, sur les axes de rotation :

```js
const gui = new GUI()
gui.add(cube.rotation, 'x', 0, Math.PI * 2)
gui.add(cube.rotation, 'y', 0, Math.PI * 2)
gui.add(cube.rotation, 'z', 0, Math.PI * 2)
```

On peut mettre nos propriétés d'interaction dans un genre de dossier :

```js
const cubeFolder = gui.addFolder('Cube')
cubeFolder.add(cube.rotation, 'x', 0, Math.PI * 2)
cubeFolder.add(cube.rotation, 'y', 0, Math.PI * 2)
cubeFolder.add(cube.rotation, 'z', 0, Math.PI * 2)
```

On peut choisir si on veut qu'un dossier soit ouvert au chargement (ils sont fermés par défaut) :

```js
cubeFolder.open()
```

Il existe bien d'autre bibliothèque de GUI à explorer.
