# Initialize Vite

`npm init vite@latest`

`npm install`

# Install tailwindcss and postcss

`npm install -D tailwindcss postcss autoprefixer`

# Create config files

## postcss.config.file
`
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
`
## tailwindcss.confing.file

`module.exports = {  
  content: [  
    "*.{html,js}"  
  ],  
  theme: {  
    extend: {},  
  },  
  plugins: [],  
}`  

# Add tailwind classes to .css file
@tailwind base;  
@tailwind components;  
@tailwind utilities;  

# Run the server

`npm run dev`