<template>
  <div>

    <index-banner/>

    <div class="halo-body">
      <div class="halo-left-content">
        <!-- 幻灯片 -->
        <div class="halo-carousel">
          <el-carousel :interval="5000" height="230px">
            <el-carousel-item v-for="item in carouselData.blogs"
                              :key="item.id"
                              @click.prevent="toBlogDetail(item.id)">
              <div class="halo-carousel-title">{{ item.title }}</div>
              <img class="post_bg"
                   :src=item.blogCover
                   :alt=item.title>
            </el-carousel-item>
          </el-carousel>
        </div>
        <!--文章-->
        <div class="halo-blogs-box">
          <div v-for="item in homeData.blogs"
               :key="item.id"
               class="blogs"
               @click="toBlogDetail(item.id)"
          >
            <div class="halo-blog-img">
              <img class="post_bg"
                   :src=item.blogCover
                   :alt=item.title>
              <p class="halo-blog-created">{{ item.created }}</p>
            </div>
            <div class="halo-blog-content">
              <h3 class="halo-blog-title">
                {{ item.title }}
              </h3>
              <p class="halo-blog-text">{{ item.description }}</p>
            </div>

          </div>
        </div>
        <!--分页-->
        <el-pagination class="halo-pagination"
                       background
                       layout="prev, pager, next"
                       :current-page="homeData.currentPage"
                       :page-size="homeData.pageSize"
                       :total="homeData.total"
                       @current-change="changePage"
        ></el-pagination>
      </div>
      <div class="halo-right-content">
        <div>
          <UserInfo></UserInfo>
        </div>
        <div></div>
        <div></div>
        <div></div>
        <div class="halo-sticky">

        </div>
      </div>
    </div>

    <!-- 回到顶部 -->
    <el-backtop  :bottom="100">

    </el-backtop>

  </div>
</template>

<script>
import homeData from "../hooks/homeData";
import carouselData from "../hooks/carouselData";
import UserInfo from "../components/Cards/UserInfo.vue"
import {useRouter} from "vue-router";
import IndexBanner from "../components/Banner/IndexBanner.vue";

export default {
  name: "Home",
  components: {UserInfo, IndexBanner},
  setup() {

    const router = useRouter()

    function toBlogDetail(id) {
      router.push({name: 'BlogDetail', params: {blogId: id}})
    }

    return {
      toBlogDetail,
      ...homeData(),
      ...carouselData()
    }
  }
}
</script>

<style lang="scss">

.halo-body {
  margin: 0 auto;
  padding: 1.5rem 1rem;
  max-width: 1024px;
  display: grid;
  grid-template-columns: 69% 29%;
  grid-gap: 2%;

  .halo-left-content {

    .halo-blogs-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-content: center;

      // 测试样式
      //border: solid 2px greenyellow;

      .blogs {
        margin-top: 20px;
        border-radius: 12px;
        box-shadow: 0 3px 8px 6px rgba(7, 17, 27, 0.06);
        background: rgba(255, 255, 255, 0.9);

        .halo-blog-content {
          cursor: pointer;

          display: flex;
          flex-direction: column;
          padding: 30px;

          .halo-blog-title {
            font-weight: 700;
            line-height: 1.6;
            font-size: 1.3rem;
            margin-bottom: 10px;

          }

          .halo-blog-text {
            display: -webkit-box;
            -webkit-box-orient: vertical;
            -webkit-line-clamp: 3;
            overflow: hidden;
            color: rgba(141, 140, 140, .856);
            font-size: .9rem;
            line-height: 160%;
          }

        }

        min-height: 100px;
        display: flex;
        overflow: hidden;

        .halo-blog-img {
          padding: 0;
          margin: 0;

          .halo-blog-created {
            position: absolute;
            z-index: 1;
            transform: translateY(-40px) translateX(10px);
            background: #ffffff;
            border-radius: 3px;
            width: 100px;
            text-align: center;
            opacity: 0.8;
          }

          img {
            width: 330px;
            height: 100%;
            padding: 0;
            margin: 0;
          }
        }
      }
    }

    .halo-pagination {
      text-align: center;
      margin-top: 20px;
    }

    .halo-carousel {
      cursor: pointer;

      .halo-carousel-title {
        margin: 15px;
        padding: 0 5px;
        position: absolute;
        background: #ffffff;
        border-radius: 3px;
      }

      .el-carousel__container {
        border-radius: 12px;
        overflow: hidden;

        img {
          width: 100%;
          padding: 0;
          margin: 0;
        }


        button {
          border-radius: 12px;
        }

        // 测试样式
        //border: solid;
      }

      .el-carousel__item h3 {
        color: #475669;
        font-size: 14px;
        opacity: 0.75;
        line-height: 150px;
        margin: 0;
        border-radius: 12px;
      }

      .el-carousel__item:nth-child(2n) {
        background-color: #99a9bf;
        overflow: hidden;
      }

      .el-carousel__item:nth-child(2n+1) {
        background-color: #d3dce6;
        overflow: hidden;
      }

    }
  }

  .halo-right-content {
    div:first-child {
      margin-top: 0;
    }

    & > div {
      min-height: 200px;
      width: auto;
      background: #ffffff;
      margin-top: 20px;
      border-radius: 10px;
    }

    .halo-sticky {
      top: 20px;
      position: sticky;
      background: #889DB8;
    }


  }

}

</style>