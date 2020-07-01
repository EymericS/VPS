# ReactJS

Official doc available [here](https://reactjs.org/)
Great youtube [video](https://www.youtube.com/watch?v=8T8oN-now9Y) from [Grafikart](https://www.grafikart.fr/)

## How to use

* Webpack Encore to manage assets / JS / CSS ....
  * Babel settings : `~/project$ yarn add @babel/preset-react --dev`
  * Webpack config : */webpack.config.js* **+** `.enableReactPreset()`
  * link CSS  `{{ encore_entry_link_tags('app') }}`
  * link JS : `{{ encor_entry_script_tags('app') }}`
* Install : `~/project$ yarn add react react-dom`
* Dependance JS : `~/project$ yarn` or `~/project$ npm install`
* Server assets : `~/project$ yarn run dev-server` or `~/project$ npm run dev-server`


## Custom elements

### The template code

In */templates/blog/post_show.html.twig* : **+** ` <post-comments data-post="{{ post.id }}" data-user="{{ app.user ? app.user : 0 }}> </post-comments> `

### The JSX code

In */assets/js//app.js* : **+** import './comments/CommentsElement.jsx`

In */assets/js/comments/Comment.jsx* : 
```JSX
import React, {useEffect} from 'react'
import {render} from 'react-dom'

function Comments () {
  const { items: comments, load, loading } = usePaginatedFetch( '/api/comments' )
  
  useEffect( () => {
    load()
  }, [])

  return <div>
    {loading && 'chargement ...
    {JSON.stringify(comments)}
    <button onClick={load}>Load comments</button>
  </div>
}

class CommentsElement extends HTMLElement {
  connectdCallback () {         /* connected ? */
    render(<Comments/>, this)
  }
  
  disconnectedCallback () {         /* disconnected ? */
    unmountComponentsAtNode(this)
  }
}

customElements.define('post-comments', CommentsElement)
```

## Hooks ?

In */assets/js/comments/hooks.js* :
```JSX
import {useState, useCallback} from 'react'

export function usePaginatedFetch (url) {
  const [loading, setLoading] = useState( false )
  const [items, setItems] = useState( [] )
  const load = useCallback( async fetch ( url, {
    setLoading( true )
    
    const response = await fetch ( url, {
      headers: {
        'Accept': 'application/ld+json'
      }
    })
    
    const responseData = await response.json()
    if ( response.ok ) {
      setItems( responseData['hydra:member'] )
    } else {
      console.errors( responseData )
    }
    
    setLoading ( false )
  }, [url])
  
  return {
    items,
    load,
    loading
  }
 ```   
 
 ## Form
 
 ```JS 
 constructor (props) {
  super(proprs)
  ...
  this.handleChange = this.handleChange.bind(this
 
 
 handleChange (e) {
  this.setState( {
   nom: e.target.value
  })
 
 /* React controlled field */
 <input type="text" id="nom" name="nom" value={this.state.nom} onChange={this.handleChange}/>
 /* React not controlled field */
 <input type="text" id="" name="" defaultValue="{this.state.nom}" onChange={this.handleChange}/>
 ```
 
 ## Form error type
 
 Around [58 min](https://www.youtube.com/watch?v=8T8oN-now9Y&t=58m00s)
    
# TODO / Search

- [x] react *hooks*
- [x] react **hooks** : `useState()`
- [ ] react **hooks** : `useEffect()`
- [ ] react **hooks** : `useRef()`
- [ ] **react** : `React.forwardRef()`
- [ ] **react** : `componetDidMount()`
- [ ] **react** : `componetWillUnmount()`
- [ ] **react** : pure component `React.memo` `extends React.PureComponent`
- [ ] react **hooks** : `useCallBack()` & `async`
- [ ] `avait fetch()`
- [ ] react custom component for relative time ( post )
- [ ] React.memo ( avoid too much reload on unchanged )
- [ ] context lose `this.someMethode.bind(this)`
- [ ] html `class=""` -> react `className=""`
- [ ] html `for=""` -> react `htmlFor=""`
- [ ] **react** *devTools* : on [firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
