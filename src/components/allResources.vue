<template>
    <ul>
        <li v-for="res in resources" :key="res.title" @click="openTab(res.link)">
            <h2> <a :href=res.link target="_blank">  {{  res.title  }}  </a></h2>
            <h3> {{ res.description }}</h3>
        </li>
    </ul>
    <!-- <p>{{ updatedRes }}</p> -->
    <!--bar plot from Chars.js  -->
</template>
 
  
<script>
    export default {
      props: {
        'resource' : Object, 
        'updatedRes' : Object
      }, 
      data() {
        return {
          resources : [
            {
                id : 1,
                title : "Google", 
                description : "Modern search engine", 
                link : "http://www.google.com"
            }, 
            {
                id : 2, 
                title : "Wikipedia", 
                description : "The free encyclopedia", 
                link : "http://www.wikipedia.org"
            }
          ]
        };
      },
      methods : {
        openTab(url){
            window.open(url, '_blank'); 
        }
      },
      watch : {
        resource: {
            handler(newv, oldv){
                console.log("resource received" + newv + "  " + oldv ) ;
                if (newv !== null ){
                    this.resources.push(newv) ;
                    console.log(this.resources) ;
                }
            },
            immediate: true,
        }, 
        updatedRes: {
            handler(newv, oldv){
                console.log("resource updated" + newv + "  " + oldv ) ;
                if (newv !== null ){
                    let searchR = this.resources.find(item => item.title.toLowerCase() === newv.title.toLowerCase()) ;
                    if (searchR){
                        searchR.link = newv.link ;
                        searchR.description = newv.description ;
                    }
                }
            },
            deep : true, 
            immediate: true,
        }, 
      }
    };
</script>

<style scoped>
    ul li {
        width: 250px;
        height: 35px;
        display: flex;
        align-items: center;
        margin: 1.5em;
        cursor: pointer;
        padding: 1em;
        background: rgb(13, 145, 168);
        position: relative;
        color: white;
        border-radius: 5px;
    }
    ul li::before,
    ul li::after {
        content: "";
        position: absolute;
        z-index: -1;
        border-radius: 5px;
        width: 105%;
        transition: all 0.4s;
    }
    ul li::before {
        left: 0%;
        height: 130%;
        background: linear-gradient(to right, #04144e, #000000);
    }
    ul li::after {
        left: -10%;
        height: 120%;
        background: #dc0d0dc7;
        backdrop-filter: blur(10px);
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.164);
    }
    /* ul li:hover::before {
        transform: translateX(-2.5%);
    } */
    ul li:hover::after {
        transform: translateX(5%);
        background-color: rgb(251, 96, 0);
    }

    h3{
     text-align: right;
    }
</style>
    