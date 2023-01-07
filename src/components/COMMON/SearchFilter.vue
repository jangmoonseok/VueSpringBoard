<template>
    <div class="filter" v-for="column in filterColumns" :key="column.value">
        <div class="filter_combo" v-if="column.filterType == 'combo'">
            <div>{{column.text}}</div>
            <div v-for="item in filterColumnsItem" :key="item.value">
                <div v-if="item.value == column.value">
                    <div v-for="i in item.items" :key="i">
                        <input type="radio" :name="item.value" :value="i">{{i}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SearchFilter',
    components: {},
    props: {
        dataHeader:Array,
        originalDatas:Array
    },
    data() {
        return {
            filterColumnsItem:[],
            filterColumns:[],
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
            this.setFilterColumns();
            this.setFilterColumnsItem();
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

            console.log(this.filterColumnsItem)
        }
    },
}
</script>

<style scoped>
.filter{
    width: 250px;
    border: 1px solid black;
    background-color: white;
    border-radius: 10px;
    position: absolute;
    right: 10px;
}
</style>