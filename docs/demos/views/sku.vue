<template>
  <demo-section>
    <demo-block :title="$t('basicUsage')">
      <div class="sku-container">
        <van-sku
          v-model="showBase"
          :sku="$t('sku').sku"
          :goods="$t('sku').goods_info"
          :goods-id="$t('sku').goods_id"
          :hide-stock="$t('sku').sku.hide_stock"
          :quota="$t('sku').quota"
          :quota-used="$t('sku').quota_used"
          :reset-stepper-on-hide="true"
          :reset-selected-sku-on-hide="true"
          :disable-stepper-input="true"
          @buy-clicked="handleBuyClicked"
          @add-cart="handleAddCartClicked"
        />
        <van-button type="primary" @click="showBase = true" block>{{ $t('basicUsage') }}</van-button>
      </div>
    </demo-block>

    <demo-block :title="$t('advancedUsage')">
      <div class="sku-container">
        <van-sku
          v-model="showCustomAction"
          :stepper-title="$t('stepperTitle')"
          :sku="$t('sku').sku"
          :goods="$t('sku').goods_info"
          :goods-id="$t('sku').goods_id"
          :hide-stock="$t('sku').sku.hide_stock"
          :show-add-cart-btn="true"
          :quota="$t('sku').quota"
          :quota-used="$t('sku').quota_used"
          :reset-stepper-on-hide="true"
          :initial-sku="initialSku"
          @buy-clicked="handleBuyClicked"
          @add-cart="handleAddCartClicked"
        >
          <template slot="sku-messages" />
          <template slot="sku-actions" slot-scope="props">
            <div class="van-sku-actions">
              <van-button bottom-action @click="handlePointClicked">{{ $t('button1') }}</van-button>
              <van-button type="primary" bottom-action @click="props.skuEventBus.$emit('sku:buy')">{{ $t('button2') }}</van-button>
            </div>
          </template>
        </van-sku>
        <van-button type="primary" @click="showCustomAction = true" block>{{ $t('advancedUsage') }}</van-button>
      </div>
    </demo-block>
  </demo-section>
</template>

<script>
import data from '../mock/sku';

export default {
  i18n: {
    'zh-CN': {
      sku: data['zh-CN'],
      stepperTitle: '我要买',
      button1: '积分兑换',
      button2: '买买买'
    },
    'en-US': {
      sku: data['en-US'],
      stepperTitle: 'Stepper title',
      button1: 'Button',
      button2: 'Button'
    }
  },

  data() {
    return {
      showBase: false,
      showCustomAction: false,
      initialSku: {
        s1: '30349',
        s2: '1193'
      }
    };
  },

  methods: {
    handleBuyClicked(data) {
      Toast(JSON.stringify(data));
    },
    handleAddCartClicked(data) {
      Toast(JSON.stringify(data));
    },
    handlePointClicked() {
      Toast('积分兑换');
    }
  }
};
</script>

<style lang="postcss">
.demo-sku {
  .sku-container {
    padding: 0 15px;
  }
}
</style>
