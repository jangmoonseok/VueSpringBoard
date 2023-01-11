<template>
    <div class="SearchBar">
        <input class="textField" type="text" v-model="searchValue" @keyup="onSearchEnter" placeholder="검색어를 입력하세요."/>
        <button type="button" v-on:click="onSearch">검색</button>
        <button type="button" v-on:click="openFilter">필터</button>
        <div class="filter" v-for="column in filterColumns" :key="column.value" v-show="filterShow">
            <div class="filter_combo" v-if="column.filterType == 'combo'">
                <div>{{column.text}}</div>
                <div v-for="item in filterColumnsItem" :key="item.value">
                    <div v-if="item.value == column.value">
                        <select :name="column.value" @change="onChangeSelect">
                            <option value="all">전체</option>
                            <option v-for="(i, index) in item.items" :key="index" :value="i">{{i}}</option>
                        </select>
                    </div>
                </div>
            </div>
            <button type="button" v-on:click="onSearchFilter">검색</button>
        </div>
    </div>
</template>

<script>

export default {
    name: 'SearchFilterForm',
    components: {
    },
    props: {
        dataHeader:Array,
        originalDatas:Array
    },
    data() {
        return {
            searchOption:"",
            searchValue:"",
            searchDatas:[],
            filterColumnsItem:[],
            filterColumns:[],
            filterShow:false,
            filterObject:[],
        }
    },
    create(){},
    computed(){},
    watch:{
        
    },
    mounted(){
        this.onLoad();
    },
    methods: {
        onLoad(){
            this.setFilterColumns();
            this.setFilterColumnsItem();
        },  
        onSearch(){
            
        },
        onSearchEnter(e){
            if(e.keyCode == 13){
                this.onSearch();
            }
        },
        setFilterColumns(){
            this.dataHeader.forEach((item) => {
                if(Object.hasOwn(item, 'filter')){
                    this.filterColumns.push(item);
                }
            })
        },
        setFilterColumnsItem(){
            this.filterColumns.forEach((column) => {
                const itemObj = {
                    value:column.value,
                    items:[],
                }
                this.originalDatas.forEach((item) => {
                    if(itemObj.items.indexOf(item[column.value]) == -1){
                        itemObj.items.push(item[column.value]);
                    }    
                })  
                this.filterColumnsItem.push(itemObj);
            });

        },
        openFilter(){
            this.filterShow = !this.filterShow;
        },
        onChangeSelect(e){
            const key = e.target.name;
            const value = e.target.value;
            const obj = {
                key:key,
                value:value
            }

            let objCheck = false;
            this.filterObject.forEach((item) => {
                if(item.key == obj.key){
                    objCheck = true;
                    item.value = obj.value;
                }
            })

            if(!objCheck){
                this.filterObject.push(obj);
            }
        },
        onSearchFilter(){
            this.searchDatas = [];
            this.filterShow = false;
            this.originalDatas.forEach((item) => {
                let flag = true;
                this.filterObject.filter(obj => obj.value != "all").forEach((obj) => {
                    if(item[obj.key] != obj.value) flag = false; 
                })

                if(flag){
                    this.searchDatas.push(item);
                }
            })
            this.$emit('filterChange', this.searchDatas);
        },
        
    },
}
</script>

<style  scoped>
.SearchBar{
    position: relative;
    width: 700px;
    margin: auto;
}
.filter{
    width: 250px;
    border: 1px solid black;
    background-color: white;
    border-radius: 10px;
    position: absolute;
    right: 10px;
    padding: 10px;
}
.filter_combo{
    display: flex;
}
</style>