<style>
.glyphicon { margin-right:5px; }
.thumbnail
{
    margin-bottom: 20px;
    padding: 0px;
    -webkit-border-radius: 0px;
    -moz-border-radius: 0px;
    border-radius: 0px;
}

.item.list-group-item
{
    float: none;
    width: 100%;
    background-color: #fff;
    margin-bottom: 10px;
}
.item.list-group-item:nth-of-type(odd):hover,.item.list-group-item:hover
{
    background: #428bca;
}

.item.list-group-item .list-group-image
{
    margin-right: 10px;
}
.item.list-group-item .thumbnail
{
    margin-bottom: 0px;
}
.item.list-group-item .caption
{
    padding: 9px 9px 0px 9px;
}
.item.list-group-item:nth-of-type(odd)
{
    background: #eeeeee;
}

.item.list-group-item:before, .item.list-group-item:after
{
    display: table;
    content: " ";
}

.item.list-group-item img
{
    float: left;
}
.item.list-group-item:after
{
    clear: both;
}
.list-group-item-text
{
    margin: 0 0 11px;
}

</style>


<template>
    <div class="container">
    <div >
        <input type="text" class="form-control" placeholder="search" v-model="data_s">
        <button class="btn btn-primary" @click="search_bt"><i class="fa fa-search"></i></button>
    </div>
    <br>
    <div id="products" class="row list-group" >
        <div v-for="(value) in product" v-bind:key="value">
            <div class="item  col-xs-4 col-lg-4">
                <div class="thumbnail">
                    <img :src="value.pro_pic" style="height:300px;" alt="">
                    <!-- <img class="group list-group-image" src="{{value.pro_pic}}" alt="" /> -->
                    <div class="caption">
                        <h4><b class="group inner list-group-item-heading">
                            {{value.pro_name}}</b></h4>
                        <p class="group inner list-group-item-text">
                           {{value.pro_detail}}
                        <div class="row">
                            <div class="col-xs-12 col-md-6">
                                <p class="lead">
                                    {{value.pro_price}}</p>
                            </div>
                            <div class="col-xs-12 col-md-6">
                                <a class="btn btn-success" href="http://www.jquery2dotnet.com">Add to cart</a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
    import axios from 'axios';

    export default {
    name: "Product",

    components: {},
        data() {
            return {
                product: [],
                data_s: "",
                
            };
        },
        methods:{
            search_bt(){

                axios.get("http://10.0.1.191:7777/getdata_search", {
                params: {
                    data_s: this.data_s,
                   
                },
                headers: {
                    "Content-Type": "application/json",
                },
                })
                .then((response) => {
                    console.log(response.data);
                //    this.product = response.data;
                })
                .catch(function (error) {
                    console.log(error);
                });
            },
        },
        mounted() {
            axios.get("http://10.0.1.191:7777/getData", {
            headers: {
                "Content-Type": "application/json",
                },
            })
            .then((response) => {
                console.log(response);
                console.log(response.data);
                this.product = response.data;
            })
            .catch(function (error) {
                console.log(error);
            });    
        },
    };
    
</script>