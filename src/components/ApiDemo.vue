<template>
    <div class="container">
        <div class="row" id="data-button-row">
            <div class="col">
                <button class="btn btn-primary" @click="getData">Get Data</button>
            </div>
        </div>
        <div class="row" id="data-row">
            <div class="col">
                <div v-for="user of mockData.users" :key="user.id">
                    {{user.id}}, {{user.name}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import 'bootstrap/dist/js/bootstrap.min'
    import 'bootstrap/dist/css/bootstrap.min.css'
    import 'jquery/src/jquery.js'
    const axios = require('axios')
    const MockAdapter = require('axios-mock-adapter')

    const axiosMock = new MockAdapter(axios)

    export default {
        name: 'ApiDemo',
        created() {
            //
        },
        mounted() {
            //
        },
        data() {
            return {
                loading: true,
                mockData: {}
            }
        },
        methods: {
            getData() {
                axiosMock.onGet("/users").reply(200, {
                    users: [{id: 1, name: "John Smith"}, {id: 2, name: "Toby Jorris"}]
                })

                axios.get('/users').then(response => {
                    this.mockData = response.data
                })

            }
        }
    }
</script>

<style>
    #data-button-row {
        border: 1px solid green;
        margin-bottom: 50px;
        padding: 30px 0;
    }

    #data-row {
        border: 1px solid blue;
        min-height: 300px;
    }
</style>
