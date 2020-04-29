大数据列表性能优化之虚拟列表

## 使用

npm install vnodelb -S

main.js

  ```js
  import Vue from 'vue';
  import VnodeLb from 'vnodelb';
  Vue.use(VnodeLb);
  ```

App.vue
```html
  <VnodeLb :luky-person.sync="lukyPerson" :config="config">
      <template v-slot="vData">
       <!-- 数据渲染列表 -->
        <li v-for="item in vData.vDota" :key="item.id" class="iztVnode-item" :style="{ height: vData.config.itemHeight + 'px',lineHeight: vData.config.itemHeight + 'px' }">
          <span class="iztVnode-clomn1">{{ item.who }}</span>
          <span class="iztVnode-clomn2">获得</span>
          <span class="iztVnode-clomn3">{{ item.name }}</span>
        </li>
        <!-- 数据渲染列表 -->
      </template>
    </VnodeLb>
  ```
  ```js
  
      export default {
        data() {
          return {
            config: {
                itemHeight: 40, // 滚动行高度 默认50
                sCro: 1, // 默认为0:禁止自动上下滚动
                startsCro: 1, // 控制什么时候开始 1
                overFlow: 1 // 0不允许手指或者鼠标滑动  默认1
              },

            // 获奖记录
            lukyPerson: [
                {
                  id:256,
                  who: 'LSIJEGKILENKW',
                  name: '升星宝石'，
                  ...
                }
              ]
          };
        }
      }
  
```
> 当前中文版本暂不提供打包发行版, 可以直接以开发模式启动或自行打包.

## 参数说明

支持自动无限滚动，支持自动与手指滑动混合模式

```bash
itemHeight: 40 // 滚动行高度 默认50
sCro: 1, // 0:禁止自动上下滚动 默认为1
startsCro: 1, // 控制什么时候开始 默认1, 0为停止
overFlow: 1, // 不允许手指或者鼠标滑动  默认1
```

如果你不想通过克隆的方式, 你可以 [下载源码](https://github.com/xiyu-526/VnodeLb).

