
# Supabase Setup

Install the npm package:

```bash
npm install -D @supabase/supabase-js
```

```
// npm install -D supabase-ui-svelte
```

DB.js

```javascript
import { createClient } from '@supabase/supabase-js'

// get keys via the settings page at https://app.supabase.io
// const supabaseClient = createClient('<your supabase url>', '<your supabase key>')
const supabase = createClient(
  import.meta.env.VITE_SUPABASE_URL,
  import.meta.env.VITE_SUPABASE_ANON_KEY
)

export default supabase
```
Usage 

```javascript
import supabase from "../db";
    export let params = {};
    const getPages = async () => {
        // return supabase.from('pages').select(`name, id`)
        // return supabase.from("pages").select();
        const { data, error } = await supabase.from('pages').select()
        return data;

    };
    let promise = getPages();
```

Add Data

```javascript
const addPage = async () => {
	const { data, error } = await supabase
	.from('pages')
	.insert({ 
		name: name, 
		path: path,
		icon: icon,
		option1: option1,
		order: order
	})
}
```

 
 Example
 
 ```javascript
async function signUp() {
  const {
    user,
    error
  } = await supabase.auth.signUp({
    email: 'sonjavanteese@ok.de',
    password: 'hoerzu36',
  })
  console.log(user, error);
}
```

 
---------

# Auth



Import the component:

```js
import Auth from 'supabase-ui-svelte'
```

Create a supabase client:

```js
import { createClient } from '@supabase/supabase-js'

// get keys via the settings page at https://app.supabase.io
const supabaseClient = createClient('<your supabase url>', '<your supabase key>')
```

Add the component anywhere on your page:

```js
<Auth {supabaseClient}/>
```

# Props

## `supabaseClient`

Required. This is the supabase client object. Call `createClient()` to get it.

## `view`

A `string` that sets which view to display.
Can be one of `sign_in` | `sign_up` | `magic_link` | `forgotten_password`. Default is `sign_in`.

## `providers`

An array of `string`. Can be any combination of `['facebook', 'google', 'twitter', 'github', 'gitlab', 'bitbucket', 'azure']`. When left empty, the social login option is not displayed.
Default is an empty array.

## `socialButtonSize`

A `string` that specifies the size of the social buttons. Can be one of `tiny` | `small` | `medium` | `large` | `xlarge`.
Default is `medium`.

## `socialLayout`

A `string` that specifies the layout direction of the social buttons. Valid options are `horizontal` or `vertical`.
Default is `vertical`.

## `socialColors`

A `boolean` that indicates whether the social buttons should use the brand's colors.
Default is `false`.

## `class`

A `string` of CSS classes to add to the outermost container.
Default is empty.

## `style`

A `string` of CSS attributes to add to the outermost container.
Default is empty.
