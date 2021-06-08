---
title: Create Vite App
author: https://github.com/sonjavanteese
date: Mai 22, 2021 - 09:24 
tags:
  - Template
  - ES6
categories:
  - Nwp-Components
---

# App Template

## Vite Tailwind

### Setup Vite

```bash
yarn create @vitejs/app vite-app-1 --template svelte
```

### Install Tailwind Postcss + Autoprefixer

```bash
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```
also
```
npm i autoprefixer@latest tailwindcss@latest postcss-import@latest cssnano@latest svelte-preprocess@latest postcss@latest -D
```


### Postcss Config

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
```

### Create Tailwind Config File

```bash
npx tailwindcss init
```

**or manually**

```javascript
module.exports = {
  purge: ['./src/**/*.svelte'],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```



## Add Markdown

```bash
npm i -D postcss-load-config svelte-preprocess
// Svelte adder
npx svelte-add mdsvex
```

### Svelte Config

```javascript
const { mdsvex } = require("mdsvex");
const mdsvexConfig = require("./mdsvex.config.cjs");
const preprocess = require("svelte-preprocess");
module.exports = {
	extensions: [".svelte", ...mdsvexConfig.extensions],
	preprocess: [
		mdsvex(mdsvexConfig),
		preprocess({
			postcss: true
		}),
	],
};
```




## Snap Sidebar

### Css

```css
.icon {
  align-self: center;
  display: inline-block;
  width: 1em;
  height: 1em;
  stroke-width: 0;
  stroke: currentColor;
  fill: currentColor;
}
html,
body {
  font-family: sans-serif;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.snap-content {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  height: auto;
  z-index: 12;
  overflow: auto;
  transition: left 0.3s ease-in-out;
}
.snap-drawers {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  width: auto;
  height: auto;
}
.snap-drawer {
  position: absolute;
  top: 0;
  right: auto;
  bottom: 0;
  left: auto;
  width: 265px;
  height: auto;
  overflow: auto;
  transition: width 0.3s ease;
}
.snap-drawer-left {
  left: 0;
  z-index: 10;
}
.snap-drawer-right {
  right: 0;
  z-index: 1;
}
.snapjs-left .snap-drawer-right,
.snapjs-right .snap-drawer-left {
  display: none;
}
.snapjs-expand-left .snap-drawer-left,
.snapjs-expand-right .snap-drawer-right {
  width: 100%;
}
.snap-header {
  display: flex;
  flex-direction: row;
  align-items: center;
  flex-wrap: nowrap;
  justify-content: space-between;
  border-bottom: 1px solid #ddd;
}
.snap-content {
  background-color: #fff;
  border: 1px solid #ddd;
}
.snap-header button {
  background-color: rgba(206, 206, 206, 0.12);
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  min-width: 50px;
  min-height: 50px;
  text-align: center;
  border: 1px solid rgba(0, 0, 0, 0);
}
.snap-header .title {
  display: flex;
  align-items: center;
  padding-top: 0;
  margin-top: 0;
  padding-bottom: 0;
  margin-bottom: 0;
}
.snap-header .button:active {
  background-color: rgba(206, 206, 206, 0.42);
}
.snap-drawers.left-open .snap-content {
  left: 266px;
}
.snap-drawers.right-open .snap-content {
  left: -266px;
}

```

### HTML

```html
<div class="snap-drawers">
  <div class="snap-drawer snap-drawer-left" id="left-drawer">
    <div>
      Sidebar Left
    </div>
  </div>
  <div class="snap-drawer snap-drawer-right" id="right-drawer">
    <div>
      Sidebar Right
    </div>
  </div>
  <div id="content" class="snap-content">
    <!-- Make sure all your bars are the first things in your <body> -->
    <header class="bar-title snap-header">
      <button class="button" id="toggle-left">Left</button>
      <h1 class="title">Ratchet</h1>
      <button class="button" id="toggle-right">Right</button>
    </header>
    <!-- Wrap all non-bar HTML in the .content div (this is actually what scrolls) -->
    <div class="content">
      <div>
        Content
      </div>
    </div>
  </div>
</div>

<script type="text/javascript">
const toggleSidebar = (el) => {
    let direction = el.dataset.sb;
    let wrap = document.querySelector(".snap-drawers");
    let isLeft = wrap.classList.contains("left-open");
    let isRight = wrap.classList.contains("right-open");
    if (direction === "left") {
        wrap.classList.remove("right-open");
        if (isLeft) {
            wrap.classList.remove("left-open");
        } else {
            wrap.classList.add("left-open");
        }
    } else if (direction === "right") {
        wrap.classList.remove("left-open");
        if (isRight) {
            wrap.classList.remove("right-open");
        } else {
            wrap.classList.add("right-open");
        }
    } else {
        wrap.classList.remove("left-open");
        wrap.classList.remove("right-open");
    }
};

const clickHandler = (event) => {
    let linkBtn = event.target.closest("a[href]");
    if (linkBtn) {
        event.preventDefault();
        console.log(linkBtn.getAttribute("href"));
    }
    let togSb = event.target.closest("[data-sb]");
    if (togSb) {
        console.log(togSb);
        toggleSidebar(togSb);
    }
};

document.addEventListener("click", clickHandler, false);

const loadIcons = () => {
    fetchXhr("temp/icons.html").then((data) => {
        let out = document.getElementById("iconlib");
    });
};

window.addEventListener("load", () => {
    console.log("Document Ready");
    // document.getElementById("svg-icons").innerHTML = iconlib();
    loadIcons();
});

</script>

```




### Example Tailwind

```javascript
 const { tailwindExtractor } = require("tailwindcss/lib/lib/purgeUnusedStyles");
// import { tailwindExtractor } from "tailwindcss/lib/lib/purgeUnusedStyles";
module.exports = {
	mode: "aot",
	purge: {
		content: [
			"./src/**/*.{html,js,svelte,ts}",
		],
		options: {
			defaultExtractor: (content) => [
				// If this stops working, please open an issue at https://github.com/svelte-add/tailwindcss/issues rather than bothering Tailwind Labs about it
				...tailwindExtractor(content),
				// Match Svelte class: directives (https://github.com/tailwindlabs/tailwindcss/discussions/1731)
				...[...content.matchAll(/(?:class:)*([\w\d-/:%.]+)/gm)].map(([_match, group, ..._rest]) => group),
			],
		},
		safelist: [/^svelte-[\d\w]+$/],
	},
	theme: {
        screens: {
            sm: '640px',
            md: '768px',
            lg: '1024px',
            xl: '1280px',
            '2xl': '1536px',
        },
        colors: {
            current: 'currentColor',
            transparent: 'transparent',
        
            black: '#000',
            white: '#fff',
        
            gray: {
                50: '#f9fafb',
                100: '#f3f4f6',
                200: '#e5e7eb',
                300: '#d1d5db',
                400: '#9ca3af',
                500: '#6b7280',
                600: '#4b5563',
                700: '#374151',
                800: '#1f2937',
                900: '#111827',
            },
            red: {
                50: '#fef2f2',
                100: '#fee2e2',
                200: '#fecaca',
                300: '#fca5a5',
                400: '#f87171',
                500: '#ef4444',
                600: '#dc2626',
                700: '#b91c1c',
                800: '#991b1b',
                900: '#7f1d1d',
            },
            yellow: {
                50: '#fffbeb',
                100: '#fef3c7',
                200: '#fde68a',
                300: '#fcd34d',
                400: '#fbbf24',
                500: '#f59e0b',
                600: '#d97706',
                700: '#b45309',
                800: '#92400e',
                900: '#78350f',
            },
            green: {
                50: '#ecfdf5',
                100: '#d1fae5',
                200: '#a7f3d0',
                300: '#6ee7b7',
                400: '#34d399',
                500: '#10b981',
                600: '#059669',
                700: '#047857',
                800: '#065f46',
                900: '#064e3b',
            },
            blue: {
                50: '#eff6ff',
                100: '#dbeafe',
                200: '#bfdbfe',
                300: '#93c5fd',
                400: '#60a5fa',
                500: '#3b82f6',
                600: '#2563eb',
                700: '#1d4ed8',
                800: '#1e40af',
                900: '#1e3a8a',
            },
            indigo: {
                50: '#eef2ff',
                100: '#e0e7ff',
                200: '#c3dafe',
                300: '#a5b4fc',
                400: '#818cf8',
                500: '#6366f1',
                600: '#4f46e5',
                700: '#4338ca',
                800: '#3730a3',
                900: '#312e81',
            },
            purple: {
                50: '#f5f3ff',
                100: '#ede9fe',
                200: '#ddd6fe',
                300: '#c4b5fd',
                400: '#a78bfa',
                500: '#8b5cf6',
                600: '#7c3aed',
                700: '#6d28d9',
                800: '#5b21b6',
                900: '#4c1d95',
            },
            pink: {
                50: '#fdf2f8',
                100: '#fce7f3',
                200: '#fbcfe8',
                300: '#f9a8d4',
                400: '#f472b6',
                500: '#ec4899',
                600: '#db2777',
                700: '#be185d',
                800: '#9d174d',
                900: '#831843',
            },
        },
        spacing: {
            px: '1px',
            px: '1px',
            '0': '0px',
            '0.5': '0.125rem',
            '1': '0.25rem',
            '1.5': '0.375rem',
            '2': '0.5rem',
            '2.5': '0.625rem',
            '3': '0.75rem',
            '3.5': '0.875rem',
            '4': '1rem',
            '5': '1.25rem',
            '6': '1.5rem',
            '7': '1.75rem',
            '8': '2rem',
            '9': '2.25rem',
            '10': '2.5rem',
            '11': '2.75rem',
            '12': '3rem',
            '14': '3.5rem',
            '16': '4rem',
            '20': '5rem',
            '24': '6rem',
            '28': '7rem',
            '32': '8rem',
            '36': '9rem',
            '40': '10rem',
            '44': '11rem',
            '48': '12rem',
            '52': '13rem',
            '56': '14rem',
            '60': '15rem',
            '64': '16rem',
            '72': '18rem',
            '80': '20rem',
            '96': '24rem'
        },
        backgroundColor: theme => ({
            ...theme('colors'),
            body: '#fff',
        }),
        backgroundPosition: {
            bottom: 'bottom',
            center: 'center',
            left: 'left',
            'left-bottom': 'left bottom',
            'left-top': 'left top',
            right: 'right',
            'right-bottom': 'right bottom',
            'right-top': 'right top',
            top: 'top',
        },
        backgroundSize: {
            auto: 'auto',
            cover: 'cover',
            contain: 'contain',
        },
        borderColor: theme => ({
            ...theme('colors'),
            DEFAULT: '#e5e7eb',
        }),
        borderRadius: {
            none: '0',
            sm: '0.125rem',
            DEFAULT: '0.25rem',
            md: '0.375rem',
            lg: '0.5rem',
            xl: '0.75rem',
            '2xl': '1rem',
            '3xl': '1.5rem',
            full: '9999px',
        },
        borderWidth: {
            DEFAULT: '1px',
            '0': '0',
            '2': '2px',
            '4': '4px',
            '8': '8px',
        },
        boxShadow: {
            sm: '0 1px 2px 0 rgba(0, 0, 0, 0.05)',
            DEFAULT: '0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06)',
            md: '0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)',
            lg: '0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05)',
            xl: '0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04)',
            '2xl': '0 25px 50px -12px rgba(0, 0, 0, 0.25)',
            inner: 'inset 0 2px 4px 0 rgba(0, 0, 0, 0.06)',
            none: 'none',
        },
        container: {
			center: true,
			padding: {
                DEFAULT: '1rem',
                sm: '1rem',
                md: '1rem',
                lg: '2rem',
                xl: '4rem',
              },
		},
        cursor: {
            auto: 'auto',
            DEFAULT: 'default',
            pointer: 'pointer',
            wait: 'wait',
            text: 'text',
            move: 'move',
            'not-allowed': 'not-allowed',
        },
        fill: {
            current: 'currentColor',
        },
        flex: {
            '1': '1 1 0%',
            auto: '1 1 auto',
            initial: '0 1 auto',
            none: 'none',
        },
        flexGrow: {
            '0': '0',
            DEFAULT: '1',
        },
        flexShrink: {
            '0': '0',
            DEFAULT: '1',
        },
        fontFamily: {
            body: 'ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"',
            heading: 'ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"',
            sans: 'ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"',
            serif: 'ui-serif, Georgia, Cambria, "Times New Roman", Times, serif',
            mono: 'ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace',
        },
        fontSize: {
            xs: '0.75rem',
            sm: '0.875rem',
            base: '1rem',
            lg: '1.125rem',
            xl: '1.25rem',
            '2xl': '1.5rem',
            '3xl': '1.875rem',
            '4xl': '2.25rem',
            '5xl': '3rem',
            '6xl': '3.75rem',
            '7xl': '4.5rem',
            '8xl': '6rem',
            '9xl': '8rem'
        },
        fontWeight: {
            hairline: '100',
            thin: '200',
            light: '300',
            normal: '400',
            medium: '500',
            semibold: '600',
            bold: '700',
            extrabold: '800',
            black: '900',
        },
        height: theme => ({
            auto: 'auto',
            ...theme('spacing'),
            full: '100%',
            screen: '100vh',
        }),
        inset: (theme, { negative }) => ({
            auto: 'auto',
            ...theme('spacing'),
            ...negative(theme('spacing')),
            '1/2': '50%',
            '1/3': '33.333333%',
            '2/3': '66.666667%',
            '1/4': '25%',
            '2/4': '50%',
            '3/4': '75%',
            full: '100%',
            '-1/2': '-50%',
            '-1/3': '-33.333333%',
            '-2/3': '-66.666667%',
            '-1/4': '-25%',
            '-2/4': '-50%',
            '-3/4': '-75%',
            '-full': '-100%',
        }),
        letterSpacing: {
            tighter: '-0.05em',
            tight: '-0.025em',
            normal: '0',
            wide: '0.025em',
            wider: '0.05em',
            widest: '0.1em',
        },
        lineHeight: {
            none: '1',
            tight: '1.25',
            snug: '1.375',
            normal: '1.5',
            relaxed: '1.625',
            loose: '2',
        },
        listStyleType: {
            none: 'none',
            disc: 'disc',
            decimal: 'decimal',
        },
        margin: (theme, { negative }) => ({
            auto: 'auto',
            ...theme('spacing'),
            ...negative(theme('spacing')),
        }),
        maxHeight: {
            full: '100%',
            screen: '100vh',
        },
        maxWidth: {
            none: 'none',
            xs: '20rem',
            sm: '24rem',
            md: '28rem',
            lg: '32rem',
            xl: '36rem',
            '2xl': '42rem',
            '3xl': '48rem',
            '4xl': '56rem',
            '5xl': '64rem',
            '6xl': '72rem',
            '7xl': '80rem',
            full: '100%',
            min: 'min-content',
            max: 'max-content',
            prose: '65ch',
        },
        minHeight: {
            '0': '0',
            full: '100%',
            screen: '100vh',
        },
        minWidth: {
            '0': '0',
            full: '100%',
        },
        objectPosition: {
            bottom: 'bottom',
            center: 'center',
            left: 'left',
            'left-bottom': 'left bottom',
            'left-top': 'left top',
            right: 'right',
            'right-bottom': 'right bottom',
            'right-top': 'right top',
            top: 'top',
        },
        opacity: {
            '0': '0',
            '5': '0.05',
            '10': '0.1',
            '20': '0.2',
            '25': '0.25',
            '30': '0.3',
            '40': '0.4',
            '50': '0.5',
            '60': '0.6',
            '70': '0.7',
            '75': '0.75',
            '80': '0.8',
            '90': '0.8',
            '95': '0.95',
            '100': '1',
        },
        order: {
            first: '-9999',
            last: '9999',
            none: '0',
            '1': '1',
            '2': '2',
            '3': '3',
            '4': '4',
            '5': '5',
            '6': '6',
            '7': '7',
            '8': '8',
            '9': '9',
            '10': '10',
            '11': '11',
            '12': '12',
        },
        padding: theme => theme('spacing'),
        placeholderColor: theme => theme('colors'),
        stroke: {
            current: 'currentColor',
        },
        textColor: theme => ({
            ...theme('colors'),
            body: '#484848',
        }),
        width: theme => ({
            auto: 'auto',
            ...theme('spacing'),
            '1/2': '50%',
            '1/3': '33.333333%',
            '2/3': '66.666667%',
            '1/4': '25%',
            '2/4': '50%',
            '3/4': '75%',
            '1/5': '20%',
            '2/5': '40%',
            '3/5': '60%',
            '4/5': '80%',
            '1/6': '16.666667%',
            '2/6': '33.333333%',
            '3/6': '50%',
            '4/6': '66.666667%',
            '5/6': '83.333333%',
            '1/12': '8.333333%',
            '2/12': '16.666667%',
            '3/12': '25%',
            '4/12': '33.333333%',
            '5/12': '41.666667%',
            '6/12': '50%',
            '7/12': '58.333333%',
            '8/12': '66.666667%',
            '9/12': '75%',
            '10/12': '83.333333%',
            '11/12': '91.666667%',
            full: '100%',
            screen: '100vw',
        }),
        zIndex: {
            auto: 'auto',
            '0': '0',
            '10': '10',
            '20': '20',
            '30': '30',
            '40': '40',
            '50': '50',
        },
    },
  variants: {
		extend: {},
	},
	plugins: [
        require('@tailwindcss/forms'),
    ],
};

```



