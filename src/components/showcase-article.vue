<style lang="scss" scoped>
.showcase {
  padding: {
    left: 15px;
    right: 15px;
  }
  float: left;
  .info {
    font-size: 12px;
    color: #909090;
    cursor: default;
  }
  .category {
    float: right;
    a {
      @extend .info;
      font-weight: bold;
      font-size: 13px;
    }
  }
  .img {
    position: relative;
    overflow: hidden;
    .news-img {
      width: 100%;
      transition: transform ease 0.8s;
      display: block;
    }
    &:hover {
      .meta {
        opacity: 1;
      }
      .news-img {
        transform: scale(1.05, 1.05);
      }
    }
  }
  .meta {
    position: absolute;
    top: 0;
    left: 0;
    width:100%;
    height: 100%;
    opacity: 0;
    transition: opacity ease 0.8s;
    color: #fff;
    background-color: rgba(246,105,95,0.9);
  }
  .author-info {
    margin: 0 auto;
    width: 180px;
    margin-top: 15%;
  }
  .author-img {
    display: block;
    width: 50px;
    height: 50px;
    border-radius: 50%;
  }
  .meta-nums {
    span {
      display: inline-block;
      &:first-child {
        margin-left: 20px;
      }
      &:last-child {
        float: right;
      }
    }
  }
  .text {
    height: 120px;
    overflow: hidden;
    h4 a{
      display: inline-block;
      height: 20px;
      position: relative;
      margin-top: 10px;
      font-size: 14px;
      color: #909090;
      font-weight: bold;
      max-height: 40px;
      overflow: hidden;
      line-height: 20px;
      padding-left: 15px;
      border-left: 5px solid #d9534f;
      &:hover {
        color: #686868;
      }
    }
  }
  .desc {
    color: #909090;
    font-size: 12px;
    overflow: hidden;
    max-height: 57px;
  }
}
.gray {
  background: rgba(62,62,62,0.3);
}
</style>

<template>
  <div class="showcase" :style="style">
    <div class="info" v-if="size!=='large'">
      <span class="time">{{data.lastTime}}</span>
      <span class="category">
        <!--:href="data.category.href"-->
        <a>
          {{data.category.name}}
        </a>
      </span>
    </div>
    <div class="img">
      <!-- http://localhost:8080/#/newsInfo -->
      <a :href="data.href"  class="block">
        <img :src="data.newsImage" class="news-img" alt="">
        <div class="meta">
          <div class="author-info">
            <img :src="data.authorImg" :alt="data.title" class="author-img middle">
            <p class="meta-nums" :style="`padding-top: ${spanTop}`">
              <span>赞 {{data.like}}</span>
              <span>{{data.comments}} Comments</span>
            </p>
          </div>
        </div>
      </a>
    </div>
    <div class="text">
      <h4>
        <a :title="data.title" :src="data.newsImage">{{data.title}}</a>
      </h4>
      <div class="desc">{{data.brief}}</div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      style: {width: '15px'},
      spanTop: ''
    }
  },
  props: {
    size: {
      type: String,
      default: 'small'
    },
    data: {
      type: Object,
      default () {
        return {
          lastTime: '',
          category: {
            name: '',
            href: ''
          },
          title: '',
          brief: '',
          newsImage: '',
          authorImg: '',
          href: '',
          like: '',
          comments: '',
          empty: false
        }
      }
    }
  },
  created () {
    if (this.size === 'middle') {
      this.style.width = '515px'
      this.style.height = '422px'
      this.spanTop = '40px'
    }
    if (this.size === 'small') {
      this.style.width = 1030 / 3 + 'px'
      this.style.height = '325px'
      this.spanTop = '20px'
    }
    if (this.size === 'large') {
      this.style.width = 1030 / 3 * 2 + 'px'
      this.style.height = '480px'
      this.spanTop = '55px'
    }
  }
}
</script>
