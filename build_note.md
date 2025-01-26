### 前端个人项目环境构建笔记

1.  **通过 Vite + Vue 搭建项目，选择 Vue 和 JavaScript**

    ```powershell
    npm create vite@latest
    ```

2.  **安装 Element Plus 文档：https://element-plus.org/zh-CN/ 版本：2.9.3**
    ```powershell
     npm install element-plus --save
     npm install -D unplugin-vue-components unplugin-auto-import
    ```
    - 添加下列代码到 vite.config.js 文件中
    ```jsx
    import { defineConfig } from 'vite' 
    import vue from "@vitejs/plugin-vue";
    import AutoImport from 'unplugin-auto-import/vite' 
    import Components from 'unplugin-vue-components/vite' 
    import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'
    export default defineConfig({
        plugins: [
            [vue()],
            AutoImport({
                resolvers: [ElementPlusResolver()],
            }),
            Components({
                resolvers: [ElementPlusResolver()],    
            }),
        ],
    })
    ```
3. **安装BootStrap5 文档：https://bootstrap.nodejs.cn/ 版本：5.3.3** 
    ```jsx
    npm i bootstrap@latest
    //我们还将安装 Popper，因为我们的下拉菜单、弹出窗口和工具提示的定位依赖于它。如果你不打算使用这些组件，则可以在此处省略 Popper。
    npm i --save-dev sass
    //安装额外的依赖。除了 Vite 和 Bootstrap 之外，我们还需要另一个依赖（Sass）来正确导入和打包 Bootstrap 的 CSS。
    ```
    - 在vite.config.js加入b5
        ```jsx
            import { defineConfig } from 'vite'    
            import vue from '@vitejs/plugin-vue'
            import { resolve } from 'path'
            // https://vite.dev/config/
            export default defineConfig({
              root: resolve(__dirname, 'src'),
              resolve: {
                alias: {
                  '~bootstrap': resolve(__dirname, 'node_modules/bootstrap'),
                }
              },
              build: {
                outDir: '../dist'
              },
              server: {
                port: 5173,
                host:true
              },
              plugins: [vue()],
            })

        ```
    - 在src/assets/style文件夹新建一个文件bootstrap5.scss ，引入bootstrap5样式：
        ```jsx
        @import "bootstrap/scss/bootstrap";
        ```
    - 在main.js引入b5
        ```jsx
        import '../src/assets/style/bootstrap5.scss'
        import * as bootstrap from 'bootstrap'
        ```
4. **Vite + Vue + Element Plus + BootStrap5**
    ```jsx
    import { defineConfig } from 'vite';
    import vue from '@vitejs/plugin-vue';
    import { resolve } from 'path';
    import AutoImport from 'unplugin-auto-import/vite';
    import Components from 'unplugin-vue-components/vite';
    import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';
    // https://vite.dev/config/
    export default defineConfig({
      root: resolve(__dirname, 'src'),
      resolve: {
        alias: {
          '~bootstrap': resolve(__dirname, 'node_modules/bootstrap'),
        },
      },
      build: {
        outDir: '../dist',
      },
      server: {
        port: 5173,
        host: true,
      },
      plugins: [
        [vue()],
        AutoImport({
          resolvers: [ElementPlusResolver()],
        }),
        Components({
          resolvers: [ElementPlusResolver()],
        }),
      ],
    });
    ```
