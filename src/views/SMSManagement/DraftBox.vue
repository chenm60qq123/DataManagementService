<template>
  <div>
    <ToolBar>
      <el-button type="primary" icon="el-icon-plus" size="small">新建草稿</el-button>
      <div style="float: right">
        <el-input
                placeholder="搜索标题"
                size="small"
                style="width: 140px"
                v-model="searchParams.postTitle"
                clearable>
        </el-input>
        <el-select v-model="searchParams.postType" size="small" clearable placeholder="请选择分类" style="width: 140px">
          <el-option
                  v-for="(v,k) in $Config.postType"
                  :key="k"
                  :label="v"
                  :value="k">
          </el-option>
        </el-select>

        <el-select v-model="searchParams.postStatus" size="small" clearable placeholder="请选择状态" style="width: 120px">
          <el-option
                  v-for="(v,k) in $Config.postStatus"
                  :key="k"
                  :label="v"
                  :value="k">
          </el-option>
        </el-select>
        <el-button type="success" icon="el-icon-search" size="small" @click="refresh = !refresh"></el-button>
      </div>
    </ToolBar>
    <el-table
            :data="tableData3"
            border
            height="760"
            style="width: 100%">
      <el-table-column
          type="index"
          width="50"
          label="序号">
       </el-table-column>
      <el-table-column
              prop="date"
              label="日期"
              width="180">
      </el-table-column>
      <el-table-column
              prop="name"
              label="短信内容"
              >
      </el-table-column>
      <el-table-column
              label="操作"
              :render-header="tableAction"
              width="150">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)" type="success" icon="fa fa-paper-plane-o" size="small" circle></el-button>
          <el-button @click="handleClick(scope.row)" type="primary" icon="el-icon-edit" size="small" circle></el-button>
          <el-button @click="handleClick(scope.row)" type="danger" icon="el-icon-delete" size="small" circle></el-button>
        </template>
      </el-table-column>
    </el-table>
    <div class="block">
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[50,100, 200, 300, 400]"
      :page-size="50"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400">
    </el-pagination>
  </div>
  </div>
</template>

<script>
  import ToolBar from '~/components/ToolBar/ToolBar.vue';
  import HelpHint from '~/components/HelpHint/HelpHint.vue';
  export default {
    data() {
      return {
        searchParams:{
            postTitle:'',
            postType:'',
            postStatus:'published',
        },
        tableData3: [{
          date: '2016-05-03',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-02',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-04',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-01',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-08',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-06',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }, {
          date: '2016-05-07',
          name: 'Lorem ipsum dolor sit amet,',
          address: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores fugit in quae vero. Adipisci blanditiis dignissimos eum facere laudantium quasi ratione repellat vitae! Alias consequatur dolores enim neque similique unde.'
        }]
      }
    },
    methods: {
      handleClick(row) {
        this.$alert(row, '标题名称', {
          confirmButtonText: '确定',
          callback: action => {
          }
        });
      },
      tableAction(){
        return this.$createElement('HelpHint',{
          props:{
            content:'发送短信 / 编辑短信 / 删除短信'
          }
        },'操作');
      },
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      }
    },
    components: {
        ToolBar,HelpHint
    }
  }
</script>