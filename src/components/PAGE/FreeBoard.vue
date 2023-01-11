<template>
    <div>
        <SearchFilterForm
            :originalDatas="originalDatas"
            :dataHeader="dataHeader"
            @filterChange="filterChange"/>
        <table style="margin: auto;">
            <thead>
                <tr>
                    <th v-for="header in dataHeader" :key="header.value">
                        {{header.text}}
                    </th>
                </tr>
            </thead>
            <tbody v-for="data in searchDatas" :key="data.id">
                <tr>
                    <td>{{data.division}}</td>
                    <td>{{data.title}}</td>
                    <td>{{data.writer}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import SearchFilterForm from '../COMMON/SearchFilterForm.vue'

export default {
    name: 'FreeBoard',
    components: {
        SearchFilterForm
    },
    props: {},
    data() {
        return {
            originalDatas:[
                {
                    id:1,
                    division:"일기",
                    title:"공부일기",
                    writer:"홍길동"
                },
                {
                    id:2,
                    division:"일기",
                    title:"운동일기",
                    writer:"이순신"
                },
                {
                    id:3,
                    division:"일기",
                    title:"연애일기",
                    writer:"이순신"
                },
                {
                    id:4,
                    division:"잡글",
                    title:"아~~하기싫다",
                    writer:"강감찬"
                },
                {
                    id:5,
                    division:"잡글",
                    title:"좆소때려치고싶다",
                    writer:"성춘향"
                },
                {
                    id:6,
                    division:"지식",
                    title:"웹개발자 로드맵",
                    writer:"을지문덕"
                },
                {
                    id:7,
                    division:"지식",
                    title:"RESTful??",
                    writer:"이몽룡"
                },
                {
                    id:8,
                    division:"잡글",
                    title:"님들 개발자왜함?",
                    writer:"홍길동"
                }
                
            ],
            dataHeader:[
                {
                    text:"구분",
                    value:"division",
                    filter:true,
                    filterType:"combo"
                },
                {
                    text:"제목",
                    value:"title",
                    searchAbled:true
                },
                {
                    text:"작성자",
                    value:"writer",
                    searchAbled:true
                },
            ],
            searchDatas:[],
        }
    },
    create(){},
    computed(){},
    watch:{},
    mounted(){
        this.onLoad();
    },
    methods: {
        onLoad(){
            this.searchDatas = [...this.originalDatas];
        },
        filterChange(v){
            this.searchDatas = v;
        }
    },
}
</script>

<style scoped>
table td,th{
    padding: 5px;
}
</style>