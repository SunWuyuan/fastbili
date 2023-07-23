
<!-- App.vue -->
<template>
  <v-app>
    <v-app-bar app>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>FastBiliApi</v-toolbar-title>
    </v-app-bar>

    <!-- 根据应用组件来调整你的内容 -->
    <v-main>

      <!-- 给应用提供合适的间距 -->
      <v-container fluid>


        <v-container>



          <h2>FastBiliApi</h2>
          <v-text-field v-model="bvid" label="请输入BVid"></v-text-field>
          <p>例如：https://www.bilibili.com/video/BV1fM4y1971n/ 后面的“BV1fM4y1971n”就是BVid</p>
          <v-btn @click="getData">解析</v-btn><a> </a>
          <br /><br />

          <v-row v-if="data"> <v-card>
              <v-card-title>{{ data.title }}</v-card-title>
              <v-card-subtitle>{{ data.desc }}</v-card-subtitle>




              <v-col cols="12">


                <template>
                  <v-row justify="center">
                    <v-expansion-panels popout>
                      <v-expansion-panel>
                        <v-expansion-panel-header>作者数据</v-expansion-panel-header>
                        <v-expansion-panel-content>


                          <v-simple-table>
                            <template v-slot:default>
                              <thead>
                                <tr>
                                  <th class="text-left">
                                    内容
                                  </th>
                                  <th class="text-left">
                                    数据
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <tr>
                                  <td>用户名</td>
                                  <td>{{ data.owner.name }}</td>
                                </tr>
                                <tr>
                                  <td>mid</td>
                                  <td>{{ data.owner.mid }}</td>
                                </tr>
                                <tr>
                                  <td>头像链接</td>
                                  <td>{{ data.owner.face }}</td>
                                </tr>
                              </tbody>
                            </template>
                          </v-simple-table>
                        </v-expansion-panel-content>
                      </v-expansion-panel><v-expansion-panel>
                        <v-expansion-panel-header>视频数据</v-expansion-panel-header>
                        <v-expansion-panel-content>

                          <v-simple-table>
                            <template v-slot:default>
                              <thead>
                                <tr>
                                  <th class="text-left">
                                    内容
                                  </th>
                                  <th class="text-left">
                                    数据
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <tr>
                                  <td>bvid</td>
                                  <td>{{ data.bvid }}</td>
                                </tr>
                                <tr>
                                  <td>avid</td>
                                  <td>{{ data.aid }}</td>
                                </tr>
                                <tr>
                                  <td>播放量</td>
                                  <td>{{ data.stat.view }}</td>
                                </tr>
                                <tr>
                                  <td>弹幕量</td>
                                  <td>{{ data.stat.danmaku }}</td>
                                </tr>
                                <tr>
                                  <td>评论数 </td>
                                  <td>{{ data.stat.reply }}</td>
                                </tr>
                                <tr>
                                  <td>收藏数</td>
                                  <td>{{ data.stat.favorite }}</td>
                                </tr>
                                <tr>
                                  <td>投币数</td>
                                  <td>{{ data.stat.view }}</td>
                                </tr>
                                <tr>
                                  <td>分享数</td>
                                  <td>{{ data.stat.share }}</td>
                                </tr>
                              </tbody>
                            </template>
                          </v-simple-table>
                        </v-expansion-panel-content>
                      </v-expansion-panel> <v-expansion-panel>
                        <v-expansion-panel-header>原始JSON数据</v-expansion-panel-header>
                        <v-expansion-panel-content>
                          <pre> {{ data }}</pre>
                        </v-expansion-panel-content>
                      </v-expansion-panel>
                    </v-expansion-panels>
                  </v-row>
                </template>
              </v-col><br /><br />
            </v-card>
          </v-row>
        </v-container>

      </v-container>
    </v-main>


  </v-app>
</template>

<script>
export default {
  data() {
    return {
      bvid: "",
      data: null,
    };
  },
  methods: {
    async getData() {
      const response = await fetch(
        `https://cors-anywhere.wuyuan.dev/biliapi.192325.xyz/x/web-interface/view?bvid=${this.bvid}`,{
  headers: {
    'Content-Type': 'application/json',
    'Accept': '*/* ',
    'Connection': 'keep-alive',
    'Accept-Encoding': 'gzip, deflate, br',
    'User-Agent': 'desktop'
  }}

      );
      const json = await response.json();
      this.data = json.data;
    },
  },
};
</script>
