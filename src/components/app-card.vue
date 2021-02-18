<template>
    <div
        class="memory-card"
        :data-framework="card.framework"
        @click="cardIsClicked(index)"
      >
        <img
          class="front-face"
          v-show="card.frontVisible"
          :src="card.imageFrontFace"
          alt="Aurelia"
        />
        <img
          class="back-face"
          v-show="card.backVisible"
          :src="card.imageBackFace"
          alt="JS Badge"
        />
      </div>
</template>

<script>
export default {
    name: 'appCard',
    props: {
        card: Object,
        index: Number
    },
    methods: {
        cardIsClicked(index) {
            this.$emit("cardIsClicked", index)
        }
    }
}
</script>