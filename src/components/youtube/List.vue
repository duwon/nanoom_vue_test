<template>
  <v-container
    id="youtubelist"
    tag="section"
  >
    <base-subheading>About Us</base-subheading>

    <div @click="getYoutubeList()">테스트</div>

  </v-container>
</template>

<script>

import youtube from '@/config/youtubeconfig'

  export default {
    name: 'YoutubeList',
    methods : {
      getYoutubeList : () => { // [테스트] 클릭시 호출 함수 -> 실제 API통신함
        let newUrl = ''; // url및 인증키, 검색어를 조합한 새로운 url
        newUrl = youtube.url + '?part=snippet&order=date&channelId=' + youtube.channelId + '&key=' + youtube.key; // newUrl 수정
        let loadYoutubeList = fetch(newUrl, { // fetch함수를 통한 비동기 통신
            method : 'GET',
        }).then(res => res.json()).then((res2)=>{ // json()을 통해 사용 가능한 데이터로 변환
          //console.log(res2);
          if (res2['items'][0]['snippet']['liveBroadcastContent'] === 'live') { //생방송 중인 데이터가 있으면
          console.log(res2['items'][0]['snippet']['title']); // title 출력
          console.log(res2['items'][0]['id']['videoId']); // vidoeID 출력
          }
          else {
            console.log("none");
          }
        })

		  }
	  }
  }
</script>
