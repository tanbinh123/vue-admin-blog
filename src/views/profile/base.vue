<template>
  <div class="app-container">
    <div v-if="user">
      <el-row :gutter="20">

        <el-col :span="6" :xs="24">
          <user-card :user="user" :activity="activity" />
        </el-col>

        <el-col :span="18" :xs="24">
          <el-card>
            <el-tabs v-model="activeTab">
              <el-tab-pane label="用户信息" name="account">
                <account :user="user" />
              </el-tab-pane>
            </el-tabs>
          </el-card>
        </el-col>

      </el-row>
    </div>
  </div>
</template>

<script>
import UserCard from './components/UserCard'
import Account from './components/Account'
import { getWork } from '@/api/user'
import { getToken } from '@/utils/auth'
import { getInfo } from '@/api/user'
export default {
  name: 'Profile',
  components: { UserCard, Account },
  data() {
    return {
      user: {},
      activeTab: 'account',
      activity: []
    }
  },
  created() {
    this.getUser()
    this.getWork()
  },
  methods: {
    getUser() {
      getInfo(getToken()).then(response => {
        this.user = response.data
      })
    },
    getWork() {
      const that = this
      getWork(getToken()).then(response => {
        that.activity = response.data
      })
    }
  }
}
</script>
