<template>
  <div class="details-container">
    <Map></Map>
    <div class="left-box">
      <general-title generalTitle="车辆信息"></general-title>
      <ul class="left-ul">
        <li class="left-li" v-for="(item, index) in items" :key="index">
          <span class="left-span1">{{ item.label }}</span>
          <span class="left-span2">{{ item.value }}</span>
        </li>
      </ul>
    </div>
    <div class="right-box">
      <general-title generalTitle="最近出入场所"></general-title>
      <ul class="left-ul">
        <li class="left-li" v-for="(item1, index1) in items1" :key="index1">
          <span class="left-span1">{{ item1.label }}</span>
          <span class="left-span2">{{ item1.value }}</span>
        </li>
      </ul>
      <general-title generalTitle="预警信息"></general-title>
      <ul class="left-ul">
        <li class="left-li" v-for="(item2, index2) in items2" :key="index2">
          <span class="left-span1">{{ item2.label }}</span>
          <span class="left-span2">{{ item2.value }}</span>
        </li>
      </ul>
      <general-title generalTitle="处置详情"></general-title>
      <el-form ref="form" :model="form" label-width="90px">
        <el-form-item label="是否违章">
          <el-radio-group v-model="form.radioVal">
            <el-radio label="是"></el-radio>
            <el-radio label="否"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="违章行为">
          <el-select :value="form.selectVal">
            <el-option
              v-for="(select, indexSelect) in options"
              :key="indexSelect"
              :label="select.label"
              :value="select.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="备注信息">
          <el-input v-model="form.inputVal"></el-input>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import Map from "./map.vue";
import GeneralTitle from "@/components/generalTitle.vue";
export default {
  components: {
    Map,
    GeneralTitle,
  },
  data() {
    return {
      reverse: true,
      items1: [
        {
          label: "场所名称",
          value: "奈儿美妆",
        },
        {
          label: "出场时间",
          value: "2021-09-10 12:05:38",
        },
      ],
      items: [
        {
          label: "车牌号码",
          value: "京A123456",
        },
        {
          label: "车牌种类",
          value: "蓝色",
        },
        {
          label: "车辆类型",
          value: "小型汽车",
        },
        {
          label: "车身颜色",
          value: "黑色",
        },
        {
          label: "发动机号",
          value: "123456",
        },
        {
          label: "车辆品牌",
          value: "奔驰",
        },
        {
          label: "所有人",
          value: "张三",
        },
        {
          label: "行车电话",
          value: "13123412341",
        },
      ],
      items2: [
        {
          label: "酒驾可能性",
          value: "99%",
        },
        {
          label: "卡口设备",
          value: "电警（DJ-001）",
        },
        {
          label: "抓拍时间",
          value: "2021-09-10 12:10:03",
        },
        {
          label: "预警地点",
          value: "执勤点地址",
        },
      ],
      form: {
        radioVal: "",
        selectVal: 0,
        inputVal: "醉酒后驾车",
      },
      options: [
        {
          label: "醉酒后驾车",
          value: 0,
        },
      ],
    };
  },
};
</script>

<style lang="scss">
.details-container {
  height: 100%;
  width: 100%;
  position: relative;
  color: #fff;
  ul,
  li {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .left-box {
    height: 100%;
    width: 420px;
    position: absolute;
    top: 0;
    left: 0;
    background-color: rgba(4, 5, 6, 0.7);
    z-index: 999;
    .left-ul {
      margin-top: 20px;
      .left-li {
        padding-left: 20px;
        line-height: 28px;
        span {
          font-size: 14px;
          display: inline-block;
        }
        .left-span1 {
          width: 100px;
          color: #9a9da1;
        }
      }
    }
  }
  .right-box {
    height: 100%;
    width: 420px;
    position: absolute;
    top: 0;
    right: 0;
    background-color: rgba(4, 5, 6, 0.7);
    z-index: 999;
    .left-ul {
      margin-top: 20px;
      margin-bottom: 20px;
      .left-li {
        padding-left: 20px;
        line-height: 28px;
        span {
          font-size: 14px;
          display: inline-block;
        }
        .left-span1 {
          width: 100px;
          color: #9a9da1;
        }
      }
    }
    .el-form {
      margin-top: 20px;
      .el-form-item {
        height: 28px;
        .el-form-item__content {
          input {
            height: 28px;
            width: 200px;
          }
          .el-input__inner {
            color: #fff;
            background-color: #384358;
            border-color: #fff;
          }
          .el-radio {
            color: #fff;
          }
        }
        // .el-select {
        //   .el-select-dropdown.el-popper {
        //     border-color: #040506;
        //     background-color: #040506;
        //   }
        // }
        .el-form-item__label {
          color: #9a9da1;
          font-size: 14px;
        }
      }
    }
  }
}
</style>