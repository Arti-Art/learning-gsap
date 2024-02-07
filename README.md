# First
- npm install
- npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
- npx tailwindcss init -p
- Configure Tailwind to remove unused styles in production (purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],)
- Include Tailwind in your CSS (@tailwind base; @tailwind components; @tailwind utilities;)
- ensure your CSS file is being imported in your ./src/main.js file (import './index.css')

<!-- Guide at https://v2.tailwindcss.com/docs/guides/vue-3-vite -->