<template>
  <section class="post-detail-content">
    <div class="post-detail-content__header">
      <h1>{{ postDetail.title }}</h1>
      <h2>
        {{ postDetail.description }}
      </h2>
      <post-detail-info :info="postDetail.info" />
      <div
        class="post-detail-content__poster flex--column column--middle--center"
      >
        <figure
          v-if="postDetail.poster"
          class="flex--column column--middle--center"
        >
          <img :src="postDetail.poster" alt="" />
          <figcaption>Photo Title</figcaption>
        </figure>
        <placeholder-image v-else />
      </div>
    </div>
    <article class="post-detail-content__html" v-html="htmlContent()"></article>
    <hr class="hr-line" />
    <div class="post-detail-content__actions flex--row row--middle--center">
      <post-tags :tags="postDetail.tags" />
      <like-box />
    </div>
  </section>
</template>
<script>
import PostDetailInfo from '~/components/PostDetailInfo.vue'
import PlaceholderImage from '~/components/PlaceholderImage.vue'
import LikeBox from '~/components/LikeBox.vue'
import PostTags from '~/components/PostTags.vue'
export default {
  name: 'PostDetailContent',
  components: { PostDetailInfo, PlaceholderImage, LikeBox, PostTags },
  props: {
    postDetail: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.htmlContent()
  },
  methods: {
    htmlContent() {
      if (process.client && atob) {
        const output = atob(this.postDetail.content)
        return output
      }
    },
  },
}
</script>
<style lang="scss">
.post-detail-content {
  width: 100%;
  max-width: 840px;

  &__header {
    font-family: $roboto-slab;

    h1 {
      @include golden-text(44);
      font-weight: 600;

      @include small-device {
        @include golden-text(32);
      }

      @include extra-small-device {
        @include golden-text(28);
      }
    }

    h2 {
      @include golden-text(20);
      padding: 40px 0;
    }
  }

  &__poster {
    padding: 40px 0;

    min-height: 400px;

    figure {
      img {
        width: 100%;
      }

      figcaption {
        font-size: 13px;
        font-weight: 500;
        color: $gray-one;
        margin-top: 10px;
      }
    }
  }

  &__html {
    p,
    span {
      display: block;
      padding: 30px 0;
      @include golden-text(18);

      @include small-device {
        @include golden-text(18);
      }
    }
    h2,
    h3,
    h4,
    h5,
    h6 {
      font-weight: 500;
      display: block;
    }
    h2 {
      @include golden-text(30);

      @include small-device {
        @include golden-text(26);
      }
    }
    h3 {
      @include golden-text(28);

      @include small-device {
        @include golden-text(24);
      }
    }

    h4 {
      @include golden-text(25);

      @include small-device {
        @include golden-text(21);
      }
    }

    h5 {
      @include golden-text(22);

      @include small-device {
        @include golden-text(19);
      }
    }

    h6 {
      @include golden-text(19);

      @include small-device {
        @include golden-text(18);
      }
    }
  }

  &__actions {
    justify-content: space-between;
    margin-top: 40px;
  }
}
</style>
