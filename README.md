# path-way-to-react-hooks
Repositório com informações e exemplos sobre a feature Hooks do React

## useState
Um exemplo de um contador de acrescentar/decrementar 

```js
import React, { useState } from "react"
...

function Counter1() {
  const [count, setCount] = useState(0)

  return (
      <Container className="text-left">
        <h1 className="mt-5">Count: {count}</h1>
        <div>
          <Button
            className="d-inline-block mr-2"
            onClick={() => setCount(count + 1)}
          >
            +
          </Button>
          <Button
            className="d-inline-block"
            onClick={() => setCount(count - 1)}
          >
            -
          </Button>
        </div>
        <Button className="d-block mt-2" onClick={() => setCount(0)}>
          Reset
        </Button>
      </Container>
  )
}

export default Counter1
```
### Descrição

- Começamos importando `useState` do react. Faça um componente funcional e use o `useState()`, ele é usado para declarar uma variável no state ee pode ser inicializada com qualquer tipo de valor. Como vemos abaixo, usamos de destructuring no valor de retorno do `useState`.

```js
const [count, setCount] = useState(0)
```

- O primeiro valor, `count` nesse caso, é o valor atual do state (como this.state) e o segundo valor `setCount` é uma função usada para fazer o update do state. O valor `0` passado por parametro nessa função atribuio esse valor para a variável `count`.


## useEffect
Exemplo usando useEffect

```js
import React, { useState, useEffect } from "react"
...

function Counter2() {
  const [count, setCount] = useState(0)

  useEffect(() => {
    document.title = `You clicked ${count} times`
  })

  return (
      <Container className="mt-3 text-left">
        <h1 className="mt-5">You clicked {count} times</h1>
        <div>
          <Button
            className="d-inline-block mr-2"
            onClick={() => setCount(count + 1)}
          >
            Click me
          </Button>
        </div>
      </Container>
  )
}
```

### Descrição

- Como mostrado anteriormente no primeiro exemplo importando `useState`, precisamos importar `useEffect()` do react. A funcão `useEffect()` é usada como um gatilho para outras funções.

- useEffect é similar ao componentDidMount e componentDidUpdate do lifecycle do React.

- Portanto, sempre quado o botão for clicado o titulo da página sera modificado com a quantidade de cliques no botão.

<a href="https://codesandbox.io/s/42r4rj4r29">Os dois exemplos acima no CodeSandbox</a>

## useContext
Exemplo usando useContext

```js
import React, { useContext } from "react"

const TestContext = React.createContext()

const ShowValues = () => {
  const value = useContext(TestContext)
  return <h1 className="mt-5">{value}, value from provider</h1>
}

const UseContextExample = () => {
  return (
      <TestContext.Provider value={"Teste value"}>
        <ShowValues />
      </TestContext.Provider>
  )
}
```

### Descrição

- Precisamos importar o `useContext` do react, no exemplo acima `TestContext` é criado usando `React.createContext()`. Foi usado o TestContext.Provider no componente funcional e uma propriedade `value` com o valor "Teste value", isso significa que qualquer componente dentro dele tem acesso a essa variável

- Para utilizarmos esse valor, foi criada a função `ShowValues()` na qual fa a chamada para `useContext` passando `TextContext` como parametro.

- Em seguida, passamos no contexto do objeto o que temos no `React.createContext` e ele automaticamente passa o valor para o componente filho. Quando o valor do Provider é atualizado esse Hook irá disparar um rerender com o valor do contexto mais recente.

## useRef
Exemplo de uso do hook useRef
Refs nos dão uma forma para acessar elementos criados no método `render()`

```js
import React, { useRef, useState } from "react"
...

const UseRefExample = () => {
  let [name, setName] = useState("dead")
  
  // useRef() retorna um ref object
  let nameRef = useRef()

  const submitButton = () => setName(nameRef.current.value)

  return (
    <Container className="mt-5">
      <h2 className="text-left">Username: {name}</h2>
      <form class="form-inline">
        <div>
          <input
            className="form-control"
            ref={nameRef}
            placeholder="Enter username"
            type="text"
          />
          <Button className="ml-2" type="button" onClick={submitButton}>
            Submit
          </Button>
        </div>
      </form>
    </Container>
  )
}

```

### Descrição

- No exemplo acima, nós usamos o `useRef()` hook em conjunto com `useState()` para renderizar o valor da input na tag h2.

- O ref é instanciado na variável `nameRef`. A variável `nameRef` pode então ser usada na input. Essencialmente, isso significa que o conteúdo da input estará acessivel por meio dessa referência.

- O botão tem um event handler chamado no click inocando a função `submitButton`, nessa função é chamada da função `setName` (criada com useState).

- Como fizemos com `useState` hooks anteriormente, setName será usada para setar a variável no state (`name`). Para extrair o nome da input nos captamos ele através da `nameRef` desse modo: `nameRef.current.value`.

- Outra coisa a notar sobre o uso da função `useRef` é que ela pode ser usado para mais de um atributo ref.

<a href="https://codesandbox.io/s/k5v954ko5o">Os dois exemplos acima no CodeSandbox</a>

// Todo - exemplo de CRUD usando hooks, comportamento consumindo APIs, useFetch...

