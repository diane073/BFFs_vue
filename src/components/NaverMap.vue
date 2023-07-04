<template>
    <div id="map">
    </div>
</template>

<script>
export default {
    name: "NaverMap",
    data() {
        return {
            map: null,
            mapOptions: {
                // 지도의 위도 경도 넣기
                lat: 37.3588000,
                lng: 127.105399,
                zoom: 15,
                disableDoubleClickZoom : true,
            },
        };
    },
    setup() {},
    mounted() {
        if (window.naver && window.naver.maps) {
            this.loadMap();
        } else {
            this.loadScript();
        }
    },
    methods: {
        loadScript() {
            const container = document.getElementById("map")
            const script = document.createElement("script");
            script.src = "https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=%process.env.VUE_APP_NAVER_MAP_CLIENT_ID%";
            script.onload = () => window.naver.maps.load(this.loadMap);
            container.appendChild(script);
        },
        loadMap() {
            const container = document.getElementById("map")
            const option = {
                center: new window.naver.maps.LatLng(33.450701, 126.570667),
                level: 3
            }
            this.map = new window.naver.maps.Map(container, option);
            this.loadMarker();
        },
        loadMarker() {
            const markerPosition = new window.naver.maps.LatLng(33.450701, 126.570667);
            const marker = new window.naver.maps.Marker({position: markerPosition,});
            marker.setMap(this.map);
        }
    },
};
</script>

<style scoped>
#map {
    width: 300px;
    height: 300px;
}