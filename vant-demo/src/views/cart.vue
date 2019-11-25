<template>
  <div class="cart">
    <van-checkbox-group class="card-commodity" v-model="checkedCommodity">
      <van-checkbox
        class="card-commodity_item"
        v-for="item in commodity"
        :key="item.id"
        :name="item.id"
      >
        <van-card
          :title="item.title"
          :desc="item.desc"
          :num="item.num"
          :price="formatPrice(item.price)"
          :thumb="item.thumb"
        />
      </van-checkbox>
    </van-checkbox-group>
    <van-submit-bar
      :price="totalPrice"
      :disabled="!checkedCommodity.length"
      :button-text="submitBarText"
      @submit="onSubmit"
    />
  </div>
</template>

<script>
import { Checkbox, CheckboxGroup, Card, SubmitBar, Toast } from "vant";

export default {
  components: {
    [Checkbox.name]: Checkbox,
    [CheckboxGroup.name]: CheckboxGroup,
    [Card.name]: Card,
    [SubmitBar.name]: SubmitBar,
    [Toast.name]: Toast
  },
  data() {
    return {
      checkedCommodity: ["1", "2", "3"],
      commodity: [
        {
          id: "1",
          title: "进口香蕉",
          desc: "约250g，2根",
          price: 200,
          num: 1,
          thumb:
            "https://img.yzcdn.cn/public_files/2017/10/24/2f9a36046449dafb8608e99990b3c205.jpeg"
        },
        {
          id: "2",
          title: "陕西蜜梨",
          desc: "约600g",
          price: 690,
          num: 2,
          thumb:
            "https://img.yzcdn.cn/public_files/2017/10/24/f6aabd6ac5521195e01e8e89ee9fc63f.jpeg"
        },
        {
          id: "3",
          title: "美国伽力果",
          desc: "约680g/3个",
          price: 2680,
          num: 3,
          thumb:
            "https://img.yzcdn.cn/public_files/2017/10/24/320454216bbe9e25c7651e1fa51b31fd.jpeg"
        }
      ]
    };
  },
  methods: {
    formatPrice(price) {
      return (price / 100).toFixed(2);
    },
    onSubmit() {
      Toast("点击结算");
    }
  },
  computed: {
    submitBarText() {
      const count = this.checkedCommodity.length;
      return "结算" + (count ? `(${count})` : "");
    },

    totalPrice() {
      return this.commodity.reduce(
        (total, item) =>
          total +
          (this.checkedCommodity.indexOf(item.id) !== -1 ? item.price : 0),
        0
      );
    }
  }
};
</script>

<style lang="scss">
.cart {
  &-commodity {
    padding: 10px 0;
    background-color: #fff;

    &_item {
      position: relative;
      background-color: #fafafa;
    }
  }
}
</style>