# Generate JS Files


## Spa Router Svelte

### Create Route  (RunJs)



```javascript
const data = [{
    name: "Start",
    path: "/",
    icon: "start",
    props: {
        header: "Nwp-Docs",
        info: "Nwp-Component Documentation",
        image: "https://nwp-cgn.de/img/poser/bgstreet01.jpg",
    },
}, {
    name: "Icons",
    path: "/icons",
    icon: "archiv",
    props: {
        header: "Nwp-Icons",
        info: "Icon and Button Libary",
        image: "https://nwp-cgn.de/img/poser/swsf1.jpg",
    },
}, {
    name: "Settings",
    path: "/settings",
    icon: "settings",
    props: {
        header: "Nwp-Settings",
        info: "Option and Settings",
        image: "https://nwp-cgn.de/img/poser/swsf2.jpg",
    },
}, ];

let a = (data) => data.map((data, id) => `import ${data.name} from './routes/${data.name}.svelte';
`).join("");
let b = (data) => data.map((data, id) => `
    '${data.path}': wrap({
        component: ${data.name},
        props: {
          pData: {
            header: '${data.props.header}',
            info: '${data.props.info}',
            image: '${data.props.image}'
          }}}),`).join("");

let t1 = (data) => `
import {wrap} from 'svelte-spa-router/wrap'
import NotFound from './routes/NotFound.svelte'
${a(data)}

export default { 
${b(data)} 
'*': NotFound,
}
`;

console.log(t1(data));
```






-------






### Data

<a href="https://beta5.objgen.com/" target="_blank">https://beta5.objgen.com/</a>

**Templ**

```javascript
name s = Nwp Docs
appconf
  appname s = Nwp-Docs
  sidebar b = true 
  dark b = true
pages[]
  name s = Start
  path s = /
  icon s = start
  props
    header s = Nwp-Docs
    info s = Nwp-Component Documentation
    image s = https://nwp-cgn.de/img/poser/bgstreet01.jpg
pages[]
  name s = Icons
  path s = /icons
  icon s = archiv
  props
    header s = Nwp-Icons
    info s = Icon and Button Libary
    image s = https://nwp-cgn.de/img/poser/swsf1.jpg
pages[]
  name s = Settings
  path s = /settings
  icon s = settings
  props
    header s = Nwp-Settings
    info s = Option and Settings
    image s = https://nwp-cgn.de/img/poser/swsf2.jpg
```

-------------------

## Output routes.js

```javascript
import {wrap} from 'svelte-spa-router/wrap'
import NotFound from './routes/NotFound.svelte'
import Start from './routes/Start.svelte';
import Icons from './routes/Icons.svelte';
import Settings from './routes/Settings.svelte';


export default { 

    '/': wrap({
        component: Start,
        props: {
          pData: {
            header: 'Nwp-Docs',
            info: 'Nwp-Component Documentation',
            image: 'https://nwp-cgn.de/img/poser/bgstreet01.jpg'
          }}}),
    '/icons': wrap({
        component: Icons,
        props: {
          pData: {
            header: 'Nwp-Icons',
            info: 'Icon and Button Libary',
            image: 'https://nwp-cgn.de/img/poser/swsf1.jpg'
          }}}),
    '/settings': wrap({
        component: Settings,
        props: {
          pData: {
            header: 'Nwp-Settings',
            info: 'Option and Settings',
            image: 'https://nwp-cgn.de/img/poser/swsf2.jpg'
          }}}), 
'*': NotFound,
}
```


