<template>
    <div id="app">
        <div id="side-menu">
            <aside class="menu">
                {{mainUrl}}

                <ul class="menu-list">
                    <router-link to="/home">Home</router-link>
                </ul>

                <p class="menu-label">Deploy</p>
                <ul class="menu-list">
                    <router-link to="/doc">Waahi for Web AppBuilder</router-link>
                    <router-link to="/doc1">Waahi Gallery</router-link>
                </ul>
                <p class="menu-label">
                    Administer
                </p>
                <ul class="menu-list">
                    <li><a>Web AppBuilder Widgets</a></li>
                </ul>

                <p class="menu-label">
                    Advanced Deployment
                </p>
                <ul class="menu-list">
                    <li><a>Geoprocessing Services</a></li>
                    <li><a>Sharing Service (.NET Core)</a></li>
                </ul>

            </aside>
        </div>

        <div id="main">
            <div id="content-wrapper">
                <intro v-if="$route.path === '/home'" ></intro>
                <iframe ref="docIframe" v-if="$route.path !== '/home'" :src="docUrl" />
            </div>

        </div>

        <!-- router not used yet 
            <router-view /> -->
    </div>
</template>

<script>
import Intro from '@/components/Intro.vue';

export default {
    name: "App",
    components: {
        Intro
    },
    data: function() {
        return {
            timerId: null,
            mainUrl: "",
            docUrl: "./docs/Admin%20Guide.htm"
        };
    },
    created() {
        this.refresh();

    },
    methods: {
        refresh() {
            if (this.timerId) {
                clearInterval(this.timerId);
            }
            var timerId = setInterval(() => {
                debugger
                var iFrame = this.$refs["docIframe"];
                var url = iFrame.contentWindow.location.href;
                var hashUrl = url.split("#")[1];
                location.href = location.href + "?ref=" + hashUrl;

            }, 1500);

        }
    },
    watch: {
        $route() {
            this.refresh();

        },
        docUrl() {
            alert(this.docUrl);
        }

    }
};
</script>


<style lang="scss">
html,
body,
#app {
    height: 100%;
    width: 100%;
    margin: 0;
    padding: 0;
}



#app {
    h1 {
        font-size: 2em;
    }

    #side-menu {
        position: absolute;
        width: 300px;
        left: 0px;
        top: 0;
        bottom: 0;
        padding: 20px;

        a {
            &.router-link-exact-active {
                border-bottom: 1px solid blue; 
            }
        }
    }

    #main {
        margin: 0 0 0 300px;
        padding: 0px;
        height: 100%;
        width: auto;

        #content-wrapper {
            margin: 0;
            padding: 20px;
            width: auto;
            height: 100%;

            iframe {
                height: 100%;
                width: 100%;
            }
        }
    }
}


</style>
