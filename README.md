# VnodeLb
大数据列表性能优化

#
# VnodeLb 使用说明
    main.js
      import Vue from 'vue';
      import VnodeLb from 'VnodeLb';
      Vue.use(VnodeLb);
      
    App.vue
      <VnodeLb :luky-person.sync="lukyPerson" :item-height="itemHeight" :s-cro="sCro" :starts-cro="startsCro" :over-flow="overFlow">
        <template v-slot="vData">
          <li v-for="item in vData.vDota" :key="item.id" class="iztVnode-item" :style="{ height: itemHeight + 'px',lineHeight: itemHeight + 'px' }">
            <span class="iztVnode-clomn1">{{ item.who }}</span>
            <span class="iztVnode-clomn2">获得</span>
            <span class="iztVnode-clomn3">{{ item.name }}</span>
          </li>
        </template>
      </VnodeLb>

      <script>
          export default {
            data() {
              return {
                itemHeight: 40, // 滚动行高度 默认50
                sCro: 1, // 默认为0:禁止自动上下滚动
                startsCro: 0, // 控制什么时候开始
                overFlow: 1, // 不允许手指或者鼠标滑动  默认1

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
      </script>

# 参数说明
支持自动无限滚动，支持自动与手指滑动混合模式

    itemHeight: 40 // 滚动行高度 默认50
    sCro: 1, // 默认为0:禁止自动上下滚动
    startsCro: 0, // 控制什么时候开始
    overFlow: 1, // 不允许手指或者鼠标滑动  默认1
    
@send 点击改变startsCro的值控制是否开始滚动
  
