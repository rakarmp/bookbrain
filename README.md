<h1 align=center>Bookbrain Light Astro</h1>

## Structure

.
├── src
│   ├── config
│   │   ├── config.json
│   │   ├── menu.json
│   │   ├── social.json
│   │   └── theme.json
│   ├── content
│   │   ├── about
│   │   │   └── index.md
│   │   ├── authors
│   │   │   ├── -index.md
│   │   │   
│   │   ├── pages
│   │   │   ├── 404.md
│   │   │   ├── contact.md
│   │   │   ├── elements.md
│   │   │   └── privacy-policy.md
│   │   ├── posts
│   │   │   ├── -index.md
│   │   │   
│   │   │   
│   │   │   
│   │   └── config.ts
│   ├── layouts
│   │   ├── components
│   │   │   ├── Logo.astro
│   │   │   ├── Pagination.astro
│   │   │   ├── Share.astro
│   │   │   ├── SimilarPosts.astro
│   │   │   ├── Social.astro
│   │   │   └── TwSizeIndicator.astro
│   │   ├── partials
│   │   │   ├── Footer.astro
│   │   │   └── Header.astro
│   │   ├── Authors.astro
│   │   ├── AuthorSingle.astro
│   │   ├── Base.astro
│   │   ├── Default.astro
│   │   ├── Posts.astro
│   │   ├── PostSingle.astro
│   │   └── Search.tsx
│   ├── lib
│   │   ├── utils
│   │   │   ├── dateFormat.ts
│   │   │   ├── readingTime.ts
│   │   │   ├── similarItems.ts
│   │   │   ├── sortFunctions.ts
│   │   │   ├── taxonomyFilter.ts
│   │   │   └── textConverter.ts
│   │   ├── contentParser.astro
│   │   └── taxonomyParser.astro
│   ├── pages
│   │   ├── authors
│   │   │   ├── page
│   │   │   │   └── [slug].astro
│   │   │   ├── index.astro
│   │   │   └── [single].astro
│   │   ├── categories
│   │   │   ├── [category].astro
│   │   │   └── index.astro
│   │   ├── page
│   │   │   └── [slug].astro
│   │   ├── tags
│   │   │   ├── index.astro
│   │   │   └── [tag].astro
│   │   ├── 404.astro
│   │   ├── about.astro
│   │   ├── contact.astro
│   │   ├── index.astro
│   │   ├── [regular].astro
│   │   └── search.astro
│   ├── styles
│   │   ├── base.scss
│   │   ├── buttons.scss
│   │   ├── components.scss
│   │   ├── navigation.scss
│   │   ├── style.scss
│   │   └── utilities.scss
│   └── env.d.ts
├── astro.config.mjs
├── LICENSE
├── netlify.toml
├── package.json
├── package-lock.json
├── postcss.config.js
├── README.md
├── tailwind.config.js
└── tsconfig.json



<!-- installation -->
## 🔧Installation

After downloading the template, you have some prerequisites to install. Then you can run it on your localhost. You can view the package.json file to see which scripts are included.

### ⚙️Install prerequisites (once for a machine)

- **Node Installation:** [Install node js](https://nodejs.org/en/download/) [Recommended LTS version]

### 🖥️Local setup

After successfully installing those dependencies, open this template with any IDE [[VS Code](https://code.visualstudio.com/) recommended], and then open the internal terminal of IDM [vs code shortcut <code>ctrl/cmd+\`</code>]

- Install dependencies

```
npm install
```

- Run locally

```
npm run dev
```

After that, it will open up a preview of the template in your default browser, watch for changes to source files, and live-reload the browser when changes are saved.

## 🔨Production Build

After finishing all the customization, you can create a production build by running this command.

```
npm run build
```