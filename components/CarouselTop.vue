<template>
  <div class="carousel-top">
    <div class="carousel-top_body">
      <span class="carousel-top_body_btn">
        <button @click="back()" :disabled="visibleContent == 0">PREV</button>
      </span>
      <transition-group
        :name="transitionGroupName"
        class="carousel-top_body_images"
      >
        <img
          v-for="(item, index) in contents"
          v-show="visibleContent == index"
          :key="item.title"
          :src="item.image"
          class="carousel-top_body_image"
        />
      </transition-group>
      <span class="carousel-top_body_btn">
        <button
          @click="next()"
          :disabled="visibleContent == contents.length - 1"
        >
          NEXT
        </button>
      </span>
    </div>
    <div class="carousel-top_footer">
      <div
        class="carousel-top_footer_dot"
        v-for="(item, index) in contents"
        :key="item.title"
        :class="{ 'is-visible': visibleContent == index }"
      ></div>
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
          image: '/images/image1.jpg',
        },
        {
          title: 'Content 2',
          image: '/images/image2.jpg',
        },
        {
          title: 'Content 3',
          image: '/images/image3.jpg',
        },
        {
          title: 'Content 4',
          image: '/images/image4.jpg',
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

<style lang="scss" scoped>
.carousel-top {
  line-height: 20vh;
  height: 50vh;
  width: 50vw;
  overflow: hidden;
  position: relative;
  // display: flex;
  // justify-content: center;
  &_body {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    position: absolute;
    top: 0%;
    width: 100%;
    height: 100%;
    &_btn {
      height: 30vh;
      top: 0%;
      left: 0%;
      right: 0%;
      bottom: 0%;
      margin: auto;
    }
    &_images {
      display: flex;
      justify-content: center;
      align-items: center;
    }
    &_image {
      width: 40vw;
      height: 40vh;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }

  &_footer {
    align-items: center;
    display: flex;
    height: auto;
    justify-content: space-between;
    position: absolute;
    top: 85%;
    left: 38%;
    width: 24%;
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
  transform: translateX(100%);
}
.show-next-leave-to,
.show-prev-enter {
  transform: translateX(-100%);
}
</style>
