# Axios

Axios est client HTTP basé sur les Promises. C'est lui qui va nous permettre de contacter notre API et de récupérer un résultat.

## Installation

```shell
npm install axios
```

## Utilisation

Comme d'habitude on va importer Axios au début de notre page.

```JSX
import axios from 'axios';
```

Ensuite on va utiliser le cycle de vie de React pour interroger notre API lorsque le composant est chargé. Pour ce faire on utilise `componentDidMount()`et à l'intérieur on place `axios.get('lien vers api')`. 

Il nous faut ensuite déterminer ce qu'il se passe avec ces données récupérées. Dans l'exemple en dessous on a une liste de personne avec un state par défaut qui contient une clé `person`qui pour l'instant est un tableau vide. On va alors (then) envoyez les infos (data) récupérées dans notre state en utiliser `.then`et `this.setState`.

Vous pouvez copier-collez ce bout de code pour tester.

```jsx
import React from 'react';
import axios from 'axios';

export default class PersonList extends React.Component {
  state = {
    persons: []
  }

  componentDidMount() {
    axios.get(`https://jsonplaceholder.typicode.com/users`)
      .then(res => {
        const persons = res.data;
        this.setState({ persons });
      })
  }

  render() {
    return (
      <ul>
        { this.state.persons.map(person => <li>{person.name}</li>)}
      </ul>
    )
  }
}
```

## Allez plus loin

Ceci n'est qu'un exemple très simple d'un appel API. Il va vous falloir maîtriser un peu plus les appels API en fonction de vos besoins et de l'API en question. Voici un lien vers [un article](https://www.digitalocean.com/community/tutorials/react-axios-react) qui explique comment utiliser Axios avec React. Bonne lecture!

![catkeyboard](https://media.giphy.com/media/LmNwrBhejkK9EFP504/giphy.gif)