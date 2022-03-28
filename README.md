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


# Checklist react-redux: Passo a passo para guardar no coração e colar na parede

### Instalação
- [x] npx create-react-app my-app-redux;
- [x] npm install redux react-redux;
- [x] npm install.
- [x] npm install redux-devtools-extension

### Criar dentro do diretório src:
diretório actions;
diretório reducers;
diretório store.
Criar dentro do diretório actions:
arquivo index.js.
Criar dentro do diretório reducers:
arquivo index.js.
Criar dentro do diretório store:
arquivo index.js.
Em src/index.js:
definir o Provider, <Provider store={ store }> , para fornecer os estados à todos os componentes encapsulados em <App /> .
Se a sua aplicação não terá outras páginas, não é necessário configurar as rotas. Caso contrário:
npm install react-router-dom@v5;
Em src/index.js:
definir o BrowserRouter, <BrowserRouter> .
No arquivo App.js:
definir o Switch, <Switch> ;
definir a Route, <Route> .
O BrowserRouter, o Switch e a Route são três componentes essenciais para trabalhar rotas em React.
Caso necessário:
criar o diretório components;
criar o diretório pages.
No arquivo store/index.js:
importar o rootReducer e criar a store;
configurar o Redux DevTools.
Na pasta reducers:
criar os reducers necessários;
configurar os exports do arquivo index.js.
Na pasta actions:
criar os actionTypes;
criar as actions necessárias.
Nos componentes:
criar a função mapStateToProps se necessário;
criar a função mapDispatchToProps se necessário;
fazer o connect se necessário.
#theend
