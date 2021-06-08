# Gen Routes

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
