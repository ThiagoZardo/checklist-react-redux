# checklist-react-redux

## 0º Instalação do redux
  npx create-react-app my-app-redux;
  npm install --save redux react-redux
  npm install.

  npm install redux-devtools-extension 

================================================================================

## 1º Criar pasta STORE dentro dela criar um index.js.

  import { createStore } from 'redux';
  const store = createStore();
  export default store;

================================================================================

## 2º Criar pasta REDUCERS dentro dela criar um index.js.

  const INITIAL_STATE = {
    value1: '',
    value2: '',
  };

  function nomeReducer(state = INITIAL_STATE, action) {
    switch (action.type) {
      case 'TIPO_DA_ACTION':
        RETURN {
          ...state,
          value1: action.payload.value1,
          value2: action.payload.value2,
        }
      default:
        return state;
    }
  }

  export default nomeReducer;

================================================================================

## 3º Criar pasta ACTIONS dentro dela criar um index.js.

  const nomeDaAction = (value1, value2) => ({ 
    type: TIPO_DA_ACTION,
    payload: {
      value1: value1
      value2: value2
    }
  });

  export default nomeDaAction;

================================================================================

## 4º Importar o reducer no STORE no index.js e criar o combinador de reducers.

  import { createStore, combineReducers } from 'redux';
  import nomeReducer from '../reducers';

  const rootReducer = combineReducers({ nomeReducer });

  const store = createStore(
    rootReducer,
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()   
  );
  export default store; 

================================================================================

## 5º No indice da aplicação do React index.js ou no App.js encapsular tudo com o Provider.

  import { Provider } from 'react-redux';
  import store from './store';

  React.render(
      <React.StricMode>
        <Provider store={store}>
          <App />
        </Provider>
      </React.StricMode>
  )

================================================================================

## 6º No Componente.js que contem o botão ou o elemento que chamará ação:

  import nomeDaAction from '../reducers';

   ======================== 1º opção ============================ 

  const mapDispatchToProps = (dispatch) => ({
    nomeDaProp: (value1, value2) => dispatch(nomeDaAction(value1, value2)),
  });

  export default connect(null, mapDispatchToProps)(nomeDoComponente);

  No botão PRECISA CONTER O DISPATCH QUE PASSARA A ACTION PARA O REDEUCER:
  1º opção onClick={ () => prop(estado) }>
  
  ======================== 2º opção ============================ 
  
  No botão PRECISA CONTER O DISPATCH QUE PASSARA A ACTION PARA O REDEUCER:
  onClick={ () => dispatch(nomeDaAction(value1, value2)) }
  export default connect()(nomeDoComponente);


================================================================================

## 7º Ainda no Componente.js que precisará ter acesso a leitura do estado:

  import { connect } from 'react-redux';

  Abaixo do Render() {
    const { value1, value2 } = this.props;
  }

  const mapStateToProps = (state) => ({
    value1: state.nomeReducer.value1,
    value2: state.nomeReducer.value2,
  })

  export default connect(mapStateToProps)(NomeDoComponente)

================================================================================


PARTES DO REDUX => 
ACTION =>
DISPATCH =>
STORE =>
REDUCER =>
GETSTATE =>
PROVIDER =>
MAPSTATETOPROPS =>
MAPDISPATCHTOPROPS =>
CONNECT =>


# RESUMO
+ A CONNECT liga a action ao componente.
+ Quando CHAMAMOS O EVENTO, ele faz o dispatch da ACTION que esta no mapDispatchToProps,
+ O mapispatchToProps, pega a estrutura da Action e leva ao reducer
+ O REDUCER faz a alteração do estado.
+ O estado é atualizado na STORE


# Checklist react-redux: Passo a passo para guardar no coração

*Antes de começar*
- [ ] pensar como será o *formato* do seu estado global
- [ ] pensar quais actions serão necessárias na sua aplicação

*Instalação*
- [ ] npm i redux react-redux;
- [ ] npm i redux-devtools-extension;

*Criar dentro do diretório src:*
- [ ] diretório `redux`

**Criar dentro do diretório `redux`**
- [ ] diretório `store`
- [ ] diretório `actions`
- [ ] diretório `reducers`

*Criar dentro do diretório `actions`:*
- [ ] arquivo `index.js`.

*Criar dentro do diretório `reducers`:*
- [ ] arquivo `index.js`.

*Criar dentro do diretório `store`:*
- [ ] arquivo `index.js`.

*Criar dentro do diretório `reducers`:*
- [ ] criar os reducers necessários
- [ ] criar `rootReducer` usando o `combineReducers` no arquivo index.js


exemplo:

*Seu reducer pode seguir esse modelo.*

```js
const INITIAL_STATE = {};

const nomeReducer1 = (state = INITIAL_STATE, action) => {
 switch(action.type) {
   default:
    return state;
 }
}

export default nomeReducer1;

```

```js
import { combineReducers } from 'redux';
import nomeReducer1 from './nomeReducer1';
import nomeReducer2 from './nomeReducer2';

const rootReducer = combineReducers({
  nomeReducer1,
  nomeReducer2,
});

export default rootReducer;
```

*No arquivo store/index.js:*
- [ ] importar `rootReducer` e usá-lo na criação da `store`
- [ ] configurar o [Redux DevTools](https://github.com/reduxjs/redux-devtools)
- [ ] exportar a `store`

```js
import { createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import rootReducer from '../reducers';

const store = createStore(
  rootReducer,
  composeWithDevTools(),
);

export default store;
```

*No arquivo App.js:*
- [ ] importar a `store`
- [ ] definir o Provider, `<Provider store={ store }>`, para fornecer os estados a todos os componentes encapsulados em `<App />`.

*Na pasta actions:*
- [ ] criar e exportar os actionTypes;`
- [ ] criar e exportar os actions creators necessários

*Exemplo de action types (arquivo actionTypes.js)*

```js
export const USER_LOGIN = 'USER_LOGIN';
```
*Exemplo action creator*

```js
import { USER_LOGIN } from '../actions/actionTypes';
export const minhaAction = (value) => ({ type: USER_LOGIN, value });
```

*Nos reducers:*
- [ ] criar os casos para cada action criada, retornando o devido estado atualizado

*Nos componentes que irão ler o estado:*
- [ ] criar a função `mapStateToProps`
- [ ] exportar usando o `connect`

*Nos componentes que irão modificar o estado:*
- [ ] criar a função `mapDispatchToProps`
- [ ] exportar usando o `connect`

```js
export default connect(mapStateToProps, mapDispatchToProps)(Component)
```
