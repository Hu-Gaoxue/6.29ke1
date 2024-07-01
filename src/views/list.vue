<template>
  <div class="list-comp">
    

    <h1>同学列表</h1>
    <div class="tool-bar">
      <button class="add-btn" type="primary" @click="showFlag = true">新增</button>
    </div>
    <ul>
      <<a-modal v-model:open="open" title="Basic Modal" @ok="handleOk">
      <span class="No">序号</span>
        <span class="study-code">学号</span>
        <span class="name">姓名</span>
        <span class="year">年龄</span>
        <div class="operation">操作</div>
    </a-modal>
      <li v-for="(item, index) in list" :key="item.id">
        <span class="No">{{ index + 1 }}.</span>
        <span class="study-code">{{ item.id }}</span>
        <span class="name">{{ item.userName }}</span>
        <span class="year">{{ item.age }}</span>
        <div class="operation">
          <button @click="deleteUser(index)">删除</button>
          <button @click="editUser(index)">编辑</button>
          <button @click="getYourName(item.id)">问名字</button>
        </div>
      </li>
    </ul>

    <div class="pop-blank" v-if="showFlag">
      <h2>{{isEdit ? '编辑同学' : '新增同学'}}</h2>
      <div class="blank-body">
        <div class="blank-item">
          <span>学号</span>
          <input type="text" v-model="studyNum">
        </div>
        <div class="blank-item">
          <span>姓名</span>
          <a-avatar shape="square" size="small">
        <template #icon><UserOutlined /></template>
      </a-avatar>
          <input type="text" v-model="name">
        </div>
        <div class="blank-item">
          <span>年龄</span>
          <input type="text" v-model="year">
        </div>
      </div>
      <div class="footer">
        <button type="primary" @click="showFlag = false">取消</button>
        <button type="primary" @click="submitFn">确定</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue';
import { UserOutlined } from '@ant-design/icons-vue';

// const showModal = () => {
//   open.value = true;
// };

const handleOk = (MouseEvent) => {
  console.log(e);
  open.value = false;
};

let showFlag = ref(false);
let isEdit = ref(false);
let curIdx = ref(0);

let studyNum = ref(0);
let name = ref('');
let year = ref(0);
let list = reactive([
  {
    id: 210812005,
    userName: '胡高雪',
    age: 18
  },
  {
    id: 210812008,
    userName: '小刘',
    age: 18
  },
  {
    id: 210812000,
    userName: '小王',
    age: 18
  }
]);

const deleteUser = index => {
  list.splice(index, 1);
};

const editUser = index => {
  isEdit.value = true;
  curIdx.value = index;
  const item = list[index];
  // item.age = 22;
  // todo: 拿到的item信息填入弹窗对应的输入框里
  studyNum.value = item.id;
  name.value = item.userName;
  year.value = item.age;
  showFlag.value = true;
};

const submitFn = () => {
  if (isEdit.value) { // 编辑
    list[curIdx.value] = {
      id: studyNum.value,
      userName: name.value,
      age: year.value
    }
  } else { // 新增
    list = [{
      id: studyNum.value,
      userName: name.value,
      age: year.value
    }, ...list];
  }
  showFlag.value = false;
  // alert(`新增的同学学号是：${studyNum.value};姓名是：${name.value};年龄是：${year.value}`);
}

const getYourName = id => {
  const student = list.find(item => item.id === id);
  alert(student.userName);
};





// import { Button } from 'ant-design-vue';
//   const ButtonGroup = Button.Group=()=>{
  
//       AButton: Button,
//       AButtonGroup: ButtonGroup,
//   };

</script>

<style lang="less" scoped>
.list-comp {
  text-align: left;
}
h1 {
  text-align: center;
}
.tool-bar {
  display: flex;
  justify-content: flex-end;
  .add-btn {
    background-color: rgba(172, 200, 255, 0.48);
    color: #e29494;
    width: 90px;
    margin-right: 24px;
  }
}
ul {
  padding-left: 0;
  padding: 0 24px;
  text-align: center;
}
.pop-blank {
  position: absolute;
  background-color: #a67d7d;
  border-radius: 8px;
  left: 50%;
  top: 50%;
  width: 50%;
  height: 50vh;
  transform: translate(-50%, -50%);
  padding: 24px;
  border: 1px solid rgba(252, 78, 78, 0.4);
    display: flex;
    flex-direction: column;
  h2 {
    text-align: center;
  }
  .blank-body {
    flex-grow: 1;
    flex-shrink: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    .blank-item {
      height: 72px;
      font-size: 24px;
      display: flex;
      span {
        margin-right: 12px;
        width: 60px;
      }
      input {
        height: 36px;
        flex-grow: 1;
        flex-shrink: 1;
        font-size: 16px;
        // width: 100%;
      }
    }
  }
  .footer {
    // position: absolute;
    display: flex;
    justify-content: flex-end;
    width: 100%;
    button {
      background-color: #1677FF;
      color: #8d5252;
    }
    & > button:nth-child(1) {
      margin-right: 12px;
      background-color: #ffffff;
      border: 1px solid #1677FF;
      color: #1677FF;
    }
  }
}
li {
  list-style: none;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  // margin-bottom: 24px;
  height: 64px;
  border-bottom: 1px solid rgba(240, 106, 106, 0.7);
  &:nth-child(1) {
    color: rgb(167, 201, 231);
    background-color: rgba(92, 142, 242, 0.48);
  }
  .No {
    width: 18%;
  }
  .study-code {
    width: 18%;
  }
  .name {
    width: 18%;
  }
  .year {
    width: 18%;
  }
  .operation {
    flex-grow: 1;
    display: flex;
    justify-content: space-around;
    & > button {
      background-color: #314659;
      color: #a96464;
      width: 90px;
    }
  }
}
</style>
