<template>
    <div>
        <h1 class="peeps-intro">Current Space Peeps!</h1>
            <div class="p-cards-container">
            <div class="people-card" v-for="peep in peopleSpaceData.people">
                <p> <a :href="prepareGoogleAddress(peep.name)" target="_blank">{{peep.name}}: {{peep.craft}} <br>Click for more information</a></p>
            </div>
        </div>
        <div class="iss-crew">
            <img src="https://thenypost.files.wordpress.com/2020/04/space-1.jpg" width="600px" alt="iss crew">
        </div>
    </div>
</template>

<script>
export default {
    name: "space-peeps",
    data() {
        return {
            peopleSpaceData: {},
        }
    },
    mounted(){
        this.fetchData()
    },
    methods: {
        fetchData() {
            fetch("http://api.open-notify.org/astros.json")
            .then(apiData => apiData.json())
            .then(apiDataJson => this.peopleSpaceData = apiDataJson)
            },
        prepareGoogleAddress(peepName){
            return `http://www.google.com/search?q=${peepName}&btnI`
        }
    },
};
</script>

<style scoped>
    p {
        font-size: 1.5em;
    }
    
    a {
        text-decoration: none;
        color: #130b5b;;
    }

    .iss-crew{
        padding: 60px;
    }

    .p-cards-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    .people-card {
            /* flex: 0 1 calc(40% - 1em); */
            background-color: #B1C4EF;
            margin: 2%;
            padding: 2%;
            border-radius: 12px;
        }

    .peeps-intro {
          margin-top: 100px;
          padding-top: 50px;
    }

</style>