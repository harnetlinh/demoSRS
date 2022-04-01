<template>
  <b-container fluid>
    <b-row class="mt-5">
      <b-col fluid="sm" cols="12">
        <b-card>
          <b-row>
            <b-col cols="3">
              <b-form-input v-model="text" placeholder="Tìm kiếm mã SV" />
            </b-col>
            <b-col cols="3">
              <b-form-select
                v-model="selected"
                :options="options"
              ></b-form-select>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
    </b-row>
    <b-row>
      <b-col fluid="sm" cols="12">
        <b-card>
          <div class="d-flex align-items-center mb-3">
            <b-progress class="w-100" :max="maxLoadingTime" height="1.5rem">
              <b-progress-bar
                :value="loadingTime"
                :label="`${((loadingTime / maxLoadingTime) * 100).toFixed(2)}%`"
              />
            </b-progress>

            <b-button class="ml-3" @click="startLoading()">Rescan</b-button>
          </div>

          <b-skeleton-wrapper :loading="loading">
            <template #loading>
              <b-card>
                <b-skeleton width="85%" />
                <b-skeleton width="55%" />
                <b-skeleton width="70%" />
              </b-card>
            </template>

            <b-card>
              <b-table-simple hover small caption-top responsive>
                <caption>
                  Danh sách sinh viên nguy cơ:
                </caption>
                <colgroup>
                  <col />
                  <col />
                </colgroup>
                <colgroup>
                  <col />
                  <col />
                  <col />
                </colgroup>
                <colgroup>
                  <col />
                  <col />
                </colgroup>
                <b-thead head-variant="dark">
                  <b-tr>
                    <b-th colspan="2">Sinh viên</b-th>
                    <b-th colspan="3">Học tập</b-th>
                    <b-th colspan="2">Ý thức</b-th>
                  </b-tr>
                  <b-tr>
                    <b-th>Mã sinh viên</b-th>
                    <b-th>Lớp</b-th>
                    <b-th>Toán</b-th>
                    <b-th>Lý</b-th>
                    <b-th>Hóa</b-th>
                    <b-th>Cần cù</b-th>
                    <b-th>Ngoại khóa</b-th>
                  </b-tr>
                </b-thead>
                <b-tbody>
                  <b-tr>
                    <b-th rowspan="3">
                      <a href="#" v-b-modal.modal-center
                        >Lê Bảo Anh (PH12345)</a
                      >
                    </b-th>
                    <b-th class="text-right">Group306</b-th>
                    <b-td>56</b-td>
                    <b-td>22</b-td>
                    <b-td>43</b-td>
                    <b-td variant="success">72</b-td>
                    <b-td>23</b-td>
                  </b-tr>
                  <b-tr>
                    <b-th class="text-right">Group530</b-th>
                    <b-td>46</b-td>
                    <b-td variant="warning">18</b-td>
                    <b-td>50</b-td>
                    <b-td>61</b-td>
                    <b-td variant="danger">15</b-td>
                  </b-tr>
                  <b-tr>
                    <b-th class="text-right">Group334</b-th>
                    <b-td>51</b-td>
                    <b-td>27</b-td>
                    <b-td>38</b-td>
                    <b-td>69</b-td>
                    <b-td>28</b-td>
                  </b-tr>
                  <b-tr>
                    <b-th rowspan="2">Trần Thanh Tâm (PH45678)</b-th>
                    <b-th class="text-right">Group263</b-th>
                    <b-td variant="success">89</b-td>
                    <b-td>34</b-td>
                    <b-td>69</b-td>
                    <b-td>85</b-td>
                    <b-td>38</b-td>
                  </b-tr>
                  <b-tr>
                    <b-th class="text-right">Group097</b-th>
                    <b-td>80</b-td>
                    <b-td variant="danger">12</b-td>
                    <b-td>43</b-td>
                    <b-td>36</b-td>
                    <b-td variant="warning">19</b-td>
                  </b-tr>
                </b-tbody>
                <b-tfoot>
                  <b-tr>
                    <b-td colspan="7" variant="secondary" class="text-right">
                      Tổng số sinh viên nguy cơ: <b>2</b>
                    </b-td>
                  </b-tr>
                </b-tfoot>
              </b-table-simple>
            </b-card>
          </b-skeleton-wrapper>
        </b-card>
      </b-col>
    </b-row>

    <b-modal id="modal-center" size="xl" centered title="BootstrapVue">
      <b-container fluid>
        <b-row>
          <b-col cols="6">
            <apexchart
              width="500"
              type="radar"
              :options="chartOptions"
              :series="series"
            ></apexchart>
            <br>
            <b-table-simple hover small caption-top responsive>
              <caption>
                Bảng điểm:
              </caption>
              <b-thead>
                <b-tr>
                  <b-th>Môn</b-th>
                  <b-th>Mã môn</b-th>
                  <b-th>Số tín chỉ</b-th>
                  <b-th>Điểm</b-th>
                  <b-th>Trạng thái</b-th>
                </b-tr>
              </b-thead>
              <b-tbody>
                <b-tr>
                  <b-td>Toán</b-td>
                  <b-td>MATH101</b-td>
                  <b-td>3</b-td>
                  <b-td>89</b-td>
                  <b-td variant="success">Đạt</b-td>
                </b-tr>
                <b-tr>
                  <b-td>Lý</b-td>
                  <b-td>F101</b-td>
                  <b-td>3</b-td>
                  <b-td>47</b-td>
                  <b-td variant="danger">Trượt</b-td>
                </b-tr>
              </b-tbody>
            </b-table-simple>
          </b-col>
          <b-col cols="6">
            <b-card
              no-body
              class="w-100"
              img-src="https://placekitten.com/380/200"
              img-alt="Image"
              img-top
            >
              <template #header>
                <h4 class="mb-0">Sinh viên ABC</h4>
              </template>

              <b-card-body>
                <b-card-title>Thông tin sinh viên</b-card-title>
                <b-card-sub-title class="mb-2">(HDI)</b-card-sub-title>
                <b-card-text>
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </b-card-text>
              </b-card-body>

              <b-list-group flush>
                <b-list-group-item>Cras justo odio</b-list-group-item>
                <b-list-group-item>Dapibus ac facilisis in</b-list-group-item>
                <b-list-group-item>Vestibulum at eros</b-list-group-item>
              </b-list-group>

              <b-card-body>
                <a href="#" class="card-link">Card link</a>
                <a href="#" class="card-link">Another link</a>
              </b-card-body>

            </b-card>
          </b-col>
        </b-row>
      </b-container>
    </b-modal>
  </b-container>
</template>

<script>
import BarChart from "../Charts/BarChart.vue";
export default {
  name: "Dashboard",
  components: {
    BarChart,
  },
  data() {
    return {
      chartOptions: {
        stroke: {
          show: true,
          width: 2,
          colors: [],
          dashArray: 0,
        },
      },
      labels: ["April", "May", "June", "July", "August", "September"],
      series: [
        {
          name: "Radar Series 1",
          data: [45, 52, 38, 24, 33, 10],
        },
        {
          name: "Radar Series 2",
          data: [26, 21, 20, 6, 8, 15],
        },
      ],
      loading: false,
      loadingTime: 0,
      maxLoadingTime: 3,
      selected: null,
      options: [
        { value: null, text: "Tìm theo tiêu chí", disabled: true },
        { value: "a", text: "Sinh viên có xu hướng DO" },
        { value: "b", text: "Sinh viên có thể bị đuổi học vì học tập" },
        { value: "c", text: "Sinh viên có thể bị đuổi học vì ý thức" },
      ],
    };
  },
  watch: {
    loading(newValue, oldValue) {
      if (newValue !== oldValue) {
        this.clearLoadingTimeInterval();

        if (newValue) {
          this.$_loadingTimeInterval = setInterval(() => {
            this.loadingTime++;
          }, 1000);
        }
      }
    },
    loadingTime(newValue, oldValue) {
      if (newValue !== oldValue) {
        if (newValue === this.maxLoadingTime) {
          this.loading = false;
        }
      }
    },
  },
  created() {
    this.$_loadingTimeInterval = null;
  },
  mounted() {
    this.startLoading();
  },
  methods: {
    clearLoadingTimeInterval() {
      clearInterval(this.$_loadingTimeInterval);
      this.$_loadingTimeInterval = null;
    },
    startLoading() {
      this.loading = true;
      this.loadingTime = 0;
    },
  },
};
</script>
