1. 什么时候用pinia?
答：状态管理是解决跨层级、跨组件、跨路由共享和同步数据的最佳工具，尤其在中大型 SPA 应用中不可或缺
材料：
- A good use case for Pinia is an application that is large, with properties being passed between many layers. Another use case would be a SPA that has very complex data that needs to be shared and manipulated by multiple parts of the application.
- 问：我的情况是属于想登录页面的id和身份信息放到header中，并且向main部分获取header中的信息。对于登录部分，properties 传递多层，可是我登录之后是redirect了，不是父子组件关系。后半部分是合适的。登录部分，是不是只能用状态管理呢？可是我的属于由登录页面到




这里确实需要记录登录状态，但是使用pinia的store记录。我已经创建stores/currentUser.js。// stores/userStore.js

import { defineStore } from 'pinia'

  

export const useCurrentUserStore = defineStore('currentUser', {

  state: () => ({

    currentUser: null,

  }),

  actions: {

    setUser(user) {

      this.currentUser = user

    },

    logout() {

      this.currentUser = null

    },

  },

})