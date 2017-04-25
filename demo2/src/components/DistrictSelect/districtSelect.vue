<template>
    <div>
        <select name="province" v-model="currentDis.province" id="province">
            <option v-for="item in provinces" :value="item.province.code">{{item.province.name}}</option>
        </select>
        <select name="city" v-model="currentDis.city" id="city">
            <option v-for="item in cities" :value="item.code">{{item.name}}</option>
        </select>
        <select name="district" v-model="currentDis.district" id="district">
            <option v-for="item in districts" :value="item.code">{{item.name}}</option>
        </select>
        <div>{{currentProvince?currentProvince.province.name:""}}</div>
        <div>{{currentCity?currentCity.name:""}}</div>
        <div>{{currentDistrict?currentDistrict.name:""}}</div>
    </div>
</template>
<script>
    import localList from '../../assets/data.js'
    export default{
        data(){
            return {
                provinces:localList,
                currentProvince:"",
                currentCity:"",
                currentDistrict:"",
                currentDis:{
                    province:"",
                    city:"",
                    district:""
                }
            }
        },
        watch:{
            currentProvince(oldVal, newVal){
                if(oldVal!=newVal){
                    this.currentCity = "";
                    this.currentDistrict = "";
                    this.currentDis.city = "";
                    this.currentDis.district = "";
                }
            },
            currentCity(oldVal, newVal){
                if(oldVal!=newVal){
                    this.currentDistrict = "";
                    this.currentDis.district = "";
                }
            },
            currentDis:{
                handler(oldVal, newVal){
                    let district = this.currentDis.district;
                    if(district){
                        this.currentDistrict = this.currentCity.district.filter((item) => {
                            if(item.code == district){
                                return item;
                            }
                        })[0];
                    }
                },
                deep:true
            }
        },
        computed:{
            cities(){
                if(!this.currentDis.province){
                    return []
                }
                this.currentProvince = localList.filter((item) => {
                    if(item.province.code == this.currentDis.province){
                        return item;
                    }
                })[0];
                return this.currentProvince.province.city
            },
            districts(){
                if(!this.currentDis.city){
                    return []
                }
                this.currentCity = this.currentProvince.province.city.filter((item) => {
                     if(item.code == this.currentDis.city){
                        return item;
                     }
                })[0];
                return this.currentCity.district
            }
        }
    }
</script>
<style scoped>
select{
    min-width:100px;
}
</style>