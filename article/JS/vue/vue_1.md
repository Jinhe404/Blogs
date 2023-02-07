# **1.Vuex概述**

### 1.1 组件之间共享数据

父向子传值： v-bind 属性绑定

子向父传值： v-bind 事件绑定

兄弟组件之间共享数据：EventBus

$on 接收数据的那个组件

$emit 发送数据的那个组件

### 1.2 Vuex

Vuex是实现组件全局状态（数据）管理的一种机制，可以方便的实现组件之间数据的共享。

![image-20230207191149863](C:\Users\JINHE1997\AppData\Roaming\Typora\typora-user-images\image-20230207191149863.png)

### 1.3 使用Vuex统一管理状态的好处

- 能够在vuex中集中管理共享的数据，易于开发和后期维护
- 能够高效的实现组件之间的数据共享，提高开发效率
- 存储到vuex中的数据都是响应式的，能够实时的保持数据与页面同步

什么样的数据是合格存储到Vuex中：

一般情况下、只有组件之间共享的数据，才有必要存储到vuex中；对于组件中私有的数据，依旧存储到组件自身的data中。

# **2.Vuex的基本使用**

1.安装vuex依赖包

```
npm install vuex -s
```

2.导入vuex包

```
import Vuex from 'vuex'
Vue.use(Vuex)
```

3.创建store对象

```
const store = new Vuex.store({
    // state 中存放的就是全局共享的数据
    state:{count:0}
}) 
```

4.将store对象挂载到vue实例中

```
new Vue ({
    el:'#app',
    render: h => h(app),
    router,
    // 将创建的共享数据对象，挂载到Vue实例中
    // 将所有的组件，就可以直接从store中获取全局的数据了
    store
})
```

如图项目中：

![image-20230207191406724](C:\Users\JINHE1997\AppData\Roaming\Typora\typora-user-images\image-20230207191406724.png)

main.js配置

![image-20230207191419165](C:\Users\JINHE1997\AppData\Roaming\Typora\typora-user-images\image-20230207191419165.png)

# **3.Vuex的核心概念**

### 3.1 核心概念概述

Vuex中的主要核心概念如下

- State
- Mutation
- Action
- Getter

### 3.2 State

State提供唯一的公共数据源，所有享的数据都要统一放到Store的State中进行存储。

```
// 创建store数据源，提供唯一的公共数据
const store = new Vuex.store({
    state:{count:0}
})
```

组件访问State中数据的第一种方式

```
this.$store.state.全局数据名称
```

组件访问State中数据的第二种方式

```
// 1.从vuex中按需导入mapState函数
import {mapState} from 'vuex'
```

通过刚才导入的mapState函数，将当前组件需要的全局数据，映射为当前组件的computed计算属性

```
// 2.将全局数据，映射为当前组件的计算属性
computed:{
    ...mapState(['count'])
}
```

### 3.3 Mutation

Mutation用于变更Store中的数据。

- - 只能通过mutation变更Store数据，不可以直接操作Store中的数据
- 通过这种方式虽然操作繁琐，但是可以集中监控所有数据的变化

```
// 定义Mutation
const store = new Vuex.Store({
    state:{
        count:0    
    },
    mutations:{
        add(state)
        // 变更状态
        state.count++    
    }
})
```

组件中调用

```
// 触发mutation
methods；{
    handle1(){
        // 触发mutations的第一种方式
        this.$store.commit('add')    
    }
}
```

可以在触发mutations时传递参数;

```
// 定义Mutation
const store = new Vuex.store({
    state：{
        count:0    
    },
    mutations；{
         addN（state,step){
             // 变更状态
             state.count += step         
         }   
    }
})
```

组件中调用

```
// 触发mutation
methods；{
    handle2(){
        // 在调用commit函数，
        // 触发mutations时携带参数
        this.$srore.commit('addN',3)    
    }
}
```

this.$store.commit()是触发mutations的第一种方式，触发mutations的第二种方式：

```
// 1.从vuex中按需导入mapMutations函数
import {mapMutations} from 'vuex'
```

通过刚才导入的mapMutations函数，映射为当前组建的methods函数

```
methods:{
    ...mapMutations(['add','addN'])
}
```

}

***不要在mutations函数中执行异步操作**

### 3.4 Action

Actons 用于处理异步任务。

如果通过异步操作变更数据，必须通过Action，而不能使用Mutation，但是在Action中还是通过触发Mutation的方式变更数据。

```
// 定义Action
const store = new Vuex.Store({
    mutations:{
        add(state){
            state,count++        
        }    
    },
    actions:{
        addAsync(context){
            setTimeout(() => {
                context.commit('add')            
            },1000)        
        }    
    }
})
```

组件中触发Actions

```
methods:{
    handle(){
        // 触发actions的第一种方式
        this.$store.dispatch('addAsync')    
    }
}
```

在Actions中，不能直接修改state中的数据

必须通过context.commit()触发某个mutation才行

只有Mutations中定义的函数，才有全部权力修改state中的数据

### 3.4 Action

触发actions异步任务是携带参数

```
// 定义Action
const store = new Vuex.Store({
    mutations:{
        addN(state,step){
            state,count += step      
        }    
    },
    actions:{
        addAsync(context，step){
            setTimeout(() => {
                context.commit('addN',step)            
            },1000)        
        }    
    }
})
```

在组件中调用

```
// 触发Action
methods:{
    handle(){
        this.$store.dispatch('addNAsync',5)    
    }
}
```

this.$store.dispatch()触发actions的第一种方式，触发actions的第二种方式：

```
// 1.从vuex中按需导入 mapActions函数
import {mapActions} from 'vuex'
```

通过刚才导入的mapAction函数，将需要的actions函数，映射为当前组件的methods方法：

```
methods:{
    ...mapActions({'addAsync','addNAsync'})
}
```

### 3.5 Getter

Getter用于对Store中的数据进行加工处理形成新的数据（无改变原始数据）

- - Getter可以对Store中已有的数据加工处理之后形成新的数据，类似Vue的计算属性。

- Store中数据发生变化，Getter的数据也会跟着变化



```
// 定义Getter
const store = new Vuex.Store({
    state:{
        count:0    
    },
    getters:{
        showNum:state => {
            return '当前最新的数量是【'+ state.count'】'        
        }    
    }
})
```

使用getters的第一种方式：

```
this.$store.getter.名称
```

使用getters的第二种方式

```
import {mapGetters} from 'vuex'

computed:{
    ...mapGetters(['showNum']})
}
```

