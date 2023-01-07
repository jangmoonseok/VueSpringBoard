<template>
    <div class="SearchBar">
        <input class="textField" type="text" v-model="searchValue" @keyup="onSearchEnter" placeholder="검색어를 입력하세요."/>
        <button type="button" v-on:click="onSearch">검색</button>
        <button type="button" v-on:click="openFilter">필터</button>
        <SearchFilter
            :dataHeader="dataHeader"
            :originalDatas="originalDatas"/>
    </div>
    <div style="margin-top:30px;">
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
import SearchFilter from "./SearchFilter.vue";

export default {
    name: 'SearchBar',
    components: {
        SearchFilter
    },
    props: {},
    data() {
        return {
            searchOption:"",
            searchValue:"",
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
            searchDatas:[]
        }
    },
    create(){},
    computed(){},
    watch:{
        // searchValue(value){
        //     console.log(value);
        // }
    },
    mounted(){
        this.onLoad();
    },
    methods: {
        onLoad(){
            this.searchDatas = [...this.originalDatas];
            // console.log(this.searchDatas[0]);
        },  
        onSearch(){
            if(this.searchOption == "division"){
                this.searchDatas = this.originalDatas.filter(item => item.division == this.searchValue);
            }

            if(this.searchOption == "title"){
                this.searchDatas = this.originalDatas.filter(item => item.title.includes(this.searchValue));
            }

            if(this.searchOption == "writer"){
                this.searchDatas = this.originalDatas.filter(item => item.writer == this.searchValue);
            }
        },
        onSearchEnter(e){
            if(e.keyCode == 13){
                this.onSearch();
            }
        },
        onChange(e){
            this.searchOption = e.target.value;
            console.log(this.searchOption);
        }
    },
}
</script>

<style  scoped>
table td,th{
    padding: 5px;
}
.SearchBar{
    position: relative;
    width: 700px;
    margin: auto;
}
</style>