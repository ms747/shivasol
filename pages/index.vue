<template>
  <div class="body">
    <nav>
        <ul class="menu">
            <MenuItem :name="brand" :isBrand="true"/>
            <div class="spacer"></div>
            <MenuItem v-for="item in menuitem" v-bind:key="item.ID" v-bind:name="item" :isBrand="false"/>
        </ul>
    </nav>

    <section class="img-slider " style="display:flex;">
        <div class="siema">
            <Slide v-for="myslide in slide" v-bind:key="myslide.id" :slide="myslide" :imgsrcs="slidesImg"/>
        </div>
    </section>

    <section class="features">
        <h1>Features</h1>
        <div class="features-grid">
            <div class="card">
                <h2>
                    <i id="icon" class="fa fa-tv"></i>
                </h2>
                <h2 class="feature-subheading">Migration</h2>
                <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fugit quos aliquam quisquam, alias rerum consectetur,
                    sapiente sit voluptates modi earum dolores ipsa est officiis eveniet!</p>
            </div>
            <div class="card">
                <h2>
                    <i id="icon" class="fa fa-fire"></i>
                </h2>
                <h2 class="feature-subheading">Firewall</h2>
                <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fugit quos aliquam quisquam, alias rerum consectetur,
                    sapiente sit voluptates modi earum dolores ipsa est officiis eveniet!</p>
            </div>
            <div class="card">
                <h2>
                    <i id="icon" class="fa fa-ambulance"></i>
                </h2>
                <h2 class="feature-subheading">GPS Tracking</h2>
                <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fugit quos aliquam quisquam, alias rerum consectetur,
                    sapiente sit voluptates modi earum dolores ipsa est officiis eveniet!</p>
            </div>
            <div class="card">
                <h2>
                    <i id="icon" class="fa fa-plus"></i>
                </h2>
                <h2 class="feature-subheading">AMC Services</h2>
                <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fugit quos aliquam quisquam, alias rerum consectetur,
                    sapiente sit voluptates modi earum dolores ipsa est officiis eveniet!</p>
            </div>
            <div class="card">
                <h2>
                    <i id="icon" class="fa fa-comment"></i>
                </h2>
                <h2 class="feature-subheading">Smart School</h2>
                <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fugit quos aliquam quisquam, alias rerum consectetur,
                    sapiente sit voluptates modi earum dolores ipsa est officiis eveniet!</p>
            </div>
            <div class="card">
                <h2>
                    <i id="icon" class="fa fa-credit-card"></i>
                </h2>
                <h2 class="feature-subheading">Web Developement</h2>
                <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fugit quos aliquam quisquam, alias rerum consectetur,
                    sapiente sit voluptates modi earum dolores ipsa est officiis eveniet!</p>
            </div>
        </div>
    </section>

    <section class="contact-us">
        <div class="social">
            <i id="social" class="fab fa-facebook-f"></i>
            <i id="social" class="fab fa-twitter"></i>
            <i id="social" class="fab fa-youtube"></i>
        </div>
        <div class="copyright">
            Copyright
            <span>&copy;</span>
        </div>
    </section>

    <script defer src="https://use.fontawesome.com/releases/v5.0.8/js/all.js"></script>
    <!-- <script src="./node_modules/siema/dist/siema.min.js"></script> -->
    <!-- <script>
        setInterval(() => mySiema.next(), 10000)
    </script> -->
</div>
</template>

<script>
import "./style.css";
import MenuItem from "../components/MenuItem";
import Slide from "../components/Slides";
import axios from "axios";
import Siema from 'siema';
export default {
  components: {
    MenuItem,
    Slide
  },
  mounted(){
    let mysiema = new Siema({
        selector: '.siema',
        perPage: 1,
        draggable : true,
        duration: 250,
        loop:true,
    });      
    setInterval(function(){
        mysiema.next();
    }.bind(this),10000);       
  },
  data: function() {
    return {
      brand: {
        title: "Shivasol"
      },
      menuitem: [],
      slide: [],
      slidesImg: [],
    };
  },
  async asyncData() {
    let menu = await axios.get(
      "http://localhost/wordpress/wp-json/myroutes/menu"
    );
    let slides = await axios.get(
      "http://localhost/wordpress/wp-json/wp/v2/shivasol_services"
    );
    let imgsrc = [];
    for (let i = 0; i < slides.data.length; i++) {
      let src = await axios.get(
        slides.data[i]._links["wp:featuredmedia"]["0"].href
      );
      imgsrc.push({ imgsrc: src.data.source_url });
    }

    for (let i = 0; i < slides.data.length; i++) {
      slides.data[i].wpimgsrc = imgsrc[i];
    }
    return {
      menuitem: menu.data,
      slide: slides.data,
      slidesImg: imgsrc
    };
  },
};
</script>

<style>

</style>
