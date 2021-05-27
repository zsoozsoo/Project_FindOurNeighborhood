<template>
  <div>
    <div class="position-relative">
      <!-- shape Hero -->
      <section class="section-shaped my-0 back">
        <div class="shape shape-style-1 shape-default shape-skew">
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="container shape-container d-flex">
          <div class="col px-0">
            <div class="row">
              <div class="col-lg-6">
                <h1 class="display-3 text-secondary">공지사항</h1>
                <p class="lead text-secondary">
                  이곳에서 공지사항을 확인해주세요!!
                </p>
                <div class="btn-wrapper">
                  <base-button
                    tag="a"
                    type="secondary"
                    class="text-white"
                    variant="primary"
                    @click="movePage"
                  >
                    게시물 등록
                  </base-button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
      <!-- 1st Hero Variation -->
    </div>

    
    <div v-if="boards.length">
      <!-- <marquee-text> -->
      <section class="section section-lg pt-lg-0 mt--200">
        <div class="container">
          <div class="row justify-content-center">
            <div class="col-lg-12">
              <div class="row row-grid">
                <list-row
                  v-for="(board, index) in boards"
                  :key="`${index}_items`"
                  :no="board.no"
                  :title="board.title"
                  :writer="board.writer"
                  :regtime="board.regtime"
                  :write_type="board.write_type"
                />
                <!--   
                            <div class="col-lg-4">
                                <card class="border-0" hover shadow body-classes="py-5">
                                    <icon name="ni ni-check-bold" type="primary" rounded class="mb-4">
                                    </icon>
                                    <h6 class="text-primary text-uppercase"><router-link :to="`board/view?no=${no}`" class="fontToWhite">{{ title }}</router-link></h6>
                                    <p class="description mt-3">{{writer}}</p>
                                    <p class="description mt-3">{{getFormatDate(regtime)}}</p>
                                    <base-button tag="a" href="#" type="primary" class="mt-4">
                                        View detail
                                    </base-button>
                                </card>
                            </div>
                            -->
              </div>
            </div>
          </div>
        </div>
      </section>
       <!-- </marquee-text> -->
    </div>
 
    <div v-else class="text-secondary">
      <section class="section section-lg pt-lg-0 mt--200">
        <div class="container">게시글이 없습니다.</div>
      </section>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapState } from "vuex";
import ListRow from "@/components/board/include/ListRow.vue";
//import moment from "moment";
// import MarqueeText from 'vue-marqee-text-component';

export default {
  name: "boardList",
  components: {
    ListRow,
    //  MarqueeText,
    // BoardCreate,
  },
  data() {
    return {
      write_type: this.write_type,
    };
  },

  computed: {
    ...mapGetters(["boards"]),
    ...mapState(["isLogin", "userInfo"]),
  },
  created() {
    this.$store.dispatch("getBoards");
  },
  methods: {
    movePage() {
      if (this.isLogin && this.userInfo.id === "admin") this.$router.push({ name: "board-create" });
      else alert("관리자만 사용 가능한 기능입니다.");
    },
    // getFormatDate(regtime) {
    //   return moment(new Date(regtime)).format("YYYY.MM.DD");
    // },
  },
};
</script>

<style></style>
