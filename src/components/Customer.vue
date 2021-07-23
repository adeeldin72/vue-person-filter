
<template>

    <div class="customer" tabindex="0">
        <Card>
        <div class="customerBackground">
        
        <div class="upperInfo">
            <div class="profileImageContainer">
                <img :src="data.imgUrl" :alt="'Profile for ' + data.name" class = "profilePicture">
            </div>
            <div class="profileHeading">
                <p class = "customerName">{{data.name}}</p>
                <p class = "customerUserName">@{{data.username}}</p>
                <p class = "companyCatchPhrase">"{{data.company.catchPhrase}}"</p>
            </div>
        </div>

        <div class="profileInfo">
            
            <ul>
                <li class="mailLi">
                    <p>{{data.email}}</p>
                </li>
                <li class="mapLi">
                    <p>{{data.address.street}}, {{data.address.suite}}, {{data.address.zipcode}}, {{data.address.geo.lat}}, {{data.address.geo.lng}}</p>
                </li>
                <li class="callLi">
                    <p>{{data.phone}}</p>
                </li>
                <li class="globeLi">
                    <p>
                    <a :href="'https://' + data.website" target="_blank">{{data.website}}</a></p>
                </li>
                <li class="bagLi">
                    <p>{{data.company.name}}</p>
                </li>
                <li class="buildingLi">
                    <p>{{data.company.bs}}</p>
                </li>
            </ul>
        </div> 
        </div>   
        </Card>
    </div>

</template>

<script>
import Card from './ui/Card.vue'
export default {
    props:['data'],
    components:{Card}
}
</script>


<style>
    @import url('https://fonts.googleapis.com/css2?family=Rubik:wght@500&display=swap');

    .customer {
        margin: 25px;
        max-width: 375px;
        min-height: 500px;
        white-space: pre-wrap;
    }
    .customerBackground {
        background: white;
    }
    .mailLi {
        position: relative;
        list-style-image: url('../assets/mail.png');
        white-space: pre-wrap;
    }
    .mailLi::after {
        content: url('../assets/Vector.png');
        position: absolute;
        top: -5px;
        left: -26px;
    }
    .mapLi {
        list-style-image: url('../assets/map.png')
    }
    .callLi {
        list-style-image: url('../assets/call.png')
    }
    .globeLi {
        list-style-image: url('../assets/globe.png')
    }
    .bagLi {
        list-style-image: url('../assets/bag.png')
    }
    .buildingLi {
        text-transform: capitalize;
        list-style-image: url('../assets/building.png')
    }
   .profileInfo p {
        text-align: left;
        padding-left: 10px;
    }
    .customerName {
        font-family: 'Rubik', sans-serif;
        font-size: 24px;
        font-style: normal;
        font-weight: 500;
        line-height: 28px;
        letter-spacing: 0px;
        text-align: left;
        margin: 20px 0px 0px 0px;
    }
    .customerUserName {
        margin: 0px;
        color: #909090;
      

    }
    .customer a {
        text-decoration: none;
        color: inherit;
    }

    .companyCatchPhrase {
        color: #51C5FF;
    }

    .profilePicture {
        width: 100%;
        height: auto;
        
        
    }
    .profileImageContainer {
        width: 100%;
        height: 300px;
        overflow: hidden;
    }
    .profileInfo {
        padding: 15px;
    }
    .customerName, .customerUserName, .companyCatchPhrase {
       padding-left: 25px ;
       text-align: left;
   }

    @media only screen and (max-width: 900px) {
        .customer {
            max-width: 300px;
            margin: 15px;
        }
    }

   @media only screen and (max-width: 600px) {
       .upperInfo {
            display: grid; 
            grid-template-columns: 1.1fr 1.1fr; 
            grid-template-rows: 1fr; 
            gap: 0px 0px; 
            grid-template-areas: 
                "info img"; 
            padding-left: 10px;
       }  
    
       .profileHeading { 
           grid-area: info; 
           padding: 10px;
        }
        .customerName, .customerUserName, .companyCatchPhrase {
            padding: 0px;
        }  
        .profileInfo {
            padding: 10px;
        }        

        .profilePicture {
            width: auto;
            margin: 25px 5px 5px 0px;
        }

        .profileImageContainer { 
            grid-area: img; 
            height: auto 
        }
        
        .customer {
            margin: 10px;
            min-height: auto;
            
        }
    }
    
</style>