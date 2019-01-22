<template>
  <div class="carousel-top">
    <div class="carousel-top_content">
      <span>
        <buton>prev</buton>
      </span>
      <span>
        <transition-group :name="transitionGroupName">
          <div
            v-for="(item, index) in contents"
            v-show="visibleContent == index"
            :style="{ backgroundColor: item.bg_color }"
            :key="item.title"
            class="carousel-top_body"
          >
            {{ item.title }}
          </div>
        </transition-group>
      </span>
      <span></span>
    </div>
    <div class="carousel-top_footer">
      <button @click="back()" :disabled="visibleContent == 0">PREV</button>
      <div
        class="carousel-top_footer_dot"
        v-for="(item, index) in contents"
        :key="item.title"
        :class="{ 'is-visible': visibleContent == index }"
      ></div>
      <button @click="next()" :disabled="visibleContent == contents.length - 1">
        NEXT
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      contents: [
        {
          title: 'Content 1',
          bg_color: '#7bbff9',
        },
        {
          title: 'Content 2',
          bg_color: '#f16972',
        },
        {
          title: 'Content 3',
          bg_color: '#20d2a3',
        },
      ],
      transitionGroupName: 'show-next',
      visibleContent: 0,
    }
  },
  methods: {
    back() {
      this.transitionGroupName = 'show-prev'
      this.visibleContent--
    },
    next() {
      this.transitionGroupName = 'show-next'
      this.visibleContent++
    },
  },
}
</script>

<style lang="scss">
.carousel-top {
  height: 50vh;
  width: 80vh;
  overflow: hidden;
  position: relative;
  &_body {
    color: #fff;
    height: 80%;
    left: 0;
    line-height: 40vh;
    position: absolute;
    text-align: center;
    top: 0%;
    left: 0%;
    right: 0%;
    bottom: 0%;
    margin: auto;
    width: 80%;
  }
  &_footer {
    align-items: center;
    display: flex;
    height: 45vh;
    justify-content: space-between;
    position: absolute;
    top: 50%;
    left: 10%;
    width: 80%;
    &_dot {
      background-color: #abc2ce;
      border-radius: 50%;
      height: 6px;
      width: 6px;
      &.is-visible {
        background-color: #7b94f9;
      }
    }
  }
}

// 進むトランジションと戻るトランジションをそれぞれ用意
.show-next-enter-active,
.show-next-leave-active,
.show-prev-enter-active,
.show-prev-leave-active {
  transition: all 0.4s;
}
.show-next-enter,
.show-prev-leave-to {
  transform: translate(100%);
}
.show-next-leave-to,
.show-prev-enter {
  transform: translateX(-100%);
}
</style>
