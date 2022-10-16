# Was ist Utility-First-CSS?
- postcss 的 plugin
- High-Level-Klassen durch Low-Level-Klassen ersetzt 
- Wenn Sie das Erscheinungsbild Ihrer Anwendung ändern müssen, müssen Sie nur den HTML-Code ändern, um Klassen hinzuzufügen/zu entfernen. Sie sollten das CSS der Klasse nicht ändern.
如果您需要更改应用程序的外观和感觉，您只需修改 HTML 以添加/删除类。您不应该修改类的 CSS。
- Code-Sharing-Philosophie 
# Installation
1. Install tailwindcss via npm, and create your tailwind.config.js file.
```
//Install tailwindcss
npm install -D tailwindcss  
//增加配置文件
npx tailwindcss init
```
2. 在tailwind配置中，我们需要让 Tailwind 知道要扫描哪些文件：  
Configure your template paths: tailwind.config.js 配置模板路径
```
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
3. Add the Tailwind directives to your CSS  将 Tailwind 指令添加到您的 CSS
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
4. Start the Tailwind CLI build process
```
npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch
```
5. Start using Tailwind in your HTML
```
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="/dist/output.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```
# Using with Preprocessors
npm install -D postcss-import  

```
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-import': {},
    tailwindcss: {},
    autoprefixer: {},
  }
}
```

# 自定义Tailwind
###  tailwind.config.js
```
module.exports = {
  content: [
    "./src/**/*.vue",
    "index.html"
  ],
  theme: {
  colors: {
    'ocean': '#16c0b0',
    'leaf': '#84cf6a',
    'mist': '#d8d8d8',
    'midnight': '#39495c',
    'cloud': '#ffffff',
  },
  screens: {
    'sm': '660px',
    'md': '860px',
    'lg': '1060px',
    'xl': '1260px',
    '2xl': '1460px',
  },
  extend: {
  },
  },
  plugins: [],
}
```
###  自定义Class @layer指令
#### src/assets/main.css
```
@layer utilities {

  .mist-border-2 {
    @apply border-2;
    @apply border-solid;
    @apply border-mist;
  }

    .btn-shading-bn {
    box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
      inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
      inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  }
}
```
### 代码重用模式

1. 按钮的样式（包括条件内的样式）：src/components/PrettyButton.vue

```
<script setup>
const { isActive } = defineProps({
  isActive: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['click'])
</script>

<template>
  <button 
    class="w-40 h-16 m-8 p-5 text-lg leading-none text-cloud text-center rounded-[5px] btn-shading-bn" 
    :class="isActive ? 
      ['bg-midnight', 'cursor-pointer'] : 
      ['bg-mist', 'cursor-not-allowed']"  
    :disabled="!isActive"
    @click="emit('click')"
  >
    <slot></slot>
  </button>
</template>
```
src/components/ProductDisplay.vue
```
<script setup>
import PrettyButton from './PrettyButton.vue'
...
</script>
...
<PrettyButton 
  :isActive="inStock"
  @click="addToCart"
>
  Add to Cart
</PrettyButton>
```
2. 可重用容器模式: src/components/ResponsiveWidth.vue
```
<template>
  <div class="w-[100%] md:w-[50%]">
    <slot></slot>
  </div>
</template>
```
ProductDisplay.vue
```
<script setup>
import ResponsiveWidth from './ResponsiveWidth.vue'
...
</script>
...
<div class="flex flex-row flex-wrap">
  <ResponsiveWidth>
    <img class = "w-[70%] m-10 p-4 md:mist-border-2"
      v-bind:src="image"
    />
  </ResponsiveWidth>
  <ResponsiveWidth>
    <div class="ml-2.5 md:ml-0">
      <h1>{{ title }}</h1>
      ...
    </div>
  <ResponsiveWidth>
```
