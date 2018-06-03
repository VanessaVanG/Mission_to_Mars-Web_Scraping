

```python
import pandas as pd
import requests

from selenium import webdriver
from splinter import Browser
from bs4 import BeautifulSoup
```

### NASA Mars News


```python
#Mars News url
news_url = 'https://mars.nasa.gov/news'

#browser setup
executable_path = {'executable_path': 'chromedriver.exe'}
browser = Browser('chrome')
browser.visit(news_url)

#create BeautifulSoup object and parse
soup = BeautifulSoup(browser.html, 'html.parser')
```


```python
#find the latest news title and remove newline characters
news_title = soup.find(class_='content_title').get_text(strip=True)

news_title
```




    'NASA CubeSats Steer Toward Mars'




```python
#find the latest news paragraph text and remove newline characters
news_p = soup.find(class_='rollover_description_inner').get_text(strip=True)

news_p
```




    'NASA has achieved a first for the class of tiny spacecraft known as CubeSats, which are opening new access to space.'



### JPL Mars Space Images - Featured Image


```python
#JPL Mars images url
img_url = 'https://www.jpl.nasa.gov/spaceimages/?search=&category=Mars'
img_base_url = 'https://www.jpl.nasa.gov'

#retrieve
result = requests.get(img_url)

#check if okay
result.ok
```




    True




```python
#make it text
html = result.text

#create BeautifulSoup object and parse
soup = BeautifulSoup(html, 'html.parser')
print(soup.prettify())
```

    <!DOCTYPE html>
    <!--[if IE 9]> <html class="no-js ie ie9" lang="en"> <![endif]-->
    <!--[if IE 8]> <html class="no-js ie ie8" lang="en"> <![endif]-->
    <html>
     <!-- START HEADER: "DEFAULT" -->
     <head>
      <meta charset="utf-8"/>
      <!-- Always force latest IE rendering engine or request Chrome Frame -->
      <meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible"/>
      <meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" name="viewport"/>
      <title>
       Space Images
      </title>
      <link href="/assets/stylesheets/manifest.css" media="all" rel="stylesheet" type="text/css"/>
      <link href="/assets/stylesheets/print.css" media="print" rel="stylesheet" type="text/css"/>
      <script src="/assets/javascripts/public_manifest.js" type="text/javascript">
      </script>
      <script src="/assets/javascripts/vendor/jquery.fancybox.js" type="text/javascript">
      </script>
      <script src="/assets/javascripts/vendor/jquery.fancybox-thumbs.js" type="text/javascript">
      </script>
     </head>
     <body class="dark_background logged_out mobile_menu" id="images">
      <!--[if lt IE 9]>
          <div class='browsehappy' style='font-size: 30px; color: white; position:absolute; top: 0; margin: 0; height: 3000px; width: 100%; background: #000; z-index: 10000; padding: 5%;'>
            You are using an
            <strong>outdated</strong>
            browser. Please
            <a href='http://browsehappy.com/'>click here</a>
            to upgrade or change your browser.
          </div>
        <![endif]-->
      <div id="main_container">
       <div id="site_body">
        <div class="site_header_area">
         <header class="site_header">
          <div class="brand_area">
           <div class="brand1">
            <a class="nasa_logo" href="http://www.nasa.gov" title="NASA">
             NASA
            </a>
           </div>
           <div class="brand2">
            <div class="jpl_logo">
             <a href="//www.jpl.nasa.gov/" id="jpl_logo" title="Jet Propulsion Laboratory">
              Jet Propulsion Laboratory
             </a>
            </div>
            <div class="caltech_logo">
             <a href="http://www.caltech.edu/" id="caltech_logo" target="_blank" title="California Institute of Technology">
              California Institute of Technology
             </a>
            </div>
           </div>
           <img alt="" class="print_only print_logo" src="/assets/images/logo_nasa_trio_black@2x.png"/>
          </div>
          <a class="visuallyhidden focusable" href="#main">
           Skip Navigation
          </a>
          <div class="nav_area">
           <a class="menu_button" href="javascript:void(0);" id="menu_button" title="menu button">
            <span class="menu_icon">
             menu and search
            </span>
           </a>
          </div>
         </header>
        </div>
        <div class="main_nav_overlay">
         <div class="modal_menu">
          <header class="site_header clearfix">
           <div class="brand_area">
            <div class="brand1">
             <a class="nasa_logo" href="http://www.nasa.gov" title="">
             </a>
            </div>
            <div class="brand2">
             <div class="jpl_logo">
              <a class="" href="" id="jpl_logo" title="">
               Jet Propulsion Laboratory
              </a>
             </div>
             <div class="caltech_logo">
              <a class="" href="" id="caltech_logo" title="">
               California Institute of Technology
              </a>
             </div>
            </div>
            <img alt="" class="print_only print_logo" src="/assets/images/logo_nasa_trio_black@2x.png"/>
           </div>
           <a class="modal_close" id="modal_close" title="close menu">
            close menu
           </a>
           <div class="nav_area">
            <a class="menu_button modal_close" href="javascript:void(0);" id="menu_button" title="menu icon">
             <span class="menu_icon">
              menu
             </span>
            </a>
           </div>
          </header>
          <section class="navigation_area">
           <div class="grid_layout">
            <div class="directory">
             <form action="/search.php" class="overlay_search top_search">
              <input class="search_field" name="q" onblur="this.placeholder = 'search'" onfocus="this.placeholder = ''" placeholder="search" type="text" value=""/>
              <input class="search_submit" type="submit" value=""/>
             </form>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/about">
                about JPL
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/about">
                 about JPL
                </a>
               </li>
               <li>
                <a href="/about/exec.php">
                 executive council
                </a>
               </li>
               <li>
                <a href="/about/history.php">
                 history
                </a>
               </li>
               <li>
                <a href="/about/reports.php">
                 annual reports
                </a>
               </li>
               <li>
                <a href="/contact_JPL.php">
                 contact us
                </a>
               </li>
               <li>
                <a href="/opportunities/">
                 opportunities
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/events">
                public events
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/events">
                 overview
                </a>
               </li>
               <li>
                <a href="/events/tours/views">
                 tours
                </a>
               </li>
               <li>
                <a href="/events/lectures.php">
                 lecture series
                </a>
               </li>
               <li>
                <a href="/events/speakers-bureau.php">
                 speakers bureau
                </a>
               </li>
               <li>
                <a href="/events/team-competitions.php">
                 team competitions
                </a>
               </li>
               <li>
                <a href="/events/special-events.php">
                 special events
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/edu/">
                education
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/edu/intern/">
                 Intern
                </a>
               </li>
               <li>
                <a href="/edu/learn/">
                 Learn
                </a>
               </li>
               <li>
                <a href="/edu/teach/">
                 Teach
                </a>
               </li>
               <li>
                <a href="/edu/news/">
                 News
                </a>
               </li>
               <li>
                <a href="/edu/events/">
                 Events
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/news">
                news
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/news">
                 latest news
                </a>
               </li>
               <li>
                <a href="/news/presskits.php">
                 press kits
                </a>
               </li>
               <li>
                <a href="/news/factsheets.php">
                 fact sheets
                </a>
               </li>
               <li>
                <a href="/news/mediainformation.php">
                 media information
                </a>
               </li>
               <li>
                <a href="http://blogs.jpl.nasa.gov">
                 blog
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/missions/">
                missions
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/missions/?type=current">
                 current
                </a>
               </li>
               <li>
                <a href="/missions/?type=past">
                 past
                </a>
               </li>
               <li>
                <a href="/missions/?type=future">
                 future
                </a>
               </li>
               <li>
                <a href="/missions/?type=proposed">
                 proposed
                </a>
               </li>
               <li>
                <a href="/missions">
                 all
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/spaceimages">
                galleries
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/spaceimages">
                 images
                </a>
               </li>
               <li>
                <a href="/videos">
                 videos
                </a>
               </li>
               <li>
                <a href="/infographics">
                 infographics
                </a>
               </li>
               <li>
                <a href="/multimedia/audio.php">
                 audio
                </a>
               </li>
               <li>
                <a href="/apps/">
                 apps
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item centered">
              <h3 class="nav_title">
               <a href="/social">
                Follow JPL
               </a>
              </h3>
              <div class="social_icons">
               <!-- AddThis Button BEGIN -->
               <div class="addthis_toolbox addthis_default_style addthis_32x32_style">
                <a addthis:userid="NASAJPL" class="addthis_button_facebook_follow icon">
                </a>
                <a addthis:userid="NASAJPL" class="addthis_button_twitter_follow icon">
                </a>
                <a addthis:userid="JPLnews" class="addthis_button_youtube_follow icon">
                </a>
                <a addthis:userid="nasajpl" class="addthis_button_instagram_follow icon">
                </a>
                <a class="icon all_icon" href="/social">
                 <span>
                  All
                 </span>
                </a>
               </div>
              </div>
             </div>
             <form action="/search.php" class="overlay_search">
              <input class="search_field" name="q" onblur="this.placeholder = 'search'" onfocus="this.placeholder = ''" placeholder="search" type="text" value=""/>
              <input class="search_submit" type="submit" value=""/>
             </form>
            </div>
           </div>
          </section>
         </div>
        </div>
        <a name="main">
        </a>
        <div id="page">
         <!-- END HEADER: "DEFAULT" -->
         <!-- START CONTENT -->
         <section class="centered_text clearfix main_feature primary_media_feature single">
          <div class="carousel_container">
           <div class="carousel_items">
            <article alt="NuSTAR Stares at the Sun" class="carousel_item" style="background-image: url('/spaceimages/images/wallpaper/PIA19821-1920x1200.jpg');">
             <div class="default floating_text_area ms-layer">
              <h2 class="category_title">
              </h2>
              <h2 class="brand_title">
               FEATURED IMAGE
              </h2>
              <h1 class="media_feature_title">
               NuSTAR Stares at the Sun
              </h1>
              <div class="description">
              </div>
              <footer>
               <a class="button fancybox" data-description="Flaring, active regions of our sun are highlighted in this image combining observations from several telescopes. During the observations, microflares went off, which are smaller versions of the larger flares that also erupt from the sun's surface." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/mediumsize/PIA19821_ip.jpg" data-link="/spaceimages/details.php?id=PIA19821" data-title="NuSTAR Stares at the Sun" id="full_image">
                FULL IMAGE
               </a>
              </footer>
             </div>
             <div class="gradient_container_top">
             </div>
             <div class="gradient_container_bottom">
             </div>
            </article>
           </div>
          </div>
         </section>
         <section class="filter_bar module">
          <div class="grid_layout">
           <header>
            <h2 class="module_title_small">
             Mars Images
            </h2>
            <div class="arrow_box">
             <span class="arrow_down">
             </span>
            </div>
           </header>
           <form action="#submit" class="section_search">
            <div class="search_binder">
             <input class="search_field" name="search" onblur="this.placeholder = 'search'" onfocus="this.placeholder = ''" placeholder="search" type="text" value=""/>
             <input class="search_submit" type="submit" value=""/>
            </div>
            <select name="category" onchange="this.form.submit()">
             <option value="">
              All
             </option>
             <option value="featured">
              Featured
             </option>
             <option value="Asteroids and Comets">
              Asteroids and Comets
             </option>
             <option value="Dwarf Planet">
              Dwarf Planet
             </option>
             <option value="Earth">
              Earth
             </option>
             <option value="Ida">
              Ida
             </option>
             <option value="Jupiter">
              Jupiter
             </option>
             <option selected="selected" value="Mars">
              Mars
             </option>
             <option value="Mercury">
              Mercury
             </option>
             <option value="Neptune">
              Neptune
             </option>
             <option value="Saturn">
              Saturn
             </option>
             <option value="Spacecraft and Technology">
              Spacecraft and Technology
             </option>
             <option value="Spacecraft and Telescope">
              Spacecraft and Telescope
             </option>
             <option value="Sun">
              Sun
             </option>
             <option value="Universe">
              Universe
             </option>
             <option value="Uranus">
              Uranus
             </option>
             <option value="Venus">
              Venus
             </option>
            </select>
           </form>
          </div>
         </section>
         <div class="filter_bar_spanner">
         </div>
         <script src="/assets/javascripts/grid_list_page.js" type="text/javascript">
         </script>
         <script>
          function build_image_item(data){
                var html = "<li class=\"slide\">";
    			html += "<a class='fancybox' data-fancybox-group='images' data-fancybox-href='" + data.images.full.src +"' data-title='" + data.title + "' data-description='" + data.tease + "' data-link='" + data.link + "' data-thumbnail='" + data.images.thumb.src + "'>";
                html +=       "<div class=\"image_and_description_container\">";
                html +=         "<div class=\"rollover_description\" style=\"word-wrap: break-word;\">";
                html +=		      "<h3 class=\"release_date\">"+data.date+"<\/h3>";
    		    html +=		      "<div class=\"item_tease_overlay\">"+data.title+"<\/div>";
                html +=           "<div class=\"overlay_arrow\">";
                html +=             "<img alt=\"more arrow\" src=\"/assets/images/overlay-arrow.png\">";
                html +=           "<\/div>";
                html +=         "<\/div>";
                html +=         "<div class=\"img\"><img alt=\""+data.images.thumb.alt+"\" class=\"thumb\" src=\""+data.images.thumb.src+"\"><\/div>";
                html +=         "<div class=\"list_text_content\">";
                html +=		      "<div class=\"article_teaser_body\">"+data.date+"<\/div>";
                html +=           "<div class=\"content_title\">";
                html +=             data.title
                html +=           "<\/div>";
                html +=           "<div class=\"article_teaser_body\">"
                html +=             data.tease
                html +=           "<\/div>"
                html +=         "<\/div>"
                html +=       "<\/div>"
                html +=  "<\/a>";
                html +=  "<\/li>";
                return html;
            };
    		$(document).ready(function(){
    			$('ul.articles').more_items({"url": "/assets/json/getMore.php?images=true&" + $.param(mb_utils._getQueryParams()), "build_item_fn": build_image_item})
    		});
         </script>
         <section class="grid_gallery module grid_view">
          <div class="grid_layout">
           <header>
            <h2 class="module_title">
             Mars Images
            </h2>
            <div class="view_selectors">
             <a class="nav_item ir list_icon">
              list view
             </a>
             <a class="nav_item ir grid_icon">
              grid view
             </a>
            </div>
           </header>
           <ul class="articles">
            <li class="slide">
             <a class="fancybox" data-description="The northern margin of Terra Sabaea is a complex area between a cratered highland and complexly eroded lower plains. This image of the region captured by NASA's 2001 Mars Odyssey spacecraft shows just one of the numerous unnamed channels." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22405_hires.jpg" data-link="/spaceimages/details.php?id=PIA22405" data-thumbnail="/spaceimages/images/wallpaper/PIA22405-640x350.jpg" data-title="Terra Sabaea">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 June 1, 2018
                </h3>
                <div class="item_tease_overlay">
                 Terra Sabaea
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Terra Sabaea" class="thumb" src="/spaceimages/images/wallpaper/PIA22405-640x350.jpg" title="Terra Sabaea"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 June 1, 2018
                </div>
                <div class="content_title">
                 Terra Sabaea
                </div>
                <div class="article_teaser_body">
                 The northern margin of Terra Sabaea is a complex area between a cratered highland and complexly eroded lower plains. This image of the region captured by NASA's 2001 Mars Odyssey spacecraft shows just one of the numerous unnamed channels.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows part of the 'rim' of Orcus Patera. Along the east facing ridge walls in this image multiple regions of dark slope streaks are visible. How Orcus Patera formed is a mystery." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22404_hires.jpg" data-link="/spaceimages/details.php?id=PIA22404" data-thumbnail="/spaceimages/images/wallpaper/PIA22404-640x350.jpg" data-title="Dark Slope Streaks">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 31, 2018
                </h3>
                <div class="item_tease_overlay">
                 Dark Slope Streaks
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Dark Slope Streaks" class="thumb" src="/spaceimages/images/wallpaper/PIA22404-640x350.jpg" title="Dark Slope Streaks"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 31, 2018
                </div>
                <div class="content_title">
                 Dark Slope Streaks
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows part of the 'rim' of Orcus Patera. Along the east facing ridge walls in this image multiple regions of dark slope streaks are visible. How Orcus Patera formed is a mystery.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows Moreux Crater, located in the northern part of Terra Sabaea. The crater has a region of sand dunes on the crater floor, as well as features that are similar to glacial topography on Earth." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22403_hires.jpg" data-link="/spaceimages/details.php?id=PIA22403" data-thumbnail="/spaceimages/images/wallpaper/PIA22403-640x350.jpg" data-title="Moreux Crater Dunes">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 30, 2018
                </h3>
                <div class="item_tease_overlay">
                 Moreux Crater Dunes
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Moreux Crater Dunes" class="thumb" src="/spaceimages/images/wallpaper/PIA22403-640x350.jpg" title="Moreux Crater Dunes"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 30, 2018
                </div>
                <div class="content_title">
                 Moreux Crater Dunes
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows Moreux Crater, located in the northern part of Terra Sabaea. The crater has a region of sand dunes on the crater floor, as well as features that are similar to glacial topography on Earth.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter shows Hale Crater, a large impact crater (more than 100 kilometers) with a suite of interesting features such as active gullies, active recurring slope lineae, and extensive icy ejecta flows." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22465_hires.jpg" data-link="/spaceimages/details.php?id=PIA22465" data-thumbnail="/spaceimages/images/wallpaper/PIA22465-640x350.jpg" data-title="Bedrock Exposed in the Rim of Hale Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 29, 2018
                </h3>
                <div class="item_tease_overlay">
                 Bedrock Exposed in the Rim of Hale Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Bedrock Exposed in the Rim of Hale Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22465-640x350.jpg" title="Bedrock Exposed in the Rim of Hale Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 29, 2018
                </div>
                <div class="content_title">
                 Bedrock Exposed in the Rim of Hale Crater
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter shows Hale Crater, a large impact crater (more than 100 kilometers) with a suite of interesting features such as active gullies, active recurring slope lineae, and extensive icy ejecta flows.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter (MRO) shows the permanent polar cap of Mars, encircled by sand dunes and looking like pulled threads, these dunes march across a fabric of patterned ground." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22464_hires.jpg" data-link="/spaceimages/details.php?id=PIA22464" data-thumbnail="/spaceimages/images/wallpaper/PIA22464-640x350.jpg" data-title="Corduroy Dunes">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 29, 2018
                </h3>
                <div class="item_tease_overlay">
                 Corduroy Dunes
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Corduroy Dunes" class="thumb" src="/spaceimages/images/wallpaper/PIA22464-640x350.jpg" title="Corduroy Dunes"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 29, 2018
                </div>
                <div class="content_title">
                 Corduroy Dunes
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter (MRO) shows the permanent polar cap of Mars, encircled by sand dunes and looking like pulled threads, these dunes march across a fabric of patterned ground.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="In early Martian summer, at the time NASA's Mars Reconnaissance Orbiter (MRO) acquired this image, the dunes are almost free of their seasonal ice cover." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22463_hires.jpg" data-link="/spaceimages/details.php?id=PIA22463" data-thumbnail="/spaceimages/images/wallpaper/PIA22463-640x350.jpg" data-title="Patches of Snow">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 29, 2018
                </h3>
                <div class="item_tease_overlay">
                 Patches of Snow
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Patches of Snow" class="thumb" src="/spaceimages/images/wallpaper/PIA22463-640x350.jpg" title="Patches of Snow"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 29, 2018
                </div>
                <div class="content_title">
                 Patches of Snow
                </div>
                <div class="article_teaser_body">
                 In early Martian summer, at the time NASA's Mars Reconnaissance Orbiter (MRO) acquired this image, the dunes are almost free of their seasonal ice cover.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="NASA's Mars Reconnaissance Orbiter continually finds new impact sites on Mars. This one occurred within the dense secondary crater field of Corinto Crater. The new crater and its ejecta have distinctive color patterns." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22462_hires.jpg" data-link="/spaceimages/details.php?id=PIA22462" data-thumbnail="/spaceimages/images/wallpaper/PIA22462-640x350.jpg" data-title="A New Impact Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 29, 2018
                </h3>
                <div class="item_tease_overlay">
                 A New Impact Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="A New Impact Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22462-640x350.jpg" title="A New Impact Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 29, 2018
                </div>
                <div class="content_title">
                 A New Impact Crater
                </div>
                <div class="article_teaser_body">
                 NASA's Mars Reconnaissance Orbiter continually finds new impact sites on Mars. This one occurred within the dense secondary crater field of Corinto Crater. The new crater and its ejecta have distinctive color patterns.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft is located on the margin of the Nili Fossae region and Isidis Planitia." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22402_hires.jpg" data-link="/spaceimages/details.php?id=PIA22402" data-thumbnail="/spaceimages/images/wallpaper/PIA22402-640x350.jpg" data-title="Complex Erosion">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 29, 2018
                </h3>
                <div class="item_tease_overlay">
                 Complex Erosion
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Complex Erosion" class="thumb" src="/spaceimages/images/wallpaper/PIA22402-640x350.jpg" title="Complex Erosion"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 29, 2018
                </div>
                <div class="content_title">
                 Complex Erosion
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft is located on the margin of the Nili Fossae region and Isidis Planitia.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows part of the margin of the north polar cap and the surrounding plains. The layering of the ice is easily visible due to the dust that is deposited on the top of the ice every year." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22401_hires.jpg" data-link="/spaceimages/details.php?id=PIA22401" data-thumbnail="/spaceimages/images/wallpaper/PIA22401-640x350.jpg" data-title="Polar Layers">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 28, 2018
                </h3>
                <div class="item_tease_overlay">
                 Polar Layers
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Polar Layers" class="thumb" src="/spaceimages/images/wallpaper/PIA22401-640x350.jpg" title="Polar Layers"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 28, 2018
                </div>
                <div class="content_title">
                 Polar Layers
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows part of the margin of the north polar cap and the surrounding plains. The layering of the ice is easily visible due to the dust that is deposited on the top of the ice every year.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows part of Olympia Undae, a large dune field that surrounds part of the north polar cap. At the top of the image the dunes are small and isolated." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22400_hires.jpg" data-link="/spaceimages/details.php?id=PIA22400" data-thumbnail="/spaceimages/images/wallpaper/PIA22400-640x350.jpg" data-title="Olympia Undae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 25, 2018
                </h3>
                <div class="item_tease_overlay">
                 Olympia Undae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Olympia Undae" class="thumb" src="/spaceimages/images/wallpaper/PIA22400-640x350.jpg" title="Olympia Undae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 25, 2018
                </div>
                <div class="content_title">
                 Olympia Undae
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows part of Olympia Undae, a large dune field that surrounds part of the north polar cap. At the top of the image the dunes are small and isolated.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows the margin between the polar cap and the surrounding plains. There are dunes on the plains at the top of the image." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22399_hires.jpg" data-link="/spaceimages/details.php?id=PIA22399" data-thumbnail="/spaceimages/images/wallpaper/PIA22399-640x350.jpg" data-title="North Polar Layers">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 24, 2018
                </h3>
                <div class="item_tease_overlay">
                 North Polar Layers
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="North Polar Layers" class="thumb" src="/spaceimages/images/wallpaper/PIA22399-640x350.jpg" title="North Polar Layers"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 24, 2018
                </div>
                <div class="content_title">
                 North Polar Layers
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows the margin between the polar cap and the surrounding plains. There are dunes on the plains at the top of the image.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="A close-up image of a 2-inch-deep hole produced using a new drilling technique for NASA's Curiosity rover. Curiosity drilled this hole in a target called 'Duluth' on May 20, 2018." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22326_hires.jpg" data-link="/spaceimages/details.php?id=PIA22326" data-thumbnail="/spaceimages/images/wallpaper/PIA22326-640x350.jpg" data-title="Curiosity Successfully Drills 'Duluth'">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 23, 2018
                </h3>
                <div class="item_tease_overlay">
                 Curiosity Successfully Drills 'Duluth'
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Curiosity Successfully Drills 'Duluth'" class="thumb" src="/spaceimages/images/wallpaper/PIA22326-640x350.jpg" title="Curiosity Successfully Drills 'Duluth'"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 23, 2018
                </div>
                <div class="content_title">
                 Curiosity Successfully Drills 'Duluth'
                </div>
                <div class="article_teaser_body">
                 A close-up image of a 2-inch-deep hole produced using a new drilling technique for NASA's Curiosity rover. Curiosity drilled this hole in a target called 'Duluth' on May 20, 2018.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="NASA's Curiosity rover successfully drilled a 2-inch-deep hole in a target called 'Duluth' on May 20, 2018. It was the first rock sample captured by the drill since October 2016." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22325_hires.jpg" data-link="/spaceimages/details.php?id=PIA22325" data-thumbnail="/spaceimages/images/wallpaper/PIA22325-640x350.jpg" data-title="First Drilled Sample on Mars Since 2016">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 23, 2018
                </h3>
                <div class="item_tease_overlay">
                 First Drilled Sample on Mars Since 2016
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="First Drilled Sample on Mars Since 2016" class="thumb" src="/spaceimages/images/wallpaper/PIA22325-640x350.jpg" title="First Drilled Sample on Mars Since 2016"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 23, 2018
                </div>
                <div class="content_title">
                 First Drilled Sample on Mars Since 2016
                </div>
                <div class="article_teaser_body">
                 NASA's Curiosity rover successfully drilled a 2-inch-deep hole in a target called 'Duluth' on May 20, 2018. It was the first rock sample captured by the drill since October 2016.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Located west of the Elysium Volcanic complex, Hebrus Valles is a complex channel system that flowed to the north. In this image from NASA's 2001 Mars Odyssey spacecraft the channel features have the appearance of a channel formed by liquid flow." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22398_hires.jpg" data-link="/spaceimages/details.php?id=PIA22398" data-thumbnail="/spaceimages/images/wallpaper/PIA22398-640x350.jpg" data-title="Hebrus Valles">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 23, 2018
                </h3>
                <div class="item_tease_overlay">
                 Hebrus Valles
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Hebrus Valles" class="thumb" src="/spaceimages/images/wallpaper/PIA22398-640x350.jpg" title="Hebrus Valles"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 23, 2018
                </div>
                <div class="content_title">
                 Hebrus Valles
                </div>
                <div class="article_teaser_body">
                 Located west of the Elysium Volcanic complex, Hebrus Valles is a complex channel system that flowed to the north. In this image from NASA's 2001 Mars Odyssey spacecraft the channel features have the appearance of a channel formed by liquid flow.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows a section of Cerberus Fossae. Located southeast of the Elysium Planitia volcanic complex, the linear graben was created by tectonic forces related to the volcanic activity." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22397_hires.jpg" data-link="/spaceimages/details.php?id=PIA22397" data-thumbnail="/spaceimages/images/wallpaper/PIA22397-640x350.jpg" data-title="Cerberus Fossae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 22, 2018
                </h3>
                <div class="item_tease_overlay">
                 Cerberus Fossae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Cerberus Fossae" class="thumb" src="/spaceimages/images/wallpaper/PIA22397-640x350.jpg" title="Cerberus Fossae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 22, 2018
                </div>
                <div class="content_title">
                 Cerberus Fossae
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows a section of Cerberus Fossae. Located southeast of the Elysium Planitia volcanic complex, the linear graben was created by tectonic forces related to the volcanic activity.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="The linear channel in the bottom half of this image from NASA's 2001 Mars Odyssey spacecraft is part of Olympica Fossae. Olympica Fossae is a complex channel form located on the Tharsis plains between Alba Mons and Olympus Mons." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22396_hires.jpg" data-link="/spaceimages/details.php?id=PIA22396" data-thumbnail="/spaceimages/images/wallpaper/PIA22396-640x350.jpg" data-title="Olympica Fossae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 21, 2018
                </h3>
                <div class="item_tease_overlay">
                 Olympica Fossae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Olympica Fossae" class="thumb" src="/spaceimages/images/wallpaper/PIA22396-640x350.jpg" title="Olympica Fossae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 21, 2018
                </div>
                <div class="content_title">
                 Olympica Fossae
                </div>
                <div class="article_teaser_body">
                 The linear channel in the bottom half of this image from NASA's 2001 Mars Odyssey spacecraft is part of Olympica Fossae. Olympica Fossae is a complex channel form located on the Tharsis plains between Alba Mons and Olympus Mons.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows a region of Chryse Chaos where the isolated mesas are beginning to be formed. The interconnected channel forms erode, and mesas are created by erosion of the bounding channels." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22395_hires.jpg" data-link="/spaceimages/details.php?id=PIA22395" data-thumbnail="/spaceimages/images/wallpaper/PIA22395-640x350.jpg" data-title="Chryse Chaos">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 18, 2018
                </h3>
                <div class="item_tease_overlay">
                 Chryse Chaos
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Chryse Chaos" class="thumb" src="/spaceimages/images/wallpaper/PIA22395-640x350.jpg" title="Chryse Chaos"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 18, 2018
                </div>
                <div class="content_title">
                 Chryse Chaos
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows a region of Chryse Chaos where the isolated mesas are beginning to be formed. The interconnected channel forms erode, and mesas are created by erosion of the bounding channels.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows an unnamed crater located in Utopia Planitia. This relatively young crater has a steep inner rim, with floor deposits that originate from the crater rim itself." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22394_hires.jpg" data-link="/spaceimages/details.php?id=PIA22394" data-thumbnail="/spaceimages/images/wallpaper/PIA22394-640x350.jpg" data-title="Utopia Planitia Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 17, 2018
                </h3>
                <div class="item_tease_overlay">
                 Utopia Planitia Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Utopia Planitia Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22394-640x350.jpg" title="Utopia Planitia Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 17, 2018
                </div>
                <div class="content_title">
                 Utopia Planitia Crater
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows an unnamed crater located in Utopia Planitia. This relatively young crater has a steep inner rim, with floor deposits that originate from the crater rim itself.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows Gale Crater on Mars, the home of the Curiosity Rover." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22393_hires.jpg" data-link="/spaceimages/details.php?id=PIA22393" data-thumbnail="/spaceimages/images/wallpaper/PIA22393-640x350.jpg" data-title="Gale Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 16, 2018
                </h3>
                <div class="item_tease_overlay">
                 Gale Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Gale Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22393-640x350.jpg" title="Gale Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 16, 2018
                </div>
                <div class="content_title">
                 Gale Crater
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows Gale Crater on Mars, the home of the Curiosity Rover.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows part of Gale Crater. Gale Crater is the home of the Curiosity Rover." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22392_hires.jpg" data-link="/spaceimages/details.php?id=PIA22392" data-thumbnail="/spaceimages/images/wallpaper/PIA22392-640x350.jpg" data-title="Gale Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 15, 2018
                </h3>
                <div class="item_tease_overlay">
                 Gale Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Gale Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22392-640x350.jpg" title="Gale Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 15, 2018
                </div>
                <div class="content_title">
                 Gale Crater
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows part of Gale Crater. Gale Crater is the home of the Curiosity Rover.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter shows barchan sand dunes, common on Mars often forming vast dune fields within very large (tens to hundreds of km) impact basins. The regions upwind of barchans are usually devoid of sandy bedforms." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22456_hires.jpg" data-link="/spaceimages/details.php?id=PIA22456" data-thumbnail="/spaceimages/images/wallpaper/PIA22456-640x350.jpg" data-title="Barchan Pac-Man">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 14, 2018
                </h3>
                <div class="item_tease_overlay">
                 Barchan Pac-Man
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Barchan Pac-Man" class="thumb" src="/spaceimages/images/wallpaper/PIA22456-640x350.jpg" title="Barchan Pac-Man"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 14, 2018
                </div>
                <div class="content_title">
                 Barchan Pac-Man
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter shows barchan sand dunes, common on Mars often forming vast dune fields within very large (tens to hundreds of km) impact basins. The regions upwind of barchans are usually devoid of sandy bedforms.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter (MRO) shows some of these on the slopes of Nectaris Montes within Coprates Chasma on Mars. Sand dunes in Valles Marineris can be impressive in size, with steep slopes that seem to climb and descend." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22455_hires.jpg" data-link="/spaceimages/details.php?id=PIA22455" data-thumbnail="/spaceimages/images/wallpaper/PIA22455-640x350.jpg" data-title="Dunes in Nectaris Montes">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 14, 2018
                </h3>
                <div class="item_tease_overlay">
                 Dunes in Nectaris Montes
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Dunes in Nectaris Montes" class="thumb" src="/spaceimages/images/wallpaper/PIA22455-640x350.jpg" title="Dunes in Nectaris Montes"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 14, 2018
                </div>
                <div class="content_title">
                 Dunes in Nectaris Montes
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter (MRO) shows some of these on the slopes of Nectaris Montes within Coprates Chasma on Mars. Sand dunes in Valles Marineris can be impressive in size, with steep slopes that seem to climb and descend.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter (MRO) shows two small impact craters located in Meridiani Planum on Mars. Small boulders on the floor and walls of the left-side crater." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22454_hires.jpg" data-link="/spaceimages/details.php?id=PIA22454" data-thumbnail="/spaceimages/images/wallpaper/PIA22454-640x350.jpg" data-title="Twin Craters in Meridiani Planum">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 14, 2018
                </h3>
                <div class="item_tease_overlay">
                 Twin Craters in Meridiani Planum
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Twin Craters in Meridiani Planum" class="thumb" src="/spaceimages/images/wallpaper/PIA22454-640x350.jpg" title="Twin Craters in Meridiani Planum"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 14, 2018
                </div>
                <div class="content_title">
                 Twin Craters in Meridiani Planum
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter (MRO) shows two small impact craters located in Meridiani Planum on Mars. Small boulders on the floor and walls of the left-side crater.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter shows two new craters on Mars with the same distinctive pattern of relatively blue ejecta surrounded by a dark blast zone and arcing patterns. This pattern indicates an oblique impact angle with a bolide." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22453_hires.jpg" data-link="/spaceimages/details.php?id=PIA22453" data-thumbnail="/spaceimages/images/wallpaper/PIA22453-640x350.jpg" data-title="A Pair of New Impact Craters">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 14, 2018
                </h3>
                <div class="item_tease_overlay">
                 A Pair of New Impact Craters
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="A Pair of New Impact Craters" class="thumb" src="/spaceimages/images/wallpaper/PIA22453-640x350.jpg" title="A Pair of New Impact Craters"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 14, 2018
                </div>
                <div class="content_title">
                 A Pair of New Impact Craters
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter shows two new craters on Mars with the same distinctive pattern of relatively blue ejecta surrounded by a dark blast zone and arcing patterns. This pattern indicates an oblique impact angle with a bolide.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows a small portion of Olympia Undae, a huge dune field that surrounds part of the north polar cap. This image was taken during summer and there is no frost on the dune forms." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22391_hires.jpg" data-link="/spaceimages/details.php?id=PIA22391" data-thumbnail="/spaceimages/images/wallpaper/PIA22391-640x350.jpg" data-title="Olympia Undae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 14, 2018
                </h3>
                <div class="item_tease_overlay">
                 Olympia Undae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Olympia Undae" class="thumb" src="/spaceimages/images/wallpaper/PIA22391-640x350.jpg" title="Olympia Undae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 14, 2018
                </div>
                <div class="content_title">
                 Olympia Undae
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows a small portion of Olympia Undae, a huge dune field that surrounds part of the north polar cap. This image was taken during summer and there is no frost on the dune forms.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Sand dunes cover this entire image from NASA's 2001 Mars Odyssey spacecraft. The dunes are part of Olympia Undae, a huge dune field surrounding 1/4 of the northern polar cap." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22390_hires.jpg" data-link="/spaceimages/details.php?id=PIA22390" data-thumbnail="/spaceimages/images/wallpaper/PIA22390-640x350.jpg" data-title="Olympia Undae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 11, 2018
                </h3>
                <div class="item_tease_overlay">
                 Olympia Undae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Olympia Undae" class="thumb" src="/spaceimages/images/wallpaper/PIA22390-640x350.jpg" title="Olympia Undae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 11, 2018
                </div>
                <div class="content_title">
                 Olympia Undae
                </div>
                <div class="article_teaser_body">
                 Sand dunes cover this entire image from NASA's 2001 Mars Odyssey spacecraft. The dunes are part of Olympia Undae, a huge dune field surrounding 1/4 of the northern polar cap.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image of Gale Crater from NASA's 2001 Mars Odyssey spacecraft shows part of the huge layered deposit that covers much of the crater floor. The top of the image shows part of the crater rim, including one of the many small channels." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22389_hires.jpg" data-link="/spaceimages/details.php?id=PIA22389" data-thumbnail="/spaceimages/images/wallpaper/PIA22389-640x350.jpg" data-title="Gale Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 10, 2018
                </h3>
                <div class="item_tease_overlay">
                 Gale Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Gale Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22389-640x350.jpg" title="Gale Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 10, 2018
                </div>
                <div class="content_title">
                 Gale Crater
                </div>
                <div class="article_teaser_body">
                 This image of Gale Crater from NASA's 2001 Mars Odyssey spacecraft shows part of the huge layered deposit that covers much of the crater floor. The top of the image shows part of the crater rim, including one of the many small channels.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows part of the interior of Candor Chasma. At the bottom of the frame is a bright feature formed by layers of material deposited in the canyon after it formed." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22388_hires.jpg" data-link="/spaceimages/details.php?id=PIA22388" data-thumbnail="/spaceimages/images/wallpaper/PIA22388-640x350.jpg" data-title="Candor Chasma">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 9, 2018
                </h3>
                <div class="item_tease_overlay">
                 Candor Chasma
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Candor Chasma" class="thumb" src="/spaceimages/images/wallpaper/PIA22388-640x350.jpg" title="Candor Chasma"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 9, 2018
                </div>
                <div class="content_title">
                 Candor Chasma
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows part of the interior of Candor Chasma. At the bottom of the frame is a bright feature formed by layers of material deposited in the canyon after it formed.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="The feature that crosses this image captured by NASA's 2001 Mars Odyssey spacecraft is a graben. Graben are formed by tectonic action, where a block of material moves downward between a pair of faults." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22387_hires.jpg" data-link="/spaceimages/details.php?id=PIA22387" data-thumbnail="/spaceimages/images/wallpaper/PIA22387-640x350.jpg" data-title="Labeatis Fossae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 8, 2018
                </h3>
                <div class="item_tease_overlay">
                 Labeatis Fossae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Labeatis Fossae" class="thumb" src="/spaceimages/images/wallpaper/PIA22387-640x350.jpg" title="Labeatis Fossae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 8, 2018
                </div>
                <div class="content_title">
                 Labeatis Fossae
                </div>
                <div class="article_teaser_body">
                 The feature that crosses this image captured by NASA's 2001 Mars Odyssey spacecraft is a graben. Graben are formed by tectonic action, where a block of material moves downward between a pair of faults.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows the part of the crater rim and ejecta surrounding Lonar Crater in the northern plains of Vastitas Borealis." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22386_hires.jpg" data-link="/spaceimages/details.php?id=PIA22386" data-thumbnail="/spaceimages/images/wallpaper/PIA22386-640x350.jpg" data-title="Lonar Crater Ejecta">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 7, 2018
                </h3>
                <div class="item_tease_overlay">
                 Lonar Crater Ejecta
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Lonar Crater Ejecta" class="thumb" src="/spaceimages/images/wallpaper/PIA22386-640x350.jpg" title="Lonar Crater Ejecta"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 7, 2018
                </div>
                <div class="content_title">
                 Lonar Crater Ejecta
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows the part of the crater rim and ejecta surrounding Lonar Crater in the northern plains of Vastitas Borealis.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the numerous unnamed channels in northern Terra Sabaea." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22384_hires.jpg" data-link="/spaceimages/details.php?id=PIA22384" data-thumbnail="/spaceimages/images/wallpaper/PIA22384-640x350.jpg" data-title="Terra Sabaea Channel">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 4, 2018
                </h3>
                <div class="item_tease_overlay">
                 Terra Sabaea Channel
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Terra Sabaea Channel" class="thumb" src="/spaceimages/images/wallpaper/PIA22384-640x350.jpg" title="Terra Sabaea Channel"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 4, 2018
                </div>
                <div class="content_title">
                 Terra Sabaea Channel
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the numerous unnamed channels in northern Terra Sabaea.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="A group of dunes captured by NASA's 2001 Mars Odyssey spacecraft is visible on the floor of this unnamed crater in Arabia Terra. The dunes contain basaltic sand, which is darker than the dust covered materials of the rest of the crater." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22383_hires.jpg" data-link="/spaceimages/details.php?id=PIA22383" data-thumbnail="/spaceimages/images/wallpaper/PIA22383-640x350.jpg" data-title="Crater Dunes">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 3, 2018
                </h3>
                <div class="item_tease_overlay">
                 Crater Dunes
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Crater Dunes" class="thumb" src="/spaceimages/images/wallpaper/PIA22383-640x350.jpg" title="Crater Dunes"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 3, 2018
                </div>
                <div class="content_title">
                 Crater Dunes
                </div>
                <div class="article_teaser_body">
                 A group of dunes captured by NASA's 2001 Mars Odyssey spacecraft is visible on the floor of this unnamed crater in Arabia Terra. The dunes contain basaltic sand, which is darker than the dust covered materials of the rest of the crater.
                </div>
               </div>
              </div>
             </a>
            </li>
           </ul>
           <footer>
            <div class="more_button">
             <a class="button" href="">
              MORE
             </a>
            </div>
           </footer>
          </div>
         </section>
         <section class="image_teaser module">
          <div class="grid_layout">
           <header>
            <h1 class="module_title">
            </h1>
           </header>
           <ul class="module_gallery gallery_list">
            <li class="slide">
             <div class="image_container">
              <a href="http://photojournal.jpl.nasa.gov/">
               <img alt="jpl photojournal" class="thumb" src="/assets/images/content/tmp/images/jpl_photojournal(3x1).jpg"/>
              </a>
             </div>
             <div class="content_title">
              <a href="http://photojournal.jpl.nasa.gov/">
               JPL Photojournal
              </a>
             </div>
             <div class="article_teaser_body">
              Access to the full library of publicly released images from various Solar System exploration programs
             </div>
            </li>
            <li class="slide">
             <div class="image_container">
              <a href="http://www.nasa.gov/multimedia/imagegallery/">
               <img alt="Great images in NASA" class="thumb" src="/assets/images/content/tmp/images/nasa_images(3x1).jpg"/>
              </a>
             </div>
             <div class="content_title">
              <a href="http://www.nasa.gov/multimedia/imagegallery/">
               Great images in NASA
              </a>
             </div>
             <div class="article_teaser_body">
              A selection of the best-known images from a half-century of exploration and discovery
             </div>
            </li>
           </ul>
          </div>
         </section>
         <section class="multi_teaser module">
          <div class="grid_layout">
           <header>
            <h1 class="module_title">
             You Might Also Like
            </h1>
           </header>
           <ul class="module_gallery gallery_list">
            <li class="slide">
             <a href="//www.jpl.nasa.gov/news/news.php?feature=7147">
              <div class="image_and_description_container">
               <div class="rollover_description">
                NASA has achieved a first for the class of tiny spacecraft known as CubeSats, which are opening new access to space.
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <img alt="An artist's concept of one of NASA's MarCO CubeSats" src="//imagecache.jpl.nasa.gov/images/640x350/marco-16-640x350.jpg"/>
              </div>
              <div class="content_title">
               NASA CubeSats Steer Toward Mars
              </div>
             </a>
            </li>
            <li class="slide">
             <a href="//www.jpl.nasa.gov/news/news.php?feature=7144">
              <div class="image_and_description_container">
               <div class="rollover_description">
                NASA's Dawn spacecraft is maneuvering to its lowest-ever orbit for a close-up examination of the inner solar system's only dwarf planet.
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <img alt="Ceres" src="//imagecache.jpl.nasa.gov/images/640x350/PIA22476-16-640x350.jpg"/>
              </div>
              <div class="content_title">
               Dawn Mission: New Orbit, New Opportunities
              </div>
             </a>
            </li>
            <li class="slide">
             <a href="//www.jpl.nasa.gov/news/news.php?feature=7140">
              <div class="image_and_description_container">
               <div class="rollover_description">
                Take a virtual trip to the imagined surfaces of planets beyond our solar system with NASA's interactive Exoplanet Travel Bureau.
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <img alt="Exoplanet poster" src="//imagecache.jpl.nasa.gov/images/640x350/exoplanet20180523-16-640x350.jpg"/>
              </div>
              <div class="content_title">
               Take a Virtual Trip to a Strange New World with NASA
              </div>
             </a>
            </li>
           </ul>
           <footer>
            <a class="outline_button dark" href="/news">
             more news
            </a>
           </footer>
          </div>
         </section>
         <!-- END CONTENT -->
         <script src="/Scripts/custom_detail.js" type="text/javascript">
         </script>
         <!-- START FOOTER: "DEFAULT" -->
        </div>
        <footer class="clearfix" id="site_footer">
         <section class="upper_footer">
          <div class="grid_layout">
           <div class="footer_newsletter">
            <h2>
             Get the Newsletter
            </h2>
            <form action="/signup/index.php" class="submit_newsletter" method="post">
             <input class="email_field" name="email_field" onblur="this.placeholder = 'enter email address'" onfocus="this.placeholder = ''" placeholder="enter email address" type="email" value=""/>
             <input class="email_submit" type="submit" value=""/>
            </form>
           </div>
           <div class="gradient_line_divider">
           </div>
           <div class="share">
            <h2>
             Follow JPL
            </h2>
            <div class="social_icons">
             <!-- AddThis Button BEGIN -->
             <div class="addthis_toolbox addthis_default_style addthis_32x32_style">
              <a addthis:userid="NASAJPL" class="addthis_button_facebook_follow icon">
              </a>
              <a addthis:userid="NASAJPL" class="addthis_button_twitter_follow icon">
              </a>
              <a addthis:userid="JPLnews" class="addthis_button_youtube_follow icon">
              </a>
              <a addthis:userid="nasajpl" class="addthis_button_instagram_follow icon">
              </a>
              <a class="icon all_icon" href="/social">
               <span>
                All
               </span>
              </a>
             </div>
             <script>
              addthis_loader.init("//s7.addthis.com/js/300/addthis_widget.js#pubid=ra-5429eeee4e460927", {follow: true})
             </script>
            </div>
           </div>
          </div>
          <div class="gradient_line">
          </div>
         </section>
         <section class="sitemap">
          <div class="grid_layout">
           <div class="sitemap_directory">
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               about JPL
              </h3>
              <ul class="subnav">
               <li>
                <a href="/about/">
                 About JPL
                </a>
               </li>
               <li>
                <a href="/about/exec.php">
                 Executive Council
                </a>
               </li>
               <li>
                <a href="/about/history.php">
                 History
                </a>
               </li>
               <li>
                <a href="/about/reports.php">
                 Annual Reports
                </a>
               </li>
               <li>
                <a href="/contact_JPL.php">
                 Contact Us
                </a>
               </li>
               <li>
                <a href="/opportunities/">
                 Opportunities
                </a>
               </li>
               <li>
                <a href="/acquisition/">
                 Doing Business with JPL
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               missions
              </h3>
              <ul class="subnav">
               <li>
                <a href="/missions/?type=current">
                 Current
                </a>
               </li>
               <li>
                <a href="/missions/?type=past">
                 Past
                </a>
               </li>
               <li>
                <a href="/missions/?type=future">
                 Future
                </a>
               </li>
               <li>
                <a href="/missions/?type=proposed">
                 Proposed
                </a>
               </li>
               <li>
                <a href="/missions">
                 All
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               galleries
              </h3>
              <ul class="subnav">
               <li>
                <a href="/spaceimages/">
                 JPL Space Images
                </a>
               </li>
               <li>
                <a href="/videos/">
                 Videos
                </a>
               </li>
               <li>
                <a href="/infographics/">
                 Infographics
                </a>
               </li>
               <li>
                <a href="https://photojournal.jpl.nasa.gov/">
                 Photojournal
                </a>
               </li>
               <li>
                <a href="http://www.nasaimages.org/">
                 NASA Images
                </a>
               </li>
               <li>
                <a href="/apps/">
                 Mobile Apps
                </a>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               education
              </h3>
              <ul class="subnav">
               <li>
                <a href="/edu/intern/">
                 Intern
                </a>
               </li>
               <li>
                <a href="/edu/learn/">
                 Learn
                </a>
               </li>
               <li>
                <a href="/edu/teach/">
                 Teach
                </a>
               </li>
               <li>
                <a href="/edu/news/">
                 News
                </a>
               </li>
               <li>
                <a href="/edu/events/">
                 Events
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               news
              </h3>
              <ul class="subnav">
               <li>
                <a href="/news">
                 Latest News
                </a>
               </li>
               <li>
                <a href="/news/presskits.php">
                 Press Kits
                </a>
               </li>
               <li>
                <a href="/news/factsheets.php">
                 Fact Sheets
                </a>
               </li>
               <li>
                <a href="/news/mediainformation.php">
                 Media Information
                </a>
               </li>
               <li>
                <a href="/universe/">
                 Universe Newspaper
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               public events
              </h3>
              <ul class="subnav">
               <li>
                <a href="/events/">
                 Overview
                </a>
               </li>
               <li>
                <a href="/events/tours/views/">
                 Tours
                </a>
               </li>
               <li>
                <a href="/events/lectures.php">
                 Lecture Series
                </a>
               </li>
               <li>
                <a href="/events/speakers-bureau.php">
                 Speakers Bureau
                </a>
               </li>
               <li>
                <a href="/events/team-competitions.php">
                 Team Competitions
                </a>
               </li>
               <li>
                <a href="/events/special-events.php">
                 Special Events
                </a>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               Our Sites
              </h3>
              <ul class="subnav">
               <li>
                <a href="/asteroidwatch/">
                 Asteroid Watch
                </a>
               </li>
               <li>
                <a href="http://saturn.jpl.nasa.gov/index.cfm">
                 Cassini - Mission to Saturn
                </a>
               </li>
               <li>
                <a href="http://climate.nasa.gov">
                 Earth / Global Climate Change
                </a>
               </li>
               <li>
                <a href="http://planetquest.jpl.nasa.gov">
                 Exoplanet Exploration
                </a>
               </li>
               <li>
                <a href="/missions/juno/">
                 Juno - Mission to Jupiter
                </a>
               </li>
               <li>
                <a href="http://marsprogram.jpl.nasa.gov/">
                 Mars Exploration
                </a>
               </li>
               <li>
                <a href="http://marsprogram.jpl.nasa.gov/msl/">
                 Mars Science Laboratory / Curiosity
                </a>
               </li>
               <li>
                <a href="http://rosetta.jpl.nasa.gov/">
                 Rosetta - Understanding Comets
                </a>
               </li>
               <li>
                <a href="http://scienceandtechnology.jpl.nasa.gov/">
                 Science and Technology
                </a>
               </li>
               <li>
                <a href="http://solarsystem.nasa.gov/">
                 Solar System Exploration
                </a>
               </li>
               <li>
                <a href="http://eyes.nasa.gov/">
                 Eyes on the Solar System
                </a>
               </li>
               <li>
                <a href="http://eyes.nasa.gov/earth/">
                 Eyes on the Earth
                </a>
               </li>
               <li>
                <a href="http://eyes.nasa.gov/exoplanets/">
                 Eyes on Exoplanets
                </a>
               </li>
               <li>
                <a href="http://www.spitzer.caltech.edu/">
                 Spitzer Space Telescope
                </a>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               Follow JPL
              </h3>
              <ul class="subnav">
               <li>
                <a href="/signup/">
                 Newsletter
                </a>
               </li>
               <li>
                <a href="https://www.facebook.com/NASAJPL">
                 Facebook
                </a>
               </li>
               <li>
                <a href="http://twitter.com/NASAJPL">
                 Twitter
                </a>
               </li>
               <li>
                <a href="http://www.youtube.com/user/JPLnews">
                 YouTube
                </a>
               </li>
               <li>
                <a href="http://www.flickr.com/photos/nasa-jpl">
                 Flickr
                </a>
               </li>
               <li>
                <a href="http://instagram.com/nasajpl">
                 Instagram
                </a>
               </li>
               <li>
                <a href="https://www.linkedin.com/company/2004/">
                 LinkedIn
                </a>
               </li>
               <li>
                <a href="http://itunes.apple.com/podcast/hd-nasas-jet-propulsion-laboratory/id262254981">
                 iTunes
                </a>
               </li>
               <li>
                <a href="http://www.ustream.tv/nasajpl">
                 UStream
                </a>
               </li>
               <li>
                <a href="/rss/">
                 RSS
                </a>
               </li>
               <li>
                <a href="http://blogs.jpl.nasa.gov">
                 Blog
                </a>
               </li>
               <li>
                <a href="/onthego/">
                 Mobile
                </a>
               </li>
               <li>
                <a href="/social/">
                 All Social Media
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               NASA
              </h3>
              <ul class="subnav">
               <li>
                <a href="http://jplwater.nasa.gov">
                 NASA Water Cleanup
                </a>
               </li>
               <li>
                <a href="http://www.hq.nasa.gov/office/pao/FOIA/agency/">
                 FOIA
                </a>
               </li>
              </ul>
             </div>
            </div>
           </div>
          </div>
          <div class="gradient_line">
          </div>
         </section>
         <section class="lower_footer">
          <div class="nav_container">
           <nav>
            <ul>
             <li>
              <a href="http://www.nasa.gov/" target="_blank">
               NASA
              </a>
             </li>
             |
             <li>
              <a href="http://www.caltech.edu/" target="_blank">
               Caltech
              </a>
             </li>
             |
             <li>
              <a href="/copyrights.php">
               Privacy
              </a>
             </li>
             |
             <li>
              <a href="/imagepolicy">
               Image Policy
              </a>
             </li>
             |
             <li>
              <a href="/faq.php">
               FAQ
              </a>
             </li>
             |
             <li>
              <a href="/contact_JPL.php">
               Feedback
              </a>
             </li>
            </ul>
           </nav>
          </div>
          <div class="credits">
           <span class="credits_manager">
            Site Manager: Jon Nelson
           </span>
           <span class="credits_webmaster">
            Webmasters: Tony Greicius, Luis Espinoza, Anil Natha
           </span>
          </div>
         </section>
        </footer>
       </div>
      </div>
      <script src="/assets/javascripts/vendor/prefixfree.js" type="text/javascript">
      </script>
      <script src="/assets/javascripts/vendor/prefixfree.jquery.js" type="text/javascript">
      </script>
      <script id="_fed_an_ua_tag" src="https://dap.digitalgov.gov/Universal-Federated-Analytics-Min.js?agency=NASA&amp;pua=UA-45212297-1&amp;subagency=JPL&amp;dclink=true&amp;sp=search,s,q&amp;sdor=false&amp;exts=tif,tiff" type="text/javascript">
      </script>
      <script type="text/javascript">
       setTimeout(function(){var a=document.createElement("script");
    var b=document.getElementsByTagName("script")[0];
    a.src=document.location.protocol+"//script.crazyegg.com/pages/scripts/0025/5267.js?"+Math.floor(new Date().getTime()/3600000);
    a.async=true;a.type="text/javascript";b.parentNode.insertBefore(a,b)}, 1);
      </script>
     </body>
     <!-- END FOOTER: "DEFAULT" -->
    </html>
    


```python
#select the part that contains the image urls
fancy_box = soup.select('li.slide a.fancybox')

#make a list of just the data-fancybox-hrefs
img_list = [i.get('data-fancybox-href') for i in fancy_box]

#combine the base url with the first img url
featured_image_url = img_base_url + img_list[0]   

print(featured_image_url)
```

    https://www.jpl.nasa.gov/spaceimages/images/largesize/PIA22405_hires.jpg
    

### Mars Weather





```python
#scrape the latest Mars weather tweet from the Mars Weather twitter account
twit_url = 'https://twitter.com/marswxreport?lang=en'
result = requests.get(twit_url)
result.ok
```




    True




```python
#make it text
html = result.text

#create BeautifulSoup object and parse
soup = BeautifulSoup(html, 'html.parser')
```


```python
print(soup.prettify())
```

    <!DOCTYPE html>
    <html data-scribe-reduced-action-queue="true" lang="en">
     <head>
      <meta charset="utf-8"/>
      <script nonce="S9uiLEWDbqlu5o4AZ4EAyA==">
       !function(){window.initErrorstack||(window.initErrorstack=[]),window.onerror=function(r,i,n,o,t){r.indexOf("Script error.")>-1||window.initErrorstack.push({errorMsg:r,url:i,lineNumber:n,column:o,errorObj:t})}}();
      </script>
      <script id="bouncer_terminate_iframe" nonce="S9uiLEWDbqlu5o4AZ4EAyA==">
       if (window.top != window) {
      window.top.postMessage({'bouncer': true, 'event': 'complete'}, '*');
    }
      </script>
      <script id="swift_action_queue" nonce="S9uiLEWDbqlu5o4AZ4EAyA==">
       !function(){function e(e){if(e||(e=window.event),!e)return!1;if(e.timestamp=(new Date).getTime(),!e.target&&e.srcElement&&(e.target=e.srcElement),document.documentElement.getAttribute("data-scribe-reduced-action-queue"))for(var t=e.target;t&&t!=document.body;){if("A"==t.tagName)return;t=t.parentNode}return i("all",o(e)),a(e)?(document.addEventListener||(e=o(e)),e.preventDefault=e.stopPropagation=e.stopImmediatePropagation=function(){},y?(v.push(e),i("captured",e)):i("ignored",e),!1):(i("direct",e),!0)}function t(e){n();for(var t,r=0;t=v[r];r++){var a=e(t.target),i=a.closest("a")[0];if("click"==t.type&&i){var o=e.data(i,"events"),u=o&&o.click,c=!i.hostname.match(g)||!i.href.match(/#$/);if(!u&&c){window.location=i.href;continue}}a.trigger(e.event.fix(t))}window.swiftActionQueue.wasFlushed=!0}function r(){for(var e in b)if("all"!=e)for(var t=b[e],r=0;r<t.length;r++)console.log("actionQueue",c(t[r]))}function n(){clearTimeout(w);for(var e,t=0;e=h[t];t++)document["on"+e]=null}function a(e){if(!e.target)return!1;var t=e.target,r=(t.tagName||"").toLowerCase();if(e.metaKey)return!1;if(e.shiftKey&&"a"==r)return!1;if(t.hostname&&!t.hostname.match(g))return!1;if(e.type.match(p)&&s(t))return!1;if("label"==r){var n=t.getAttribute("for");if(n){var a=document.getElementById(n);if(a&&f(a))return!1}else for(var i,o=0;i=t.childNodes[o];o++)if(f(i))return!1}return!0}function i(e,t){t.bucket=e,b[e].push(t)}function o(e){var t={};for(var r in e)t[r]=e[r];return t}function u(e){for(;e&&e!=document.body;){if("A"==e.tagName)return e;e=e.parentNode}}function c(e){var t=[];e.bucket&&t.push("["+e.bucket+"]"),t.push(e.type);var r,n,a=e.target,i=u(a),o="",c=e.timestamp&&e.timestamp-d;return"click"===e.type&&i?(r=i.className.trim().replace(/\s+/g,"."),n=i.id.trim(),o=/[^#]$/.test(i.href)?" ("+i.href+")":"",a='"'+i.innerText.replace(/\n+/g," ").trim()+'"'):(r=a.className.trim().replace(/\s+/g,"."),n=a.id.trim(),a=a.tagName.toLowerCase(),e.keyCode&&(a=String.fromCharCode(e.keyCode)+" : "+a)),t.push(a+o+(n&&"#"+n)+(!n&&r?"."+r:"")),c&&t.push(c),t.join(" ")}function f(e){var t=(e.tagName||"").toLowerCase();return"input"==t&&"checkbox"==e.getAttribute("type")}function s(e){var t=(e.tagName||"").toLowerCase();return"textarea"==t||"input"==t&&"text"==e.getAttribute("type")||"true"==e.getAttribute("contenteditable")}for(var m,d=(new Date).getTime(),l=1e4,g=/^([^\.]+\.)*twitter\.com$/,p=/^key/,h=["click","keydown","keypress","keyup"],v=[],w=null,y=!0,b={captured:[],ignored:[],direct:[],all:[]},k=0;m=h[k];k++)document["on"+m]=e;w=setTimeout(function(){y=!1},l),window.swiftActionQueue={buckets:b,flush:t,logActions:r,wasFlushed:!1}}();
      </script>
      <script id="composition_state" nonce="S9uiLEWDbqlu5o4AZ4EAyA==">
       !function(){function t(t){t.target.setAttribute("data-in-composition","true")}function n(t){t.target.removeAttribute("data-in-composition")}document.addEventListener&&(document.addEventListener("compositionstart",t,!1),document.addEventListener("compositionend",n,!1))}();
      </script>
      <link class="coreCSSBundles" href="https://abs.twimg.com/a/1527811926/css/t1/twitter_core.bundle.css" rel="stylesheet"/>
      <link class="moreCSSBundles" href="https://abs.twimg.com/a/1527811926/css/t1/twitter_more_1.bundle.css" rel="stylesheet"/>
      <link class="moreCSSBundles" href="https://abs.twimg.com/a/1527811926/css/t1/twitter_more_2.bundle.css" rel="stylesheet"/>
      <link href="https://pbs.twimg.com" rel="dns-prefetch"/>
      <link href="https://t.co" rel="dns-prefetch"/>
      <link as="script" href="https://abs.twimg.com/k/en/init.en.ae62202c2e7a8c3978db.js" rel="preload"/>
      <link as="script" href="https://abs.twimg.com/k/en/0.commons.en.5f1fff63dfb14e0c74d2.js" rel="preload"/>
      <link as="script" href="https://abs.twimg.com/k/en/3.pages_profile.en.0b0807e07fe459ee1c36.js" rel="preload"/>
      <title>
       Mars Weather (@MarsWxReport) | Twitter
      </title>
      <meta content="NOODP" name="robots"/>
      <meta content="The latest Tweets from Mars Weather (@MarsWxReport). Updates as avail from the REMS weather instrument aboard @MarsCuriosity.  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct. Gale Crater, Mars" name="description"/>
      <meta content="//abs.twimg.com/favicons/win8-tile-144.png" name="msapplication-TileImage">
       <meta content="#00aced" name="msapplication-TileColor">
        <link color="#1da1f2" href="https://abs.twimg.com/a/1527811926/icons/favicon.svg" rel="mask-icon" sizes="any"/>
        <link href="//abs.twimg.com/favicons/favicon.ico" rel="shortcut icon" type="image/x-icon"/>
        <link href="https://abs.twimg.com/icons/apple-touch-icon-192x192.png" rel="apple-touch-icon" sizes="192x192"/>
        <link href="/manifest.json" rel="manifest"/>
        <meta content="profile" id="swift-page-name" name="swift-page-name"/>
        <meta content="profile" id="swift-section-name" name="swift-page-section"/>
        <link href="https://twitter.com/marswxreport" rel="canonical"/>
        <link href="https://twitter.com/marswxreport" hreflang="x-default" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=fr" hreflang="fr" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=en" hreflang="en" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ar" hreflang="ar" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ja" hreflang="ja" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=es" hreflang="es" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=de" hreflang="de" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=it" hreflang="it" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=id" hreflang="id" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=pt" hreflang="pt" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ko" hreflang="ko" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=tr" hreflang="tr" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ru" hreflang="ru" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=nl" hreflang="nl" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=fil" hreflang="fil" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ms" hreflang="ms" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=zh-tw" hreflang="zh-tw" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=zh-cn" hreflang="zh-cn" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=hi" hreflang="hi" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=no" hreflang="no" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=sv" hreflang="sv" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=fi" hreflang="fi" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=da" hreflang="da" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=pl" hreflang="pl" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=hu" hreflang="hu" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=fa" hreflang="fa" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=he" hreflang="he" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ur" hreflang="ur" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=th" hreflang="th" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=uk" hreflang="uk" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ca" hreflang="ca" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ga" hreflang="ga" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=el" hreflang="el" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=eu" hreflang="eu" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=cs" hreflang="cs" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=gl" hreflang="gl" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ro" hreflang="ro" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=hr" hreflang="hr" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=en-gb" hreflang="en-gb" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=vi" hreflang="vi" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=bn" hreflang="bn" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=bg" hreflang="bg" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=sr" hreflang="sr" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=sk" hreflang="sk" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=gu" hreflang="gu" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=mr" hreflang="mr" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=ta" hreflang="ta" rel="alternate"/>
        <link href="https://twitter.com/marswxreport?lang=kn" hreflang="kn" rel="alternate"/>
        <link href="https://publish.twitter.com/oembed?url=https://twitter.com/MarsWxReport" rel="alternate" title="Mars Weather (@MarsWxReport) | Twitter" type="application/json+oembed"/>
        <link href="https://mobile.twitter.com/marswxreport?locale=en" media="handheld, only screen and (max-width: 640px)" rel="alternate"/>
        <link href="android-app://com.twitter.android/twitter/user?screen_name=MarsWxReport&amp;ref_src=twsrc%5Egoogle%7Ctwcamp%5Eandroidseo%7Ctwgr%5Eprofile" rel="alternate"/>
        <link href="/opensearch.xml" rel="search" title="Twitter" type="application/opensearchdescription+xml"/>
        <link id="async-css-placeholder"/>
        <meta content="twitter://user?screen_name=MarsWxReport" property="al:ios:url"/>
        <meta content="333903271" property="al:ios:app_store_id"/>
        <meta content="Twitter" property="al:ios:app_name"/>
        <meta content="twitter://user?screen_name=MarsWxReport" property="al:android:url"/>
        <meta content="com.twitter.android" property="al:android:package"/>
        <meta content="Twitter" property="al:android:app_name"/>
       </meta>
      </meta>
     </head>
     <body class="three-col logged-out user-style-MarsWxReport enhanced-mini-profile ProfilePage ProfilePage--withWarning" data-fouc-class-names="swift-loading no-nav-banners" dir="ltr">
      <script id="swift_loading_indicator" nonce="S9uiLEWDbqlu5o4AZ4EAyA==">
       document.body.className=document.body.className+" "+document.body.getAttribute("data-fouc-class-names");
      </script>
      <noscript>
       <form action="https://mobile.twitter.com/i/nojs_router?path=%2Fmarswxreport&amp;lang=en" class="NoScriptForm" method="POST">
        <input name="authenticity_token" type="hidden" value="127abef84d637ecd5578abab7ac0d383aebbc21a"/>
        <div class="NoScriptForm-content">
         <span class="NoScriptForm-logo Icon Icon--logo Icon--extraLarge">
         </span>
         <p>
          We've detected that JavaScript is disabled in your browser. Would you like to proceed to legacy Twitter?
         </p>
         <p class="NoScriptForm-buttonContainer">
          <button class="EdgeButton EdgeButton--primary" type="submit">
           Yes
          </button>
         </p>
        </div>
       </form>
      </noscript>
      <a class="u-hiddenVisually focusable" href="#timeline">
       Skip to content
      </a>
      <div class="route-profile" data-at-shortcutkeys='{"Enter":"Open Tweet details","o":"Expand photo","/":"Search","?":"This menu","j":"Next Tweet","k":"Previous Tweet","Space":"Page down",".":"Load new Tweets","gu":"Go to user\u2026"}' id="doc">
       <div class="topbar js-topbar">
        <div class="global-nav global-nav--newLoggedOut" data-section-term="top_nav">
         <div class="global-nav-inner">
          <div class="container">
           <ul class="nav js-global-actions" id="global-actions" role="navigation">
            <li class="home" data-global-action="home" id="global-nav-home">
             <a class="js-nav js-tooltip js-dynamic-tooltip" data-component-context="home_nav" data-nav="home" data-placement="bottom" href="/">
              <span class="Icon Icon--bird Icon--large">
              </span>
              <span aria-hidden="true" class="text">
               Home
              </span>
              <span class="u-hiddenVisually a11y-inactive-page-text">
               Home
              </span>
              <span class="u-hiddenVisually a11y-active-page-text">
               Home, current page.
              </span>
             </a>
            </li>
            <li class="moments" data-global-action="moments" id="global-nav-moments">
             <a class="js-nav js-tooltip js-dynamic-tooltip" data-component-context="moments_nav" data-nav="moments" data-placement="bottom" href="/i/moments">
              <span class="Icon Icon--lightning Icon--large">
              </span>
              <span class="Icon Icon--lightningFilled Icon--large">
              </span>
              <span aria-hidden="true" class="text">
               Moments
              </span>
              <span class="u-hiddenVisually a11y-inactive-page-text">
               Moments
              </span>
              <span class="u-hiddenVisually a11y-active-page-text">
               Moments, current page.
              </span>
             </a>
            </li>
           </ul>
           <div class="pull-right nav-extras">
            <div role="search">
             <form action="/search" class="t1-form form-search js-search-form" id="global-nav-search">
              <label class="visuallyhidden" for="search-query">
               Search query
              </label>
              <input autocomplete="off" class="search-input" id="search-query" name="q" placeholder="Search Twitter" spellcheck="false" type="text"/>
              <span class="search-icon js-search-action">
               <button class="Icon Icon--medium Icon--search nav-search" type="submit">
                <span class="visuallyhidden">
                 Search Twitter
                </span>
               </button>
              </span>
              <div class="dropdown-menu typeahead" role="listbox">
               <div aria-hidden="true" class="dropdown-caret">
                <div class="caret-outer">
                </div>
                <div class="caret-inner">
                </div>
               </div>
               <div class="dropdown-inner js-typeahead-results" role="presentation">
                <div class="typeahead-saved-searches" role="presentation">
                 <h3 class="typeahead-category-title saved-searches-title" id="saved-searches-heading">
                  Saved searches
                 </h3>
                 <ul class="typeahead-items saved-searches-list" role="presentation">
                  <li class="typeahead-item typeahead-saved-search-item" role="presentation">
                   <span aria-hidden="true" class="Icon Icon--close">
                    <span class="visuallyhidden">
                     Remove
                    </span>
                   </span>
                   <a aria-describedby="saved-searches-heading" class="js-nav" data-ds="saved_search" data-query-source="" data-search-query="" href="" role="option" tabindex="-1">
                   </a>
                  </li>
                 </ul>
                </div>
                <ul class="typeahead-items typeahead-topics" role="presentation">
                 <li class="typeahead-item typeahead-topic-item" role="presentation">
                  <a class="js-nav" data-ds="topics" data-query-source="typeahead_click" data-search-query="" href="" role="option" tabindex="-1">
                  </a>
                 </li>
                </ul>
                <ul class="typeahead-items typeahead-accounts social-context js-typeahead-accounts" role="presentation">
                 <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                  <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                   <div class="js-selectable typeahead-in-conversation hidden">
                    <span class="Icon Icon--follower Icon--small">
                    </span>
                    <span class="typeahead-in-conversation-text">
                     In this conversation
                    </span>
                   </div>
                   <img alt="" class="avatar size32"/>
                   <span class="typeahead-user-item-info account-group">
                    <span class="fullname">
                    </span>
                    <span class="UserBadges">
                     <span class="Icon Icon--verified js-verified hidden">
                      <span class="u-hiddenVisually">
                       Verified account
                      </span>
                     </span>
                     <span class="Icon Icon--protected js-protected hidden">
                      <span class="u-hiddenVisually">
                       Protected Tweets
                      </span>
                     </span>
                    </span>
                    <span class="UserNameBreak">
                    </span>
                    <span class="username u-dir" dir="ltr">
                     @
                     <b>
                     </b>
                    </span>
                   </span>
                   <span class="typeahead-social-context">
                   </span>
                  </a>
                 </li>
                 <li class="js-selectable typeahead-accounts-shortcut js-shortcut" role="presentation">
                  <a class="js-nav" data-ds="account_search" data-query-source="typeahead_click" data-search-query="" data-shortcut="true" href="" role="option">
                  </a>
                 </li>
                </ul>
                <ul class="typeahead-items typeahead-trend-locations-list" role="presentation">
                 <li class="typeahead-item typeahead-trend-locations-item" role="presentation">
                  <a class="js-nav" data-ds="trend_location" data-search-query="" href="" role="option" tabindex="-1">
                  </a>
                 </li>
                </ul>
                <div class="typeahead-user-select" role="presentation">
                 <div class="typeahead-empty-suggestions" role="presentation">
                  Suggested users
                 </div>
                 <ul class="typeahead-items typeahead-selected js-typeahead-selected" role="presentation">
                  <li class="typeahead-item typeahead-selected-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                   <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                    <img alt="" class="avatar size32"/>
                    <span class="typeahead-user-item-info account-group">
                     <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                     </span>
                     <span class="select-status select-disabled Icon Icon--unfollow">
                     </span>
                     <span class="fullname">
                     </span>
                     <span class="UserBadges">
                      <span class="Icon Icon--verified js-verified hidden">
                       <span class="u-hiddenVisually">
                        Verified account
                       </span>
                      </span>
                      <span class="Icon Icon--protected js-protected hidden">
                       <span class="u-hiddenVisually">
                        Protected Tweets
                       </span>
                      </span>
                     </span>
                     <span class="UserNameBreak">
                     </span>
                     <span class="username u-dir" dir="ltr">
                      @
                      <b>
                      </b>
                     </span>
                    </span>
                   </a>
                  </li>
                  <li class="typeahead-selected-end" role="presentation">
                  </li>
                 </ul>
                 <ul class="typeahead-items typeahead-accounts js-typeahead-accounts" role="presentation">
                  <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                   <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                    <img alt="" class="avatar size32"/>
                    <span class="typeahead-user-item-info account-group">
                     <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                     </span>
                     <span class="select-status select-disabled Icon Icon--unfollow">
                     </span>
                     <span class="fullname">
                     </span>
                     <span class="UserBadges">
                      <span class="Icon Icon--verified js-verified hidden">
                       <span class="u-hiddenVisually">
                        Verified account
                       </span>
                      </span>
                      <span class="Icon Icon--protected js-protected hidden">
                       <span class="u-hiddenVisually">
                        Protected Tweets
                       </span>
                      </span>
                     </span>
                     <span class="UserNameBreak">
                     </span>
                     <span class="username u-dir" dir="ltr">
                      @
                      <b>
                      </b>
                     </span>
                    </span>
                   </a>
                  </li>
                  <li class="typeahead-accounts-end" role="presentation">
                  </li>
                 </ul>
                </div>
                <div class="typeahead-dm-conversations" role="presentation">
                 <ul class="typeahead-items typeahead-dm-conversation-items" role="presentation">
                  <li class="typeahead-item typeahead-dm-conversation-item" role="presentation">
                   <a role="option" tabindex="-1">
                   </a>
                  </li>
                 </ul>
                </div>
               </div>
              </div>
             </form>
            </div>
            <ul class="nav secondary-nav language-dropdown">
             <li class="dropdown js-language-dropdown">
              <a class="dropdown-toggle js-dropdown-toggle" href="#supported_languages">
               <small>
                Language:
               </small>
               <span class="js-current-language">
                English
               </span>
               <b class="caret">
               </b>
              </a>
              <div class="dropdown-menu dropdown-menu--rightAlign is-forceRight">
               <div class="dropdown-caret right">
                <span class="caret-outer">
                </span>
                <span class="caret-inner">
                </span>
               </div>
               <ul id="supported_languages">
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="id" href="?lang=id" rel="noopener" title="Indonesian">
                  Bahasa Indonesia
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="msa" href="?lang=msa" rel="noopener" title="Malay">
                  Bahasa Melayu
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ca" href="?lang=ca" rel="noopener" title="Catalan">
                  Català
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="cs" href="?lang=cs" rel="noopener" title="Czech">
                  Čeština
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="da" href="?lang=da" rel="noopener" title="Danish">
                  Dansk
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="de" href="?lang=de" rel="noopener" title="German">
                  Deutsch
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="en-gb" href="?lang=en-gb" rel="noopener" title="British English">
                  English UK
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="es" href="?lang=es" rel="noopener" title="Spanish">
                  Español
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fil" href="?lang=fil" rel="noopener" title="Filipino">
                  Filipino
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fr" href="?lang=fr" rel="noopener" title="French">
                  Français
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="hr" href="?lang=hr" rel="noopener" title="Croatian">
                  Hrvatski
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="it" href="?lang=it" rel="noopener" title="Italian">
                  Italiano
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="hu" href="?lang=hu" rel="noopener" title="Hungarian">
                  Magyar
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="nl" href="?lang=nl" rel="noopener" title="Dutch">
                  Nederlands
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="no" href="?lang=no" rel="noopener" title="Norwegian">
                  Norsk
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="pl" href="?lang=pl" rel="noopener" title="Polish">
                  Polski
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="pt" href="?lang=pt" rel="noopener" title="Portuguese">
                  Português
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ro" href="?lang=ro" rel="noopener" title="Romanian">
                  Română
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="sk" href="?lang=sk" rel="noopener" title="Slovak">
                  Slovenčina
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fi" href="?lang=fi" rel="noopener" title="Finnish">
                  Suomi
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="sv" href="?lang=sv" rel="noopener" title="Swedish">
                  Svenska
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="vi" href="?lang=vi" rel="noopener" title="Vietnamese">
                  Tiếng Việt
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="tr" href="?lang=tr" rel="noopener" title="Turkish">
                  Türkçe
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="el" href="?lang=el" rel="noopener" title="Greek">
                  Ελληνικά
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="bg" href="?lang=bg" rel="noopener" title="Bulgarian">
                  Български език
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ru" href="?lang=ru" rel="noopener" title="Russian">
                  Русский
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="sr" href="?lang=sr" rel="noopener" title="Serbian">
                  Српски
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="uk" href="?lang=uk" rel="noopener" title="Ukrainian">
                  Українська мова
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="he" href="?lang=he" rel="noopener" title="Hebrew">
                  עִבְרִית
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ar" href="?lang=ar" rel="noopener" title="Arabic">
                  العربية
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fa" href="?lang=fa" rel="noopener" title="Persian">
                  فارسی
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="mr" href="?lang=mr" rel="noopener" title="Marathi">
                  मराठी
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="hi" href="?lang=hi" rel="noopener" title="Hindi">
                  हिन्दी
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="bn" href="?lang=bn" rel="noopener" title="Bangla">
                  বাংলা
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="gu" href="?lang=gu" rel="noopener" title="Gujarati">
                  ગુજરાતી
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ta" href="?lang=ta" rel="noopener" title="Tamil">
                  தமிழ்
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="kn" href="?lang=kn" rel="noopener" title="Kannada">
                  ಕನ್ನಡ
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="th" href="?lang=th" rel="noopener" title="Thai">
                  ภาษาไทย
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ko" href="?lang=ko" rel="noopener" title="Korean">
                  한국어
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ja" href="?lang=ja" rel="noopener" title="Japanese">
                  日本語
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="zh-cn" href="?lang=zh-cn" rel="noopener" title="Simplified Chinese">
                  简体中文
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="zh-tw" href="?lang=zh-tw" rel="noopener" title="Traditional Chinese">
                  繁體中文
                 </a>
                </li>
               </ul>
              </div>
              <div class="js-front-language">
               <form action="/sessions/change_locale" class="t1-form language" method="POST">
                <input name="lang" type="hidden"/>
                <input name="redirect" type="hidden"/>
                <input name="authenticity_token" type="hidden" value="127abef84d637ecd5578abab7ac0d383aebbc21a"/>
               </form>
              </div>
             </li>
            </ul>
            <ul class="nav secondary-nav session-dropdown" id="session">
             <li class="dropdown js-session">
              <a class="dropdown-toggle js-dropdown-toggle dropdown-signin" data-nav="login" href="/login" id="signin-link" role="button">
               <small>
                Have an account?
               </small>
               <span class="emphasize">
                Log in
               </span>
               <span class="caret">
               </span>
              </a>
              <div class="dropdown-menu dropdown-form dropdown-menu--rightAlign is-forceRight" id="signin-dropdown">
               <div class="dropdown-caret right">
                <span class="caret-outer">
                </span>
                <span class="caret-inner">
                </span>
               </div>
               <div class="signin-dialog-body">
                <div>
                 Have an account?
                </div>
                <form action="https://twitter.com/sessions" class="LoginForm js-front-signin" data-component="login_callout" data-element="form" method="post">
                 <div class="LoginForm-input LoginForm-username">
                  <input autocomplete="username" class="text-input email-input js-signin-email" name="session[username_or_email]" placeholder="Phone, email, or username" type="text">
                  </input>
                 </div>
                 <div class="LoginForm-input LoginForm-password">
                  <input autocomplete="current-password" class="text-input" name="session[password]" placeholder="Password" type="password"/>
                 </div>
                 <div class="LoginForm-rememberForgot">
                  <label>
                   <input checked="checked" name="remember_me" type="checkbox" value="1"/>
                   <span>
                    Remember me
                   </span>
                  </label>
                  <span class="separator">
                   ·
                  </span>
                  <a class="forgot" href="/account/begin_password_reset" rel="noopener">
                   Forgot password?
                  </a>
                 </div>
                 <input class="EdgeButton EdgeButton--primary EdgeButton--medium submit js-submit" type="submit" value="Log in"/>
                 <input name="return_to_ssl" type="hidden" value="true"/>
                 <input name="scribe_log" type="hidden"/>
                 <input name="redirect_after_login" type="hidden" value="/marswxreport?lang=en"/>
                 <input name="authenticity_token" type="hidden" value="127abef84d637ecd5578abab7ac0d383aebbc21a"/>
                 <input autocomplete="off" name="ui_metrics" type="hidden"/>
                 <script async="" src="/i/js_inst?c_name=ui_metrics">
                 </script>
                </form>
                <hr/>
                <div class="signup SignupForm">
                 <div class="SignupForm-header">
                  New to Twitter?
                 </div>
                 <a class="EdgeButton EdgeButton--secondary EdgeButton--medium u-block js-signup" data-component="signup_callout" data-element="dropdown" href="https://twitter.com/signup" role="button">
                  Sign up
                 </a>
                </div>
               </div>
              </div>
             </li>
            </ul>
           </div>
          </div>
         </div>
        </div>
       </div>
       <div id="page-outer">
        <div class="AppContent" id="page-container">
         <style id="user-style-MarsWxReport">
          a,
      a:hover,
      a:focus,
      a:active {
        color: #0084B4;
      }
    
      .u-textUserColor,
      .u-textUserColorHover:hover,
      .u-textUserColorHover:hover .ProfileTweet-actionCount,
      .u-textUserColorHover:focus {
        color: #0084B4 !important;
      }
    
      .u-borderUserColor,
      .u-borderUserColorHover:hover,
      .u-borderUserColorHover:focus {
        border-color: #0084B4 !important;
      }
    
      .u-bgUserColor,
      .u-bgUserColorHover:hover,
      .u-bgUserColorHover:focus {
        background-color: #0084B4 !important;
      }
    
      .u-dropdownUserColor > li:hover,
      .u-dropdownUserColor > li:focus,
      .u-dropdownUserColor > li > button:hover,
      .u-dropdownUserColor > li > button:focus,
      .u-dropdownUserColor > li > a:focus,
      .u-dropdownUserColor > li > a:hover {
        color: #fff !important;
        background-color: #0084B4 !important;
      }
    
      .u-boxShadowInsetUserColorHover:hover,
      .u-boxShadowInsetUserColorHover:focus {
        box-shadow: inset 0 0 0 5px #0084B4 !important;
      }
    
      .u-dropdownOpenUserColor.dropdown.open .dropdown-toggle {
        color: #0084B4;
      }
    
    
      .u-textUserColorLight {
        color: #99CDE1 !important;
      }
    
      .u-borderUserColorLight,
      .u-borderUserColorLightFocus:focus,
      .u-borderUserColorLightHover:hover,
      .u-borderUserColorLightHover:focus {
        border-color: #99CDE1 !important;
      }
    
      .u-bgUserColorLight {
        background-color: #99CDE1 !important;
      }
    
    
      .u-boxShadowUserColorLighterFocus:focus {
        box-shadow: 0 0 8px rgba(0, 0, 0, 0.05), inset 0 1px 2px rgba(0,132,180,0.25) !important;
      }
    
    
      .u-textUserColorLightest {
        color: #E5F2F7 !important;
      }
    
      .u-borderUserColorLightest {
        border-color: #E5F2F7 !important;
      }
    
      .u-bgUserColorLightest {
        background-color: #E5F2F7 !important;
      }
    
    
      .u-textUserColorLighter {
        color: #BFE0EC !important;
      }
    
      .u-borderUserColorLighter {
        border-color: #BFE0EC !important;
      }
    
      .u-bgUserColorLighter {
        background-color: #BFE0EC !important;
      }
    
    
      .u-bgUserColorDarkHover:hover {
        background-color: #05719A !important;
      }
    
      .u-borderUserColorDark {
        border-color: #05719A !important;
      }
    
    
      .u-bgUserColorDarkerActive:active {
        background-color: #0A5F81 !important;
      }
    
    
    
    
    
    
    
    
    
    
    
    
    
    a,
    .btn-link,
    .btn-link:focus,
    .icon-btn,
    
    
    
    .pretty-link b,
    .pretty-link:hover s,
    .pretty-link:hover b,
    .pretty-link:focus s,
    .pretty-link:focus b,
    
    .metadata a:hover,
    .metadata a:focus,
    
    a.account-group:hover .fullname,
    a.account-group:focus .fullname,
    .account-summary:focus .fullname,
    
    .message .message-text a,
    .message .message-text button,
    .stats a strong,
    .plain-btn:hover,
    .plain-btn:focus,
    .dropdown.open .user-dropdown.plain-btn,
    .open > .plain-btn,
    #global-actions .new:before,
    .module .list-link:hover,
    .module .list-link:focus,
    
    .stats a:hover,
    .stats a:hover strong,
    .stats a:focus,
    .stats a:focus strong,
    
    .find-friends-sources li:hover .source,
    
    
    
    
    
    .stream-item a:hover .fullname,
    .stream-item a:focus .fullname,
    
    .stream-item .view-all-supplements:hover,
    .stream-item .view-all-supplements:focus,
    
    .tweet .time a:hover,
    .tweet .time a:focus,
    .tweet .details.with-icn b,
    .tweet .details.with-icn .Icon,
    
    .stream-item:hover .original-tweet .details b,
    .stream-item .original-tweet.focus .details b,
    .stream-item.open .original-tweet .details b,
    
    .client-and-actions a:hover,
    .client-and-actions a:focus,
    
    .dismiss-btn:hover b,
    
    .tweet .context .pretty-link:hover s,
    .tweet .context .pretty-link:hover b,
    .tweet .context .pretty-link:focus s,
    .tweet .context .pretty-link:focus b,
    
    .list .username a:hover,
    .list .username a:focus,
    .list-membership-container .create-a-list,
    .list-membership-container .create-a-list:hover,
    .new-tweets-bar,
    
    
    
    .card .list-details a:hover,
    .card .list-details a:focus,
    .card .card-body:hover .attribution,
    .card .card-body .attribution:focus {
      color: #0084B4;
    }
    
    
    
    
      
      .FoundMediaSearch--keyboard .FoundMediaSearch-focusable.is-focused {
        border-color: #0084B4;
      }
    
      
      .photo-selector:hover .btn,
      .icon-btn:hover,
      .icon-btn:active,
      .icon-btn.active,
      .icon-btn.enabled {
        border-color: #0084B4;
        border-color: rgba(0,132,180,0.4);
        color: #0084B4;
      }
    
      
      .photo-selector:hover .btn,
      .icon-btn:hover {
        background-image: linear-gradient(rgba(255,255,255,0), rgba(0,132,180,0.1));
      }
    
      .icon-btn.disabled,
      .icon-btn.disabled:hover,
      .icon-btn[disabled],
      .icon-btn[aria-disabled=true] {
        color: #0084B4;
      }
    
      
      
    
      .EdgeButton--primary,
      .EdgeButton--primary:focus {
        background-color: #329CC3;
        border-color: transparent;
      }
    
      .EdgeButton--primary:hover,
      .EdgeButton--primary:active {
        background-color: #0084B4;
        border-color: #0084B4;
      }
    
      .EdgeButton--primary:focus {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px #99CDE1;
      }
    
      .EdgeButton--primary:active {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px #329CC3;
      }
    
      
      
    
      .EdgeButton--secondary,
      .EdgeButton--secondary:hover,
      .EdgeButton--secondary:focus,
      .EdgeButton--secondary:active {
        border-color: #0084B4;
        color: #0084B4;
      }
    
      .EdgeButton--secondary:hover,
      .EdgeButton--secondary:active {
        background-color: #E5F2F7;
      }
    
      .EdgeButton--secondary:focus {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px rgba(0,132,180,0.4);
      }
    
      .EdgeButton--secondary:active {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px #0084B4;
      }
    
      
      
    
      .EdgeButton--invertedPrimary {
        color: #0084B4 !important;
      }
    
      .EdgeButton--invertedPrimary:focus {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #99CDE1;
      }
    
      .EdgeButton--invertedPrimary:active {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #FFFFFF;
      }
    
      
      
    
      .EdgeButton--invertedSecondary {
        background-color: #0084B4;
      }
    
      .EdgeButton--invertedSecondary:hover {
        background-color: #329CC3;
      }
    
      .EdgeButton--invertedSecondary:focus {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #99CDE1;
      }
    
      .EdgeButton--invertedSecondary:active {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #FFFFFF;
      }
    
      
    
      .btn:focus,
      .btn.focus,
      .Button:focus,
      .EmojiPicker-item.is-focused,
      .EmojiPicker .EmojiCategoryIcon:focus,
      .EmojiPicker-skinTone:focus + .EmojiPicker-skinToneSwatch,
      a:focus > img:first-child:last-child,
      button:focus {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 2px 4px rgba(0,132,180,0.4);
      }
    
      .selected-stream-item:focus {
        box-shadow: 0 0 0 3px rgba(0,132,180,0.4);
      }
    
      
      .js-navigable-stream.stream-table-view .selected-stream-item[tabindex="-1"]:focus {
        outline: 3px solid rgba(0,132,180,0.4) !important;
      }
    
      
      .js-navigable-stream.stream-table-view .selected-stream-item:focus {
        box-shadow: none;
      }
    
      
    
      .global-dm-nav.new.with-count .dm-new .count-inner {
        background: #0084B4;
      }
    
      .global-nav .people .count .count-inner {
        background: #0084B4;
      }
    
      .dropdown-menu li > a:hover,
      .dropdown-menu li > a:focus,
      .dropdown-menu .dropdown-link:hover,
      .dropdown-menu .dropdown-link:focus,
      .dropdown-menu .dropdown-link.is-focused,
      .dropdown-menu li:hover .dropdown-link,
      .dropdown-menu li:focus .dropdown-link,
      .dropdown-menu .selected a,
      .dropdown-menu .dropdown-link.selected {
        background-color: #0084B4 !important;
      }
    
      /* for items in typeahead dropdown menu on logged in pages */
      .dropdown-menu .typeahead-items li > a:focus,
      .dropdown-menu .typeahead-items li > a:hover,
      .dropdown-menu .typeahead-items .selected,
      .dropdown-menu .typeahead-items .selected a {
        background-color: #E5F2F7 !important;
        color: #0084B4 !important;
      }
    
      .typeahead a:hover,
      .typeahead a:hover strong,
      .typeahead a:hover .fullname,
      .typeahead .selected a,
      .typeahead .selected strong,
      .typeahead .selected .fullname,
      .typeahead .selected .Icon--close {
        color: #0084B4 !important;
      }
    
    
    .home-tweet-box,
    .LiveVideo-tweetBox,
    .RetweetDialog-commentBox {
      background-color: #E5F2F7;
    }
    
    .top-timeline-tweetbox .timeline-tweet-box .tweet-form.condensed .tweet-box {
      color: #0084B4;
    }
    
    .RichEditor,
    .TweetBoxAttachments {
      border-color: #BFE0EC;
    }
    
    input:focus,
    textarea:focus,
    div[contenteditable="true"]:focus,
    div[contenteditable="true"].fake-focus,
    div[contenteditable="plaintext-only"]:focus,
    div[contenteditable="plaintext-only"].fake-focus {
      border-color: #99CDE1;
      box-shadow: inset 0 0 0 1px rgba(0,132,180,0.7);
    }
    
    .tweet-box textarea:focus,
    .tweet-box input[type=text],
    .currently-dragging .tweet-form.is-droppable .tweet-drag-help,
    .tweet-box[contenteditable="true"]:focus,
    .RichEditor.is-fakeFocus,
    .RichEditor.is-fakeFocus ~ .TweetBoxAttachments {
      border-color: #99CDE1;
      box-shadow: 0 0 0 1px #99CDE1;
    }
    
    .MomentCapsuleItem.selected-stream-item:focus {
      box-shadow: 0 0 0 3px rgba(0,132,180,0.4);
    }
    
    
    
    
    s,
    .pretty-link:hover s,
    .pretty-link:focus s,
    .stream-item-activity-notification .latest-tweet .tweet-row a:hover s,
    .stream-item-activity-notification .latest-tweet .tweet-row a:focus s {
        color: #0084B4;
    }
    
    
    
    .vellip,
    .vellip:before,
    .vellip:after,
    .conversation-module > li:after,
    .conversation-module > li:before,
    .ThreadedConversation--loneTweet:after,
    .ThreadedConversation-tweet:not(.is-hiddenAncestor) ~ .ThreadedConversation-tweet:before,
    .ThreadedConversation-tweet:after,
    .ThreadedConversation-moreReplies:before,
    .ThreadedConversation-viewOther:before,
    .ThreadedConversation-unavailableTweet:before,
    .ThreadedConversation-unavailableTweet:after,
    .ThreadedConversation--permalinkTweetWithAncestors:before,
    .mini-avatar-with-thread:before,
    .permalink.self-thread-permalink-with-descendant .permalink-tweet-container:after,
    .permalink.self-thread-permalink-with-descendant .inline-reply-tweetbox-container:after {
        border-color: #99CDE1;
    }
    
    
    
    
    .tweet .sm-reply,
    .tweet .sm-rt,
    .tweet .sm-fav,
    .tweet .sm-image,
    .tweet .sm-video,
    .tweet .sm-audio,
    .tweet .sm-geo,
    .tweet .sm-in,
    .tweet .sm-trash,
    .tweet .sm-more,
    .tweet .sm-page,
    .tweet .sm-embed,
    .tweet .sm-summary,
    .tweet .sm-chat,
    
    .timelines-navigation .active .profile-nav-icon,
    .timelines-navigation .profile-nav-icon:hover,
    .timelines-navigation .profile-nav-link:focus .profile-nav-icon,
    
    .sm-top-tweet {
        background-color: #0084B4;
    }
    
    .enhanced-mini-profile .mini-profile .profile-summary {
      background-image: url(https://pbs.twimg.com/profile_banners/786939553/1403835009/mobile);
    }
    
      #global-tweet-dialog .modal-header,
      #Tweetstorm-dialog .modal-header {
        border-bottom: solid 1px rgba(0,132,180,0.25);
      }
    
      #global-tweet-dialog .modal-tweet-form-container,
      #Tweetstorm-dialog .modal-body {
        background-color: #0084B4;
        background: rgba(0,132,180,0.1);
      }
    
      .TweetstormDialog-reply-context .tweet-box-avatar:after,
      .TweetstormDialog-reply-context .tweet-box-avatar:before,
      .TweetstormDialog-tweet-box .tweet-box-avatar:after,
      .TweetstormDialog-tweet-box .tweet-box-avatar:before {
        border-color: #99CDE1;
      }
    
      .global-nav .search-input:focus,
      .global-nav .search-input.focus {
        border: 2px solid #0084B4;
      }
    }
    
      .inline-reply-tweetbox {
        background-color: #E5F2F7;
      }
         </style>
         <div class="ProfileCanopy ProfileCanopy--withNav ProfileCanopy--large js-variableHeightTopBar">
          <div class="ProfileCanopy-inner">
           <div class="ProfileCanopy-header u-bgUserColor">
            <div class="ProfileCanopy-headerBg">
             <img alt="" src="https://pbs.twimg.com/profile_banners/786939553/1403835009/1500x500"/>
            </div>
            <div class="AppContainer">
             <div class="ProfileCanopy-avatar">
              <div class="ProfileAvatar">
               <a class="ProfileAvatar-container u-block js-tooltip profile-picture" data-resolved-url-large="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg" data-url="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg" href="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg" rel="noopener" target="_blank" title="Mars Weather">
                <img alt="Mars Weather" class="ProfileAvatar-image " src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg"/>
               </a>
              </div>
             </div>
             <div class="ProfileCanopy-headerPromptAnchor">
             </div>
            </div>
           </div>
           <div class="ProfileCanopy-navBar u-boxShadow">
            <div class="AppContainer">
             <div class="Grid Grid--withGutter">
              <div class="Grid-cell u-size1of3 u-lg-size1of4">
               <div class="ProfileCanopy-card" role="presentation">
                <div class="ProfileCardMini">
                 <a class="ProfileCardMini-avatar profile-picture js-tooltip" data-resolved-url-large="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere.jpg" data-url="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere.jpg" href="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere.jpg" rel="noopener" target="_blank" title="Mars Weather">
                  <img alt="Mars Weather" class="ProfileCardMini-avatarImage" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                 </a>
                 <div class="ProfileCardMini-details">
                  <div class="ProfileNameTruncated account-group">
                   <div class="u-textTruncate u-inlineBlock">
                    <a class="fullname ProfileNameTruncated-link u-textInheritColor js-nav" data-aria-label-part="" href="/MarsWxReport">
                     Mars Weather
                    </a>
                   </div>
                   <span class="UserBadges">
                   </span>
                  </div>
                  <div class="ProfileCardMini-screenname">
                   <a class="ProfileCardMini-screennameLink u-linkComplex js-nav u-dir" dir="ltr" href="/MarsWxReport">
                    <span class="username u-dir" dir="ltr">
                     @
                     <b class="u-linkComplex-target">
                      MarsWxReport
                     </b>
                    </span>
                   </a>
                  </div>
                 </div>
                </div>
               </div>
              </div>
              <div class="Grid-cell u-size2of3 u-lg-size3of4">
               <div class="ProfileCanopy-nav">
                <div class="ProfileNav" data-user-id="786939553" role="navigation">
                 <ul class="ProfileNav-list">
                  <li class="ProfileNav-item ProfileNav-item--tweets is-active">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-nav" data-nav="tweets" tabindex="0" title="1,455 Tweets">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Tweets
                    </span>
                    <span class="u-hiddenVisually">
                     Tweets, current page.
                    </span>
                    <span class="ProfileNav-value" data-count="1455" data-is-compact="false">
                     1,455
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--following">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="following" href="/MarsWxReport/following" title="53 Following">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Following
                    </span>
                    <span class="u-hiddenVisually">
                     Following
                    </span>
                    <span class="ProfileNav-value" data-count="53" data-is-compact="false">
                     53
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--followers">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="followers" href="/MarsWxReport/followers" title="39,885 Followers">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Followers
                    </span>
                    <span class="u-hiddenVisually">
                     Followers
                    </span>
                    <span class="ProfileNav-value" data-count="39885" data-is-compact="true">
                     39.9K
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--favorites" data-more-item=".ProfileNav-dropdownItem--favorites">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="favorites" href="/MarsWxReport/likes" title="196 Likes">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Likes
                    </span>
                    <span class="u-hiddenVisually">
                     Likes
                    </span>
                    <span class="ProfileNav-value" data-count="196" data-is-compact="false">
                     196
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--lists" data-more-item=".ProfileNav-dropdownItem--lists">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="all_lists" href="/MarsWxReport/lists" title="9 Lists">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Lists
                    </span>
                    <span class="u-hiddenVisually">
                     Lists
                    </span>
                    <span class="ProfileNav-value" data-is-compact="false">
                     9
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--more dropdown is-hidden">
                   <a class="ProfileNav-stat ProfileNav-stat--link ProfileNav-stat--moreLink js-openSignupDialog js-nonNavigable" href="#more" role="button">
                    <span class="ProfileNav-label">
                    </span>
                    <span class="ProfileNav-value">
                     More
                     <span class="ProfileNav-dropdownCaret Icon Icon--medium Icon--caretDown">
                     </span>
                    </span>
                   </a>
                   <div class="dropdown-menu">
                    <div class="dropdown-caret">
                     <span class="caret-outer">
                     </span>
                     <span class="caret-inner">
                     </span>
                    </div>
                    <ul>
                     <li>
                      <a class="ProfileNav-dropdownItem ProfileNav-dropdownItem--favorites is-hidden u-bgUserColorHover u-bgUserColorFocus u-linkClean js-nav" href="/MarsWxReport/likes">
                       Likes
                      </a>
                     </li>
                     <li>
                      <a class="ProfileNav-dropdownItem ProfileNav-dropdownItem--lists is-hidden u-bgUserColorHover u-bgUserColorFocus u-linkClean js-nav" href="/MarsWxReport/lists">
                       Lists
                      </a>
                     </li>
                    </ul>
                   </div>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--userActions u-floatRight u-textRight with-rightCaret ">
                   <div class="UserActions u-textLeft">
                    <div class="user-actions btn-group not-following " data-name="Mars Weather" data-protected="false" data-screen-name="MarsWxReport" data-user-id="786939553">
                     <span class="UserActions-moreActions u-inlineBlock">
                      <button class="js-tooltip unmute-button btn small plain-btn" data-placement="top" title="Unmute @MarsWxReport" type="button">
                       <span class="Icon Icon--muted Icon--medium">
                        <span class="visuallyhidden">
                         Unmute
                         <span class="username u-dir u-textTruncate" dir="ltr">
                          @
                          <b>
                           MarsWxReport
                          </b>
                         </span>
                        </span>
                       </span>
                      </button>
                      <button class="first-load js-tooltip mute-button btn small plain-btn" data-placement="top" title="Mute @MarsWxReport" type="button">
                       <span class="Icon Icon--unmuted Icon--medium">
                        <span class="visuallyhidden">
                         Mute
                         <span class="username u-dir u-textTruncate" dir="ltr">
                          @
                          <b>
                           MarsWxReport
                          </b>
                         </span>
                        </span>
                       </span>
                      </button>
                     </span>
                     <span class="user-actions-follow-button js-follow-btn follow-button">
                      <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                       <span aria-hidden="true">
                        Follow
                       </span>
                       <span class="u-hiddenVisually">
                        Follow
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                       <span aria-hidden="true">
                        Following
                       </span>
                       <span class="u-hiddenVisually">
                        Following
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                       <span aria-hidden="true">
                        Unfollow
                       </span>
                       <span class="u-hiddenVisually">
                        Unfollow
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                       <span aria-hidden="true">
                        Blocked
                       </span>
                       <span class="u-hiddenVisually">
                        Blocked
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                       <span aria-hidden="true">
                        Unblock
                       </span>
                       <span class="u-hiddenVisually">
                        Unblock
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                       <span aria-hidden="true">
                        Pending
                       </span>
                       <span class="u-hiddenVisually">
                        Pending follow request from
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                       <span aria-hidden="true">
                        Cancel
                       </span>
                       <span class="u-hiddenVisually">
                        Cancel your follow request to
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                     </span>
                    </div>
                   </div>
                  </li>
                 </ul>
                </div>
               </div>
              </div>
             </div>
            </div>
           </div>
          </div>
         </div>
         <div class="AppContainer">
          <div aria-labelledby="content-main-heading" class="AppContent-main content-main u-cf" role="main">
           <div class="Grid Grid--withGutter">
            <div class="Grid-cell u-size1of3 u-lg-size1of4">
             <div class="Grid Grid--withGutter">
              <div class="Grid-cell">
               <div class="ProfileSidebar ProfileSidebar--withLeftAlignment">
                <div class="ProfileHeaderCard">
                 <h1 class="ProfileHeaderCard-name">
                  <a class="ProfileHeaderCard-nameLink u-textInheritColor js-nav" href="/MarsWxReport">
                   Mars Weather
                  </a>
                 </h1>
                 <h2 class="ProfileHeaderCard-screenname u-inlineBlock u-dir" dir="ltr">
                  <a class="ProfileHeaderCard-screennameLink u-linkComplex js-nav" href="/MarsWxReport">
                   <span class="username u-dir" dir="ltr">
                    @
                    <b class="u-linkComplex-target">
                     MarsWxReport
                    </b>
                   </span>
                  </a>
                 </h2>
                 <p class="ProfileHeaderCard-bio u-dir" dir="ltr">
                  Updates as avail from the REMS weather instrument aboard
                  <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                   <s>
                    @
                   </s>
                   <b>
                    MarsCuriosity
                   </b>
                  </a>
                  .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                 </p>
                 <div class="ProfileHeaderCard-location ">
                  <span aria-hidden="true" class="Icon Icon--geo Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-locationText u-dir" dir="ltr">
                   Gale Crater, Mars
                  </span>
                 </div>
                 <div class="ProfileHeaderCard-url ">
                  <span aria-hidden="true" class="Icon Icon--url Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-urlText u-dir">
                   <a class="u-textUserColor" href="http://t.co/OcX0oySes3" rel="me nofollow noopener" target="_blank" title="http://mars.nasa.gov/msl/mission/instruments/environsensors/rems/">
                    mars.nasa.gov/msl/mission/in…
                   </a>
                  </span>
                 </div>
                 <div class="ProfileHeaderCard-joinDate">
                  <span aria-hidden="true" class="Icon Icon--calendar Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-joinDateText js-tooltip u-dir" dir="ltr" title="5:48 AM - 28 Aug 2012">
                   Joined August 2012
                  </span>
                 </div>
                 <div class="ProfileHeaderCard-birthdate u-hidden">
                  <span aria-hidden="true" class="Icon Icon--balloon Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-birthdateText u-dir" dir="ltr">
                  </span>
                 </div>
                </div>
                <div class="PhotoRail">
                 <div class="PhotoRail-heading">
                  <span aria-hidden="true" class="Icon Icon--camera Icon--medium" role="presentation">
                  </span>
                  <span class="PhotoRail-headingText">
                   <a class="PhotoRail-headingWithCount js-nav" href="/MarsWxReport/media">
                    182 Photos and videos
                   </a>
                   <a class="PhotoRail-headingWithoutCount js-nav" href="/MarsWxReport/media">
                    Photos and videos
                   </a>
                  </span>
                 </div>
                 <div class="PhotoRail-mediaBox">
                  <span class="js-photoRailInsertPoint">
                  </span>
                 </div>
                </div>
               </div>
              </div>
             </div>
            </div>
            <div class="Grid-cell u-size2of3 u-lg-size3of4">
             <div class="Grid Grid--withGutter">
              <div class="Grid-cell">
               <div class="js-profileClusterFollow">
               </div>
              </div>
              <div class="Grid-cell u-lg-size2of3 " data-test-selector="ProfileTimeline">
               <div class="ProfileHeading">
                <div class="ProfileHeading-spacer">
                </div>
                <div class="ProfileHeading-content">
                 <h2 class="ProfileHeading-title u-hiddenVisually " id="content-main-heading">
                  Tweets
                 </h2>
                 <ul class="ProfileHeading-toggle">
                  <li class="ProfileHeading-toggleItem is-active" data-element-term="tweets_toggle">
                   <span aria-hidden="true">
                    Tweets
                   </span>
                   <span class="u-hiddenVisually">
                    Tweets, current page.
                   </span>
                  </li>
                  <li class="ProfileHeading-toggleItem u-textUserColor" data-element-term="tweets_with_replies_toggle">
                   <a class="ProfileHeading-toggleLink js-openSignupDialog js-nonNavigable" data-nav="tweets_with_replies_toggle" href="/MarsWxReport/with_replies">
                    Tweets &amp; replies
                   </a>
                  </li>
                  <li class="ProfileHeading-toggleItem u-textUserColor" data-element-term="photos_and_videos_toggle">
                   <a class="ProfileHeading-toggleLink js-openSignupDialog js-nonNavigable" data-nav="photos_and_videos_toggle" href="/MarsWxReport/media">
                    Media
                   </a>
                  </li>
                 </ul>
                </div>
               </div>
               <div class="ProfileWarningTimeline" data-element-context="blocked_profile">
                <h2 class="ProfileWarningTimeline-heading" id="content-main-heading">
                 You blocked
                 <span class="username u-dir u-textTruncate" dir="ltr">
                  @
                  <b>
                   MarsWxReport
                  </b>
                 </span>
                </h2>
                <p class="ProfileWarningTimeline-explanation">
                 Are you sure you want to view these Tweets? Viewing Tweets won't unblock
                 <span class="username u-dir u-textTruncate" dir="ltr">
                  @
                  <b>
                   MarsWxReport
                  </b>
                 </span>
                </p>
                <button class="EdgeButton EdgeButton--tertiary ProfileWarningTimeline-button">
                 Yes, view profile
                </button>
               </div>
               <div class="ScrollBumpDialog modal-container" id="scroll-bump-dialog">
                <div class="modal draggable">
                 <div class="modal-content clearfix">
                  <button class="modal-btn modal-close js-close" type="button">
                   <span class="Icon Icon--close Icon--medium">
                    <span class="visuallyhidden">
                     Close
                    </span>
                   </span>
                  </button>
                  <div class="modal-header">
                   <h3 class="modal-title">
                    Mars Weather followed
                   </h3>
                  </div>
                  <div class="modal-body">
                   <div class="loading">
                    <span class="spinner-bigger">
                    </span>
                   </div>
                   <ol class="ScrollBumpDialog-usersList clearfix js-users-list">
                   </ol>
                  </div>
                 </div>
                </div>
               </div>
               <div class="ProfileTimeline " id="timeline">
                <div class="stream-container " data-max-position="1002958236339843073" data-min-position="994003918148571136">
                 <div class="stream-item js-new-items-bar-container">
                 </div>
                 <div class="stream">
                  <ol class="stream-items js-navigable-stream" id="stream-items-id">
                   <li class="js-stream-item stream-item stream-item " data-item-id="1002951794765357058" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"1002951794765357058","scribe_component":"tweet"}' id="stream-item-tweet-1002951794765357058">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet tweet-has-context has-cards has-content " data-conversation-id="1002951794765357058" data-disclosure-type="" data-follows-you="false" data-has-cards="true" data-item-id="1002951794765357058" data-name="CassiniSaturn" data-permalink-path="/CassiniSaturn/status/1002951794765357058" data-reply-to-users-json='[{"id_str":"15165493","screen_name":"CassiniSaturn","name":"CassiniSaturn","emojified_name":{"text":"CassiniSaturn","emojified_text_as_html":"CassiniSaturn"}},{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-retweet-id="1002958236339843073" data-retweeter="MarsWxReport" data-screen-name="CassiniSaturn" data-tweet-id="1002951794765357058" data-tweet-nonce="1002951794765357058-4a584a86-fe5a-492b-82c7-558ca363fd84" data-tweet-stat-initialized="true" data-user-id="15165493" data-you-block="false" data-you-follow="false">
                     <div class="context">
                      <div class="tweet-context with-icn ">
                       <span class="Icon Icon--small Icon--retweeted">
                       </span>
                       <span class="js-retweet-text">
                        <a class="pretty-link js-user-profile-link" data-user-id="786939553" href="/MarsWxReport" rel="noopener">
                         <b>
                          Mars Weather
                         </b>
                        </a>
                        Retweeted
                       </span>
                      </div>
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="15165493" href="/CassiniSaturn">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/814511840449306624/jY7BGXQ2_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          CassiniSaturn
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                          <span class="Icon Icon--verified">
                           <span class="u-hiddenVisually">
                            Verified account
                           </span>
                          </span>
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          CassiniSaturn
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="1002951794765357058" href="/CassiniSaturn/status/1002951794765357058" title="9:35 AM - 2 Jun 2018">
                         <span aria-hidden="true" class="_timestamp js-short-timestamp js-relative-timestamp" data-long-form="true" data-time="1527957316" data-time-ms="1527957316000">
                          7h
                         </span>
                         <span class="u-hiddenVisually" data-aria-label-part="last">
                          7 hours ago
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Saturn’s planet-sized moon Titan, its encircling atmosphere backlit by the Sun, as seen 12 years ago today. Details:
                        <a class="twitter-timeline-link" data-expanded-url="https://go.nasa.gov/2HadMcO" dir="ltr" href="https://t.co/AIR704OKXD" rel="nofollow noopener" target="_blank" title="https://go.nasa.gov/2HadMcO">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          go.nasa.gov/2HadMcO
                         </span>
                         <span class="invisible">
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                         </span>
                        </a>
                        <a class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr" href="/hashtag/SaturnSaturday?src=hash">
                         <s>
                          #
                         </s>
                         <b>
                          SaturnSaturday
                         </b>
                        </a>
                        <a class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr" href="https://t.co/zeVCa1N2vd">
                         pic.twitter.com/zeVCa1N2vd
                        </a>
                       </p>
                      </div>
                      <div class="AdaptiveMediaOuterContainer">
                       <div class="AdaptiveMedia is-square ">
                        <div class="AdaptiveMedia-container">
                         <div class="AdaptiveMedia-singlePhoto" style="padding-top: calc(1.1301703163017032 * 100% - 0.5px);">
                          <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[38,38,38]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/Desy5GtV4AEWO8s.jpg" style="background-color:rgba(38,38,38,1.0);">
                           <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/Desy5GtV4AEWO8s.jpg" style="width: 100%; top: -32px;"/>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="8">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-1002951794765357058">
                           8 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="259">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-1002951794765357058">
                           259 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="905">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-1002951794765357058">
                           905 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-1002951794765357058" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-1002951794765357058" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            259
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            259
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-1002951794765357058" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            905
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            905
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="1002909566361841665" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"1002909566361841665","scribe_component":"tweet"}' id="stream-item-tweet-1002909566361841665">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="1002909566361841665" data-disclosure-type="" data-follows-you="false" data-item-id="1002909566361841665" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/1002909566361841665" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="1002909566361841665" data-tweet-nonce="1002909566361841665-6eae1a59-2fc1-4f95-8d53-c431f808377a" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="1002909566361841665" href="/MarsWxReport/status/1002909566361841665" title="6:47 AM - 2 Jun 2018">
                         <span aria-hidden="true" class="_timestamp js-short-timestamp js-relative-timestamp" data-long-form="true" data-time="1527947248" data-time-ms="1527947248000">
                          10h
                         </span>
                         <span class="u-hiddenVisually" data-aria-label-part="last">
                          10 hours ago
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2067 (May 30, 2018), Sunny, high 3C/37F, low -74C/-101F, pressure at 7.43 hPa, daylight 05:19-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="2">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-1002909566361841665">
                           2 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="9">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-1002909566361841665">
                           9 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="22">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-1002909566361841665">
                           22 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-1002909566361841665" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            2
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-1002909566361841665" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-1002909566361841665" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            22
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            22
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="1002308951956971520" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"1002308951956971520","scribe_component":"tweet"}' id="stream-item-tweet-1002308951956971520">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet tweet-has-context has-cards has-content " data-conversation-id="1002308951956971520" data-disclosure-type="" data-follows-you="false" data-has-cards="true" data-item-id="1002308951956971520" data-name="Christian Fröschlin" data-permalink-path="/chrfrde/status/1002308951956971520" data-reply-to-users-json='[{"id_str":"308444820","screen_name":"chrfrde","name":"Christian Fr\u00f6schlin","emojified_name":{"text":"Christian Fr\u00f6schlin","emojified_text_as_html":"Christian Fr\u00f6schlin"}},{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-retweet-id="1002624726672519169" data-retweeter="MarsWxReport" data-screen-name="chrfrde" data-tweet-id="1002308951956971520" data-tweet-nonce="1002308951956971520-340e79c6-ac6a-46de-941e-a253fd6a0278" data-tweet-stat-initialized="true" data-user-id="308444820" data-you-block="false" data-you-follow="false">
                     <div class="context">
                      <div class="tweet-context with-icn ">
                       <span class="Icon Icon--small Icon--retweeted">
                       </span>
                       <span class="js-retweet-text">
                        <a class="pretty-link js-user-profile-link" data-user-id="786939553" href="/MarsWxReport" rel="noopener">
                         <b>
                          Mars Weather
                         </b>
                        </a>
                        Retweeted
                       </span>
                      </div>
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="308444820" href="/chrfrde">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2730788875/deb0e3e052694cb7a2bc242bd7d6d69d_bigger.jpeg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Christian Fröschlin
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          chrfrde
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="1002308951956971520" href="/chrfrde/status/1002308951956971520" title="3:00 PM - 31 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1527804050" data-time-ms="1527804050000">
                          May 31
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Three views of
                        <a class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr" href="/hashtag/ISS?src=hash">
                         <s>
                          #
                         </s>
                         <b>
                          ISS
                         </b>
                        </a>
                        pass tonight as seen from The Hague, NL. 7 x 0.2 ms unfiltered mono in Celestron 8" at f/10.
                        <a class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr" href="https://t.co/5PvF1ECjjf">
                         pic.twitter.com/5PvF1ECjjf
                        </a>
                       </p>
                      </div>
                      <div class="AdaptiveMediaOuterContainer">
                       <div class="AdaptiveMedia is-square ">
                        <div class="AdaptiveMedia-container">
                         <div class="AdaptiveMedia-singlePhoto" style="padding-top: calc(0.3706896551724138 * 100% - 0.5px);">
                          <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[38,38,38]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DejqMi3WAAAsYPv.jpg" style="background-color:rgba(38,38,38,1.0);">
                           <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DejqMi3WAAAsYPv.jpg" style="width: 100%; top: -0px;"/>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="12">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-1002308951956971520">
                           12 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="75">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-1002308951956971520">
                           75 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="299">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-1002308951956971520">
                           299 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-1002308951956971520" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            12
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-1002308951956971520" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            75
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            75
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-1002308951956971520" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            299
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            299
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                      <div class="self-thread-context">
                       Show this thread
                      </div>
                      <div class="self-thread-tweet-cta self-thread-head">
                       <div class="mini-avatar-with-thread">
                        <img class="avatar--circular size24" src="https://pbs.twimg.com/profile_images/2730788875/deb0e3e052694cb7a2bc242bd7d6d69d_normal.jpeg"/>
                       </div>
                       <a class="js-nav show-thread-link" href="/chrfrde/status/1002308951956971520">
                        Show this thread
                       </a>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="1001976365271404544" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"1001976365271404544","scribe_component":"tweet"}' id="stream-item-tweet-1001976365271404544">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="1001976365271404544" data-disclosure-type="" data-follows-you="false" data-item-id="1001976365271404544" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/1001976365271404544" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="1001976365271404544" data-tweet-nonce="1001976365271404544-30c1e127-6293-4f0e-9fd1-99bee768e41f" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="1001976365271404544" href="/MarsWxReport/status/1001976365271404544" title="4:59 PM - 30 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1527724755" data-time-ms="1527724755000">
                          May 30
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2063 (May 26, 2018), Sunny, high 3C/37F, low -71C/-95F, pressure at 7.48 hPa, daylight 05:19-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-1001976365271404544">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="7">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-1001976365271404544">
                           7 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="23">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-1001976365271404544">
                           23 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-1001976365271404544" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-1001976365271404544" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-1001976365271404544" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            23
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            23
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="1001613980325109760" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"1001613980325109760","scribe_component":"tweet"}' id="stream-item-tweet-1001613980325109760">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="1001613980325109760" data-disclosure-type="" data-follows-you="false" data-item-id="1001613980325109760" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/1001613980325109760" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="1001613980325109760" data-tweet-nonce="1001613980325109760-37e71137-d362-4d7e-a8d0-8e476c270877" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="1001613980325109760" href="/MarsWxReport/status/1001613980325109760" title="4:59 PM - 29 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1527638356" data-time-ms="1527638356000">
                          May 29
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2062 (May 25, 2018), Sunny, high 2C/35F, low -72C/-97F, pressure at 7.45 hPa, daylight 05:19-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-1001613980325109760">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="7">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-1001613980325109760">
                           7 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="22">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-1001613980325109760">
                           22 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-1001613980325109760" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-1001613980325109760" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-1001613980325109760" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            22
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            22
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="1000164447279878144" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"1000164447279878144","scribe_component":"tweet"}' id="stream-item-tweet-1000164447279878144">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="1000164447279878144" data-disclosure-type="" data-follows-you="false" data-item-id="1000164447279878144" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/1000164447279878144" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="1000164447279878144" data-tweet-nonce="1000164447279878144-1104ddd0-1717-4259-951d-a4fcbe350ed1" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="1000164447279878144" href="/MarsWxReport/status/1000164447279878144" title="4:59 PM - 25 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1527292761" data-time-ms="1527292761000">
                          May 25
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2060 (May 23, 2018), Sunny, high 4C/39F, low -73C/-99F, pressure at 7.43 hPa, daylight 05:20-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-1000164447279878144">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="8">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-1000164447279878144">
                           8 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="25">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-1000164447279878144">
                           25 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-1000164447279878144" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-1000164447279878144" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-1000164447279878144" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            25
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            25
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="999990283533213696" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"999990283533213696","scribe_component":"tweet"}' id="stream-item-tweet-999990283533213696">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet tweet-has-context has-cards cards-forward " data-card2-type="player" data-conversation-id="999990283533213696" data-disclosure-type="" data-follows-you="false" data-has-cards="true" data-item-id="999990283533213696" data-name="Tony Rice" data-permalink-path="/rtphokie/status/999990283533213696" data-reply-to-users-json='[{"id_str":"16207462","screen_name":"rtphokie","name":"Tony Rice","emojified_name":{"text":"Tony Rice","emojified_text_as_html":"Tony Rice"}},{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-retweet-id="999990479998672896" data-retweeter="MarsWxReport" data-screen-name="rtphokie" data-tweet-id="999990283533213696" data-tweet-nonce="999990283533213696-4dad2e80-5870-44c6-abd5-015e93d663d3" data-tweet-stat-initialized="true" data-user-id="16207462" data-you-block="false" data-you-follow="false">
                     <div class="context">
                      <div class="tweet-context with-icn ">
                       <span class="Icon Icon--small Icon--retweeted">
                       </span>
                       <span class="js-retweet-text">
                        <a class="pretty-link js-user-profile-link" data-user-id="786939553" href="/MarsWxReport" rel="noopener">
                         <b>
                          Mars Weather
                         </b>
                        </a>
                        Retweeted
                       </span>
                      </div>
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="16207462" href="/rtphokie">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/804445910667296768/dr2IIYda_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Tony Rice
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                          <span class="Icon Icon--verified">
                           <span class="u-hiddenVisually">
                            Verified account
                           </span>
                          </span>
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          rtphokie
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="999990283533213696" href="/rtphokie/status/999990283533213696" title="5:27 AM - 25 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1527251237" data-time-ms="1527251237000">
                          May 25
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        On this day in 1961, President Kennedy asked a joint session of Congress to commit to "achieving the goal, before this decade is out, of landing a man on the Moon and returning him safely to the Earth."
                        <a class="twitter-timeline-link u-hidden" data-expanded-url="https://www.youtube.com/watch?v=TUXuV7XbZvU" dir="ltr" href="https://t.co/6JjCEll0Av" rel="nofollow noopener" target="_blank" title="https://www.youtube.com/watch?v=TUXuV7XbZvU">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://www.
                         </span>
                         <span class="js-display-url">
                          youtube.com/watch?v=TUXuV7
                         </span>
                         <span class="invisible">
                          XbZvU
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                       </p>
                      </div>
                      <div class="card2 js-media-container " data-card2-name="player">
                       <div class="js-macaw-cards-iframe-container initial-card-height card-type-player" data-amplify-content-id="" data-amplify-playlist-url="" data-card-name="player" data-card-url="https://t.co/6JjCEll0Av" data-creator-id="" data-full-card-iframe-url="/i/cards/tfw/v1/999990283533213696?cardname=player&amp;autoplay_disabled=true&amp;earned=true&amp;edge=true&amp;lang=en" data-has-autoplayable-media="false" data-publisher-id="10228272" data-src="/i/cards/tfw/v1/999990283533213696?cardname=player&amp;autoplay_disabled=true&amp;forward=true&amp;earned=true&amp;edge=true&amp;lang=en">
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-999990283533213696">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-999990283533213696">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="25">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-999990283533213696">
                           25 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-999990283533213696" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-999990283533213696" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-999990283533213696" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            25
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            25
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="999439678091689985" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"999439678091689985","scribe_component":"tweet"}' id="stream-item-tweet-999439678091689985">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="999439678091689985" data-disclosure-type="" data-follows-you="false" data-item-id="999439678091689985" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/999439678091689985" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="999439678091689985" data-tweet-nonce="999439678091689985-e96942db-d416-4c5d-897b-dbdc546d2eba" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="999439678091689985" href="/MarsWxReport/status/999439678091689985" title="4:59 PM - 23 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1527119962" data-time-ms="1527119962000">
                          May 23
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2058 (May 21, 2018), Sunny, high 4C/39F, low -71C/-95F, pressure at 7.43 hPa, daylight 05:20-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-999439678091689985">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-999439678091689985">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="24">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-999439678091689985">
                           24 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-999439678091689985" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-999439678091689985" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-999439678091689985" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            24
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            24
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="998934003213193217" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"998934003213193217","scribe_component":"tweet"}' id="stream-item-tweet-998934003213193217">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet has-cards has-content " data-conversation-id="998934003213193217" data-disclosure-type="" data-follows-you="false" data-has-cards="true" data-item-id="998934003213193217" data-mentions="MarsCuriosity" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/998934003213193217" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}},{"id_str":"15473958","screen_name":"MarsCuriosity","name":"Curiosity Rover","emojified_name":{"text":"Curiosity Rover","emojified_text_as_html":"Curiosity Rover"}}]' data-screen-name="MarsWxReport" data-tweet-id="998934003213193217" data-tweet-nonce="998934003213193217-2e515765-b1d1-4996-bc38-276f05205ef2" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="998934003213193217" href="/MarsWxReport/status/998934003213193217" title="7:30 AM - 22 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526999400" data-time-ms="1526999400000">
                          May 22
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Welcome Spring! (to
                        <a class="twitter-atreply pretty-link js-nav" data-mentioned-user-id="15473958" dir="ltr" href="/MarsCuriosity">
                         <s>
                          @
                         </s>
                         <b>
                          MarsCuriosity
                         </b>
                        </a>
                        ’s home in the southern hemisphere of Mars). May 22 at 1431 UTC Mars reached a solar longitude of 180° in its trip around the sun
                        <a class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr" href="https://t.co/bzbkEwvfE4">
                         pic.twitter.com/bzbkEwvfE4
                        </a>
                       </p>
                      </div>
                      <div class="AdaptiveMediaOuterContainer">
                       <div class="AdaptiveMedia is-square " style="max-width:450px;">
                        <div class="AdaptiveMedia-container">
                         <div class="AdaptiveMedia-singlePhoto" style="padding-top: calc(0.5311111111111111 * 100% - 0.5px);">
                          <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[64,46,30]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DdzKnEJVAAA-ZDp.jpg" style="background-color:rgba(64,46,30,1.0);">
                           <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DdzKnEJVAAA-ZDp.jpg"/>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-998934003213193217">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="23">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-998934003213193217">
                           23 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="37">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-998934003213193217">
                           37 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-998934003213193217" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-998934003213193217" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            23
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            23
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-998934003213193217" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            37
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            37
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="998745545039462400" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"998745545039462400","scribe_component":"tweet"}' id="stream-item-tweet-998745545039462400">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet tweet-has-context " data-conversation-id="998745545039462400" data-disclosure-type="" data-follows-you="false" data-item-id="998745545039462400" data-name="Tanya Harrison" data-permalink-path="/tanyaofmars/status/998745545039462400" data-reply-to-users-json='[{"id_str":"25219709","screen_name":"tanyaofmars","name":"Tanya Harrison","emojified_name":{"text":"Tanya Harrison","emojified_text_as_html":"Tanya Harrison"}},{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-retweet-id="998748132287680512" data-retweeter="MarsWxReport" data-screen-name="tanyaofmars" data-tweet-id="998745545039462400" data-tweet-nonce="998745545039462400-f4c951ca-6c3a-4f05-ade8-a01b1a9401ed" data-tweet-stat-initialized="true" data-user-id="25219709" data-you-block="false" data-you-follow="false">
                     <div class="context">
                      <div class="tweet-context with-icn ">
                       <span class="Icon Icon--small Icon--retweeted">
                       </span>
                       <span class="js-retweet-text">
                        <a class="pretty-link js-user-profile-link" data-user-id="786939553" href="/MarsWxReport" rel="noopener">
                         <b>
                          Mars Weather
                         </b>
                        </a>
                        Retweeted
                       </span>
                      </div>
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="25219709" href="/tanyaofmars">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/837323515942453248/TehRrI9a_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate ">
                          Tanya Harrison
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                          <span class="Icon Icon--verified">
                           <span class="u-hiddenVisually">
                            Verified account
                           </span>
                          </span>
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          tanyaofmars
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="998745545039462400" href="/tanyaofmars/status/998745545039462400" title="7:01 PM - 21 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526954468" data-time-ms="1526954468000">
                          May 21
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="1">
                       Tanya Harrison Retweeted Kevin M. Gill
                      </p>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="4" lang="en">
                        The dust devil tracks are the squiggly bluish lines, where the dust devils have swept away the red dust that coats
                        <a class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr" href="/hashtag/Mars?src=hash">
                         <s>
                          #
                         </s>
                         <b>
                          Mars
                         </b>
                        </a>
                        ' surface to reveal the underlying darker sand dunes.
                        <a class="twitter-timeline-link u-hidden" data-expanded-url="https://twitter.com/kevinmgill/status/998710663072563200" dir="ltr" href="https://t.co/oPALZfn8b8" rel="nofollow noopener" target="_blank" title="https://twitter.com/kevinmgill/status/998710663072563200">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          twitter.com/kevinmgill/sta
                         </span>
                         <span class="invisible">
                          tus/998710663072563200
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                       </p>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="3">
                       Tanya Harrison added,
                      </p>
                      <div class="QuoteTweet u-block js-tweet-details-fixer">
                       <div class="QuoteTweet-container">
                        <a aria-hidden="true" class="QuoteTweet-link js-nav" data-conversation-id="998645441108496384" href="/kevinmgill/status/998710663072563200">
                        </a>
                        <div class="QuoteTweet-innerContainer u-cf js-permalink js-media-container" data-conversation-id="998645441108496384" data-item-id="998710663072563200" data-item-type="tweet" data-screen-name="kevinmgill" data-user-id="18145341" href="/kevinmgill/status/998710663072563200" tabindex="0">
                         <div class="tweet-content">
                          <div class="QuoteMedia">
                           <div class="QuoteMedia-container js-quote-media-container">
                            <div class="QuoteMedia-singlePhoto">
                             <div class="QuoteMedia-photoContainer js-quote-photo" data-dominant-color="[64,40,33]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/Ddwht3SVwAAKCU-.jpg" style="background-color:rgba(64,40,33,1.0);">
                              <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/Ddwht3SVwAAKCU-.jpg" style="height: 100%; left: -39px;"/>
                             </div>
                            </div>
                           </div>
                          </div>
                          <div class="QuoteTweet-authorAndText u-alignTop">
                           <div class="QuoteTweet-originalAuthor u-cf u-textTruncate stream-item-header account-group js-user-profile-link">
                            <b class="QuoteTweet-fullname u-linkComplex-target">
                             Kevin M. Gill
                            </b>
                            <span class="UserBadges">
                            </span>
                            <span class="UserNameBreak">
                            </span>
                            <span class="username u-dir u-textTruncate" dir="ltr">
                             @
                             <b>
                              kevinmgill
                             </b>
                            </span>
                           </div>
                           <div class="QuoteTweet-text tweet-text u-dir js-ellipsis" data-aria-label-part="2" dir="ltr" lang="en">
                            Bird's eye view of intracrater dunes and the tracks of countless dust devils on
                            <span class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr">
                             <s>
                              #
                             </s>
                             <b>
                              Mars
                             </b>
                            </span>
                            -
                            <span class="twitter-timeline-link" data-expanded-url="https://flic.kr/p/24D2hay" dir="ltr" rel="nofollow noopener" target="_blank" title="https://flic.kr/p/24D2hay">
                             <span class="tco-ellipsis">
                             </span>
                             <span class="invisible">
                              https://
                             </span>
                             <span class="js-display-url">
                              flic.kr/p/24D2hay
                             </span>
                             <span class="invisible">
                             </span>
                             <span class="tco-ellipsis">
                              <span class="invisible">
                              </span>
                             </span>
                            </span>
                            <span class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr">
                             pic.twitter.com/icqzU4KfMD
                            </span>
                           </div>
                           <div class="self-thread-context">
                            Show this thread
                           </div>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="3">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-998745545039462400">
                           3 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-998745545039462400">
                           19 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="70">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-998745545039462400">
                           70 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-998745545039462400" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            3
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-998745545039462400" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-998745545039462400" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            70
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            70
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="998714910195503105" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"998714910195503105","scribe_component":"tweet"}' id="stream-item-tweet-998714910195503105">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="998714910195503105" data-disclosure-type="" data-follows-you="false" data-item-id="998714910195503105" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/998714910195503105" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="998714910195503105" data-tweet-nonce="998714910195503105-2dbdbc13-fd24-418a-9fcc-112fa09799c2" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="998714910195503105" href="/MarsWxReport/status/998714910195503105" title="4:59 PM - 21 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526947164" data-time-ms="1526947164000">
                          May 21
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2056 (May 19, 2018), Sunny, high 5C/41F, low -74C/-101F, pressure at 7.40 hPa, daylight 05:20-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-998714910195503105">
                           1 reply
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="9">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-998714910195503105">
                           9 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="16">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-998714910195503105">
                           16 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-998714910195503105" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-998714910195503105" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-998714910195503105" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            16
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            16
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="997627758871277568" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"997627758871277568","scribe_component":"tweet"}' id="stream-item-tweet-997627758871277568">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="997627758871277568" data-disclosure-type="" data-follows-you="false" data-item-id="997627758871277568" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/997627758871277568" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="997627758871277568" data-tweet-nonce="997627758871277568-603a56a7-36c8-4110-9b97-9a9e4ecb0575" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="997627758871277568" href="/MarsWxReport/status/997627758871277568" title="4:59 PM - 18 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526687967" data-time-ms="1526687967000">
                          May 18
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2054 (May 17, 2018), Sunny, high 4C/39F, low -72C/-97F, pressure at 7.40 hPa, daylight 05:21-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="2">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-997627758871277568">
                           2 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="6">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-997627758871277568">
                           6 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="17">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-997627758871277568">
                           17 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-997627758871277568" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            2
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-997627758871277568" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-997627758871277568" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="997265374025482240" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"997265374025482240","scribe_component":"tweet"}' id="stream-item-tweet-997265374025482240">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="997265374025482240" data-disclosure-type="" data-follows-you="false" data-item-id="997265374025482240" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/997265374025482240" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="997265374025482240" data-tweet-nonce="997265374025482240-cb814a72-28c0-4771-9939-1e0b45028b58" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="997265374025482240" href="/MarsWxReport/status/997265374025482240" title="4:59 PM - 17 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526601568" data-time-ms="1526601568000">
                          May 17
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2053 (May 16, 2018), Sunny, high 3C/37F, low -71C/-95F, pressure at 7.40 hPa, daylight 05:21-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-997265374025482240">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="14">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-997265374025482240">
                           14 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="27">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-997265374025482240">
                           27 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-997265374025482240" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-997265374025482240" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            14
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            14
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-997265374025482240" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            27
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            27
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="996902987674025984" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"996902987674025984","scribe_component":"tweet"}' id="stream-item-tweet-996902987674025984">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="996902987674025984" data-disclosure-type="" data-follows-you="false" data-item-id="996902987674025984" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/996902987674025984" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="996902987674025984" data-tweet-nonce="996902987674025984-d4e3889a-0ba8-4eba-b435-ea177c36e7b5" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="996902987674025984" href="/MarsWxReport/status/996902987674025984" title="4:59 PM - 16 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526515168" data-time-ms="1526515168000">
                          May 16
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2051 (May 14, 2018), Sunny, high 1C/33F, low -71C/-95F, pressure at 7.39 hPa, daylight 05:21-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-996902987674025984">
                           1 reply
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-996902987674025984">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="17">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-996902987674025984">
                           17 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-996902987674025984" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-996902987674025984" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-996902987674025984" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="996178220507680768" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"996178220507680768","scribe_component":"tweet"}' id="stream-item-tweet-996178220507680768">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="996178220507680768" data-disclosure-type="" data-follows-you="false" data-item-id="996178220507680768" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/996178220507680768" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="996178220507680768" data-tweet-nonce="996178220507680768-19c55495-3e1c-4821-8593-a2987c5e3e1e" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="996178220507680768" href="/MarsWxReport/status/996178220507680768" title="4:59 PM - 14 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526342370" data-time-ms="1526342370000">
                          May 14
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2050 (May 13, 2018), Sunny, high 1C/33F, low -71C/-95F, pressure at 7.37 hPa, daylight 05:21-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-996178220507680768">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="9">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-996178220507680768">
                           9 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="21">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-996178220507680768">
                           21 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-996178220507680768" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-996178220507680768" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-996178220507680768" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            21
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            21
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="995091070500392961" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"995091070500392961","scribe_component":"tweet"}' id="stream-item-tweet-995091070500392961">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="995091070500392961" data-disclosure-type="" data-follows-you="false" data-item-id="995091070500392961" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/995091070500392961" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="995091070500392961" data-tweet-nonce="995091070500392961-fbb896a0-b02e-462b-9fe0-fa34179e31a2" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="995091070500392961" href="/MarsWxReport/status/995091070500392961" title="4:59 PM - 11 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526083173" data-time-ms="1526083173000">
                          May 11
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2047 (May 10, 2018), Sunny, high 3C/37F, low -71C/-95F, pressure at 7.33 hPa, daylight 05:22-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-995091070500392961">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="6">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-995091070500392961">
                           6 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="14">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-995091070500392961">
                           14 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-995091070500392961" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-995091070500392961" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-995091070500392961" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            14
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            14
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994766443555250176" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994766443555250176","scribe_component":"tweet"}' id="stream-item-tweet-994766443555250176">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994766443555250176" data-disclosure-type="" data-follows-you="false" data-item-id="994766443555250176" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994766443555250176" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994766443555250176" data-tweet-nonce="994766443555250176-888a1861-7312-4b7f-87a8-b8b74edb7991" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate ">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994766443555250176" href="/MarsWxReport/status/994766443555250176" title="7:29 PM - 10 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1526005776" data-time-ms="1526005776000">
                          May 10
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="1">
                       Mars Weather Retweeted Sam Sun
                      </p>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="4" lang="en">
                        <a class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr" href="/hashtag/InSight?src=hash">
                         <s>
                          #
                         </s>
                         <b>
                          InSight
                         </b>
                        </a>
                        rising above the California fog on liftoff.
                        <a class="twitter-timeline-link u-hidden" data-expanded-url="https://twitter.com/birdsnspace/status/993603886106660864" dir="ltr" href="https://t.co/7bMYYBvGlA" rel="nofollow noopener" target="_blank" title="https://twitter.com/birdsnspace/status/993603886106660864">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          twitter.com/birdsnspace/st
                         </span>
                         <span class="invisible">
                          atus/993603886106660864
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                       </p>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="3">
                       Mars Weather added,
                      </p>
                      <div class="QuoteTweet u-block js-tweet-details-fixer">
                       <div class="QuoteTweet-container">
                        <a aria-hidden="true" class="QuoteTweet-link js-nav" data-conversation-id="993603886106660864" href="/BirdsNSpace/status/993603886106660864">
                        </a>
                        <div class="QuoteTweet-innerContainer u-cf js-permalink js-media-container" data-conversation-id="993603886106660864" data-item-id="993603886106660864" data-item-type="tweet" data-screen-name="BirdsNSpace" data-user-id="993061794296938497" href="/BirdsNSpace/status/993603886106660864" tabindex="0">
                         <div class="tweet-content">
                          <div class="QuoteMedia">
                           <div class="QuoteMedia-container js-quote-media-container">
                            <div class="QuoteMedia-singlePhoto">
                             <div class="QuoteMedia-photoContainer js-quote-photo" data-dominant-color="[38,19,10]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/Dcn5APsVMAAj80X.jpg" style="background-color:rgba(38,19,10,1.0);">
                              <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/Dcn5APsVMAAj80X.jpg" style="height: 100%; left: -25px;"/>
                             </div>
                            </div>
                           </div>
                          </div>
                          <div class="QuoteTweet-authorAndText u-alignTop">
                           <div class="QuoteTweet-originalAuthor u-cf u-textTruncate stream-item-header account-group js-user-profile-link">
                            <b class="QuoteTweet-fullname u-linkComplex-target">
                             Sam Sun
                            </b>
                            <span class="UserBadges">
                            </span>
                            <span class="UserNameBreak">
                            </span>
                            <span class="username u-dir u-textTruncate" dir="ltr">
                             @
                             <b>
                              BirdsNSpace
                             </b>
                            </span>
                           </div>
                           <div class="QuoteTweet-text tweet-text u-dir js-ellipsis" data-aria-label-part="2" dir="ltr" lang="en">
                            I've been quietly supporting
                            <span class="twitter-atreply pretty-link js-nav" data-mentioned-user-id="21292523" dir="ltr">
                             <s>
                              @
                             </s>
                             <b>
                              NASASpaceFlight
                             </b>
                            </span>
                            with aerial launch photography for a while but finally joining the twittersphere as this photo of the Mars
                            <span class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr">
                             <s>
                              #
                             </s>
                             <b>
                              InSight
                             </b>
                            </span>
                            launch wanted my audience.
                            <span class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr">
                             <s>
                              #
                             </s>
                             <b>
                              myfirstTweet
                             </b>
                            </span>
                            <span class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr">
                             pic.twitter.com/51q1OFpU9j
                            </span>
                           </div>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994766443555250176">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994766443555250176">
                           1 retweet
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="7">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994766443555250176">
                           7 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994766443555250176" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994766443555250176" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994766443555250176" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994366302545498113" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994366302545498113","scribe_component":"tweet"}' id="stream-item-tweet-994366302545498113">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994366302545498113" data-disclosure-type="" data-follows-you="false" data-item-id="994366302545498113" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994366302545498113" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994366302545498113" data-tweet-nonce="994366302545498113-ec7f9f7e-f5e6-4bbe-ab2c-ce3ebfe8ff3c" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994366302545498113" href="/MarsWxReport/status/994366302545498113" title="4:59 PM - 9 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525910375" data-time-ms="1525910375000">
                          May 9
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2045 (May 08, 2018), Sunny, high -7C/19F, low -74C/-101F, pressure at 7.33 hPa, daylight 05:22-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994366302545498113">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="5">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994366302545498113">
                           5 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994366302545498113">
                           10 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994366302545498113" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994366302545498113" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            5
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            5
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994366302545498113" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994076500340215809" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994076500340215809","scribe_component":"tweet"}' id="stream-item-tweet-994076500340215809">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994076500340215809" data-disclosure-type="" data-follows-you="false" data-item-id="994076500340215809" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994076500340215809" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994076500340215809" data-tweet-nonce="994076500340215809-05ec0fa9-a969-4df7-8071-b901406834e4" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate ">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994076500340215809" href="/MarsWxReport/status/994076500340215809" title="9:48 PM - 8 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525841281" data-time-ms="1525841281000">
                          May 8
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="1">
                       Mars Weather Retweeted Doug Ellison
                      </p>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="4" lang="en">
                        What a long beautiful neck full of science you have Curiosity’s Earth bound twin sister
                        <a class="twitter-timeline-link u-hidden" data-expanded-url="https://twitter.com/doug_ellison/status/994057810668212225" dir="ltr" href="https://t.co/NIJoNgmRzy" rel="nofollow noopener" target="_blank" title="https://twitter.com/doug_ellison/status/994057810668212225">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          twitter.com/doug_ellison/s
                         </span>
                         <span class="invisible">
                          tatus/994057810668212225
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                       </p>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="3">
                       Mars Weather added,
                      </p>
                      <div class="QuoteTweet u-block js-tweet-details-fixer">
                       <div class="QuoteTweet-container">
                        <a aria-hidden="true" class="QuoteTweet-link js-nav" data-conversation-id="994057810668212225" href="/doug_ellison/status/994057810668212225">
                        </a>
                        <div class="QuoteTweet-innerContainer u-cf js-permalink js-media-container" data-conversation-id="994057810668212225" data-item-id="994057810668212225" data-item-type="tweet" data-screen-name="doug_ellison" data-user-id="15402623" href="/doug_ellison/status/994057810668212225" tabindex="0">
                         <div class="tweet-content">
                          <div class="QuoteMedia">
                           <div class="QuoteMedia-container js-quote-media-container">
                            <div class="QuoteMedia-singlePhoto">
                             <div class="QuoteMedia-photoContainer js-quote-photo" data-dominant-color="[64,61,47]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DcuaTNwVMAEqy3k.jpg" style="background-color:rgba(64,61,47,1.0);">
                              <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DcuaTNwVMAEqy3k.jpg" style="width: 100%; top: -81px;"/>
                             </div>
                            </div>
                           </div>
                          </div>
                          <div class="QuoteTweet-authorAndText u-alignTop">
                           <div class="QuoteTweet-originalAuthor u-cf u-textTruncate stream-item-header account-group js-user-profile-link">
                            <b class="QuoteTweet-fullname u-linkComplex-target">
                             Doug Ellison
                            </b>
                            <span class="UserBadges">
                            </span>
                            <span class="UserNameBreak">
                            </span>
                            <span class="username u-dir u-textTruncate" dir="ltr">
                             @
                             <b>
                              doug_ellison
                             </b>
                            </span>
                           </div>
                           <div class="QuoteTweet-text tweet-text u-dir js-ellipsis" data-aria-label-part="2" dir="ltr" lang="en">
                            So important to visit the testbed every now and again....reminds me of the hardware I'm operating on Mars. Having a mental model of it really helps with planning. Watching this hardware execute commands makes it all a lot less intangible.
                            <span class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr">
                             pic.twitter.com/lMHq3kUlLp
                            </span>
                           </div>
                           <div class="self-thread-context">
                            Show this thread
                           </div>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994076500340215809">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994076500340215809">
                           1 retweet
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="4">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994076500340215809">
                           4 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994076500340215809" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994076500340215809" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994076500340215809" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            4
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            4
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994003918148571136" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994003918148571136","scribe_component":"tweet"}' id="stream-item-tweet-994003918148571136">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994003918148571136" data-disclosure-type="" data-follows-you="false" data-item-id="994003918148571136" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994003918148571136" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994003918148571136" data-tweet-nonce="994003918148571136-0693e665-10a7-48ac-987a-6c524c6801a2" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ‏
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994003918148571136" href="/MarsWxReport/status/994003918148571136" title="4:59 PM - 8 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525823976" data-time-ms="1525823976000">
                          May 8
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2043 (May 06, 2018), Sunny, high -14C/6F, low -71C/-95F, pressure at 7.36 hPa, daylight 05:22-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994003918148571136">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="7">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994003918148571136">
                           7 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994003918148571136">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994003918148571136" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994003918148571136" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994003918148571136" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                  </ol>
                  <div class="stream-footer ">
                   <div class="timeline-end has-items has-more-items">
                    <div class="stream-end">
                     <div class="stream-end-inner">
                      <span class="Icon Icon--large Icon--logo">
                      </span>
                      <p class="empty-text">
                       @MarsWxReport hasn't Tweeted yet.
                      </p>
                      <p>
                       <button class="btn-link back-to-top hidden" type="button">
                        Back to top ↑
                       </button>
                      </p>
                     </div>
                    </div>
                    <div class="stream-loading">
                     <div class="stream-end-inner">
                      <span class="spinner" title="Loading...">
                      </span>
                     </div>
                    </div>
                   </div>
                  </div>
                  <div class="stream-fail-container">
                   <div class="js-stream-whale-end stream-whale-end stream-placeholder centered-placeholder">
                    <div class="stream-end-inner">
                     <h2 class="title">
                      Loading seems to be taking a while.
                     </h2>
                     <p>
                      Twitter may be over capacity or experiencing a momentary hiccup.
                      <a class="try-again-after-whale" href="#" role="button">
                       Try again
                      </a>
                      or visit
                      <a href="http://status.twitter.com" rel="noopener" target="_blank">
                       Twitter Status
                      </a>
                      for more information.
                     </p>
                    </div>
                   </div>
                  </div>
                  <ol class="hidden-replies-container">
                  </ol>
                 </div>
                </div>
               </div>
              </div>
              <div class="Grid-cell u-size1of3">
               <div class="Grid Grid--withGutter">
                <div class="Grid-cell">
                 <div class="ProfileSidebar ProfileSidebar--withRightAlignment">
                  <div class="MoveableModule">
                   <div class="SidebarCommonModules">
                    <div class="SignupCallOut module js-signup-call-out ">
                     <div class="SignupCallOut-header">
                      <h3 class="SignupCallOut-title u-textBreak">
                       New to Twitter?
                      </h3>
                     </div>
                     <div class="SignupCallOut-subheader">
                      Sign up now to get your own personalized timeline!
                     </div>
                     <div class="signup SignupForm ">
                      <a class="EdgeButton EdgeButton--large EdgeButton--primary SignupForm-submit u-block js-signup " data-component="signup_callout" data-element="form" href="https://twitter.com/signup" role="button">
                       Sign up
                      </a>
                     </div>
                    </div>
                    <div class="RelatedUsers module u-hidden">
                     <div class="RelatedUsers-header">
                      <h3 class="RelatedUsers-title">
                       You may also like
                      </h3>
                      ·
                      <button class="btn-link js-refresh-related-users" type="button">
                       Refresh
                      </button>
                     </div>
                     <div class="RelatedUsers-users">
                     </div>
                    </div>
                    <div class="module Trends trends hidden">
                     <div class="trends-inner">
                      <div class="flex-module trends-container ">
                       <div class="flex-module-header">
                        <h3>
                         <span class="trend-location js-trend-location">
                          false
                         </span>
                        </h3>
                       </div>
                       <div class="flex-module-inner">
                        <ul class="trend-items js-trends">
                        </ul>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="Footer module roaming-module Footer--slim Footer--blankBackground">
                     <div class="flex-module">
                      <div class="flex-module-inner js-items-container">
                       <ul class="u-cf">
                        <li class="Footer-item Footer-copyright copyright">
                         © 2018 Twitter
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="/about" rel="noopener">
                          About
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="//support.twitter.com" rel="noopener">
                          Help Center
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="/tos" rel="noopener">
                          Terms
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="/privacy" rel="noopener">
                          Privacy policy
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="//support.twitter.com/articles/20170514" rel="noopener">
                          Cookies
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="//support.twitter.com/articles/20170451" rel="noopener">
                          Ads info
                         </a>
                        </li>
                       </ul>
                      </div>
                     </div>
                    </div>
                   </div>
                  </div>
                 </div>
                </div>
               </div>
              </div>
             </div>
            </div>
           </div>
          </div>
         </div>
         <div class="trends-dialog modal-container" id="trends_dialog">
          <div class="modal draggable">
           <div class="modal-content">
            <button class="modal-btn modal-close js-close" type="button">
             <span class="Icon Icon--close Icon--medium">
              <span class="visuallyhidden">
               Close
              </span>
             </span>
            </button>
            <div class="modal-header">
             <h3 class="modal-title">
              Choose a trend location
             </h3>
            </div>
            <div class="modal-body">
             <div class="trends-dialog-error">
              <p>
              </p>
             </div>
             <div class="trends-wrapper" id="trends_dialog_content">
              <div class="loading">
               <span class="spinner-bigger">
               </span>
              </div>
             </div>
            </div>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="alert-messages hidden" id="message-drawer">
       <div class="message ">
        <div class="message-inside">
         <span class="message-text">
         </span>
         <a class="Icon Icon--close Icon--medium dismiss" href="#" role="button">
          <span class="visuallyhidden">
           Dismiss
          </span>
         </a>
        </div>
       </div>
      </div>
      <div class="gallery-overlay">
      </div>
      <div class="Gallery with-tweet">
       <style class="Gallery-styles">
       </style>
       <div class="Gallery-closeTarget">
       </div>
       <div class="Gallery-content">
        <button class="modal-btn modal-close modal-close-fixed js-close" type="button">
         <span class="Icon Icon--close Icon--large">
          <span class="visuallyhidden">
           Close
          </span>
         </span>
        </button>
        <div class="Gallery-media">
        </div>
        <div class="GalleryNav GalleryNav--prev">
         <span class="GalleryNav-handle GalleryNav-handle--prev">
          <span class="Icon Icon--caretLeft Icon--large">
           <span class="u-hiddenVisually">
            Previous
           </span>
          </span>
         </span>
        </div>
        <div class="GalleryNav GalleryNav--next">
         <span class="GalleryNav-handle GalleryNav-handle--next">
          <span class="Icon Icon--caretRight Icon--large">
           <span class="u-hiddenVisually">
            Next
           </span>
          </span>
         </span>
        </div>
        <div class="GalleryTweet">
        </div>
       </div>
      </div>
      <div class="modal-overlay">
      </div>
      <div id="profile-hover-container">
      </div>
      <div class="modal-container" id="goto-user-dialog">
       <div class="modal modal-small draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Go to a person's profile
          </h3>
         </div>
         <div class="modal-body">
          <div class="modal-inner">
           <form class="t1-form goto-user-form">
            <input aria-label="User" class="input-block username-input" placeholder="Start typing a name to jump to a profile" type="text"/>
            <div class="dropdown-menu typeahead" role="listbox">
             <div aria-hidden="true" class="dropdown-caret">
              <div class="caret-outer">
              </div>
              <div class="caret-inner">
              </div>
             </div>
             <div class="dropdown-inner js-typeahead-results" role="presentation">
              <div class="typeahead-saved-searches" role="presentation">
               <h3 class="typeahead-category-title saved-searches-title" id="saved-searches-heading">
                Saved searches
               </h3>
               <ul class="typeahead-items saved-searches-list" role="presentation">
                <li class="typeahead-item typeahead-saved-search-item" role="presentation">
                 <span aria-hidden="true" class="Icon Icon--close">
                  <span class="visuallyhidden">
                   Remove
                  </span>
                 </span>
                 <a aria-describedby="saved-searches-heading" class="js-nav" data-ds="saved_search" data-query-source="" data-search-query="" href="" role="option" tabindex="-1">
                 </a>
                </li>
               </ul>
              </div>
              <ul class="typeahead-items typeahead-topics" role="presentation">
               <li class="typeahead-item typeahead-topic-item" role="presentation">
                <a class="js-nav" data-ds="topics" data-query-source="typeahead_click" data-search-query="" href="" role="option" tabindex="-1">
                </a>
               </li>
              </ul>
              <ul class="typeahead-items typeahead-accounts social-context js-typeahead-accounts" role="presentation">
               <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                 <div class="js-selectable typeahead-in-conversation hidden">
                  <span class="Icon Icon--follower Icon--small">
                  </span>
                  <span class="typeahead-in-conversation-text">
                   In this conversation
                  </span>
                 </div>
                 <img alt="" class="avatar size32"/>
                 <span class="typeahead-user-item-info account-group">
                  <span class="fullname">
                  </span>
                  <span class="UserBadges">
                   <span class="Icon Icon--verified js-verified hidden">
                    <span class="u-hiddenVisually">
                     Verified account
                    </span>
                   </span>
                   <span class="Icon Icon--protected js-protected hidden">
                    <span class="u-hiddenVisually">
                     Protected Tweets
                    </span>
                   </span>
                  </span>
                  <span class="UserNameBreak">
                  </span>
                  <span class="username u-dir" dir="ltr">
                   @
                   <b>
                   </b>
                  </span>
                 </span>
                 <span class="typeahead-social-context">
                 </span>
                </a>
               </li>
               <li class="js-selectable typeahead-accounts-shortcut js-shortcut" role="presentation">
                <a class="js-nav" data-ds="account_search" data-query-source="typeahead_click" data-search-query="" data-shortcut="true" href="" role="option">
                </a>
               </li>
              </ul>
              <ul class="typeahead-items typeahead-trend-locations-list" role="presentation">
               <li class="typeahead-item typeahead-trend-locations-item" role="presentation">
                <a class="js-nav" data-ds="trend_location" data-search-query="" href="" role="option" tabindex="-1">
                </a>
               </li>
              </ul>
              <div class="typeahead-user-select" role="presentation">
               <div class="typeahead-empty-suggestions" role="presentation">
                Suggested users
               </div>
               <ul class="typeahead-items typeahead-selected js-typeahead-selected" role="presentation">
                <li class="typeahead-item typeahead-selected-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                 <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                  <img alt="" class="avatar size32"/>
                  <span class="typeahead-user-item-info account-group">
                   <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                   </span>
                   <span class="select-status select-disabled Icon Icon--unfollow">
                   </span>
                   <span class="fullname">
                   </span>
                   <span class="UserBadges">
                    <span class="Icon Icon--verified js-verified hidden">
                     <span class="u-hiddenVisually">
                      Verified account
                     </span>
                    </span>
                    <span class="Icon Icon--protected js-protected hidden">
                     <span class="u-hiddenVisually">
                      Protected Tweets
                     </span>
                    </span>
                   </span>
                   <span class="UserNameBreak">
                   </span>
                   <span class="username u-dir" dir="ltr">
                    @
                    <b>
                    </b>
                   </span>
                  </span>
                 </a>
                </li>
                <li class="typeahead-selected-end" role="presentation">
                </li>
               </ul>
               <ul class="typeahead-items typeahead-accounts js-typeahead-accounts" role="presentation">
                <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                 <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                  <img alt="" class="avatar size32"/>
                  <span class="typeahead-user-item-info account-group">
                   <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                   </span>
                   <span class="select-status select-disabled Icon Icon--unfollow">
                   </span>
                   <span class="fullname">
                   </span>
                   <span class="UserBadges">
                    <span class="Icon Icon--verified js-verified hidden">
                     <span class="u-hiddenVisually">
                      Verified account
                     </span>
                    </span>
                    <span class="Icon Icon--protected js-protected hidden">
                     <span class="u-hiddenVisually">
                      Protected Tweets
                     </span>
                    </span>
                   </span>
                   <span class="UserNameBreak">
                   </span>
                   <span class="username u-dir" dir="ltr">
                    @
                    <b>
                    </b>
                   </span>
                  </span>
                 </a>
                </li>
                <li class="typeahead-accounts-end" role="presentation">
                </li>
               </ul>
              </div>
              <div class="typeahead-dm-conversations" role="presentation">
               <ul class="typeahead-items typeahead-dm-conversation-items" role="presentation">
                <li class="typeahead-item typeahead-dm-conversation-item" role="presentation">
                 <a role="option" tabindex="-1">
                 </a>
                </li>
               </ul>
              </div>
             </div>
            </div>
           </form>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="QuickPromoteDialog modal-container" id="quick-promote-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close modal-close-fixed js-close" type="button">
          <span class="Icon Icon--close Icon--large">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Promote this Tweet
          </h3>
         </div>
         <div class="modal-body">
          <div class="quick-promote-view-container">
           <div class="media">
            <iframe class="quick-promote-iframe js-initial-focus" frameborder="0" scrolling="no" src="">
            </iframe>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="block-user-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Block
          </h3>
         </div>
         <div class="tweet-loading">
          <div class="spinner-bigger">
          </div>
         </div>
         <div class="modal-body modal-tweet">
         </div>
         <div class="modal-footer">
          <button class="EdgeButton EdgeButton--tertiary cancel-action js-close">
           Cancel
          </button>
          <button class="EdgeButton EdgeButton--danger block-action">
           Block
          </button>
         </div>
        </div>
       </div>
      </div>
      <div id="geo-disabled-dropdown">
       <div tabindex="-1">
        <div class="dropdown-caret">
         <span class="caret-outer">
         </span>
         <span class="caret-inner">
         </span>
        </div>
        <ul>
         <li class="geo-not-enabled-yet">
          <h2>
           Tweet with a location
          </h2>
          <p>
           You can add location information to your Tweets, such as your city or precise location, from the web and via third-party applications. You always have the option to delete your Tweet location history.
           <a href="http://support.twitter.com/forums/26810/entries/78525" rel="noopener" target="_blank">
            Learn more
           </a>
          </p>
          <div>
           <button class="geo-turn-on EdgeButton EdgeButton--primary" type="button">
            Turn on
           </button>
           <button class="geo-not-now EdgeButton EdgeButton--secondary" type="button">
            Not now
           </button>
          </div>
         </li>
        </ul>
       </div>
      </div>
      <div id="geo-enabled-dropdown">
       <div tabindex="-1">
        <div class="dropdown-caret">
         <span class="caret-outer">
         </span>
         <span class="caret-inner">
         </span>
        </div>
        <div>
         <div class="geo-query-location">
          <input autocomplete="off" class="GeoSearch-queryInput" placeholder="Search for a neighborhood or city" type="text"/>
          <span class="Icon Icon--search">
          </span>
         </div>
         <div class="geo-dropdown-status">
         </div>
         <ul class="GeoSearch-dropdownMenu">
         </ul>
        </div>
       </div>
      </div>
      <div class="modal-container" id="list-membership-dialog">
       <div class="modal modal-small draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Your lists
          </h3>
         </div>
         <div class="modal-body">
          <div class="list-membership-content">
          </div>
          <span class="spinner lists-spinner" title="Loading…">
          </span>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="list-operations-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Create a new list
          </h3>
         </div>
         <div class="modal-body">
          <div class="list-editor">
           <div class="field">
            <label class="t1-label" for="list-name">
             List name
            </label>
            <input class="text" id="list-name" name="name" type="text" value="">
            </input>
           </div>
           <hr>
            <div class="field">
             <label class="t1-label" for="list-description">
              Description
             </label>
             <textarea id="list-description" name="description"></textarea>
             <span class="help-text">
              Under 100 characters, optional
             </span>
            </div>
            <hr/>
            <fieldset class="field">
             <legend class="t1-legend">
              Privacy
             </legend>
             <div class="options">
              <label class="t1-label" for="list-public-radio">
               <input checked="checked" class="radio" id="list-public-radio" name="mode" type="radio" value="public">
                <b>
                 Public
                </b>
                · Anyone can follow this list
               </input>
              </label>
              <label class="t1-label" for="list-private-radio">
               <input class="radio" id="list-private-radio" name="mode" type="radio" value="private">
                <b>
                 Private
                </b>
                · Only you can access this list
               </input>
              </label>
             </div>
            </fieldset>
            <hr/>
            <div class="list-editor-save">
             <button class="EdgeButton EdgeButton--secondary update-list-button" data-list-id="" type="button">
              Save list
             </button>
            </div>
           </hr>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="activity-popup-dialog">
       <div class="modal draggable">
        <div class="modal-content clearfix">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
          </h3>
         </div>
         <div class="modal-body">
          <div class="tweet-loading">
           <div class="spinner-bigger">
           </div>
          </div>
          <div class="activity-popup-dialog-content modal-tweet clearfix">
          </div>
          <div class="loading">
           <span class="spinner-bigger">
           </span>
          </div>
          <div class="activity-popup-dialog-users clearfix">
          </div>
          <div class="activity-popup-dialog-footer">
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="copy-link-to-tweet-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Copy link to Tweet
          </h3>
         </div>
         <div class="modal-body">
          <div class="copy-link-to-tweet-container">
           <label class="t1-label">
            <p class="copy-link-to-tweet-instructions">
             Here's the URL for this Tweet. Copy it to easily share with friends.
            </p>
            <textarea class="link-to-tweet-destination js-initial-focus u-dir" dir="ltr" readonly=""></textarea>
           </label>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="embed-tweet-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title embed-tweet-title">
           Embed this Tweet
          </h3>
          <h3 class="modal-title embed-video-title">
           Embed this Video
          </h3>
         </div>
         <div class="modal-body">
          <div class="embed-code-container">
           <p class="embed-tweet-instructions">
            Add this Tweet to your website by copying the code below.
            <a href="https://dev.twitter.com/web/embedded-tweets" rel="noopener" target="_blank">
             Learn more
            </a>
           </p>
           <p class="embed-video-instructions">
            Add this video to your website by copying the code below.
            <a href="https://dev.twitter.com/web/embedded-tweets" rel="noopener" target="_blank">
             Learn more
            </a>
           </p>
           <form class="t1-form">
            <div class="embed-destination-wrapper">
             <div class="embed-overlay embed-overlay-spinner">
              <div class="embed-overlay-content">
              </div>
             </div>
             <div class="embed-overlay embed-overlay-error">
              <p class="embed-overlay-content">
               Hmm, there was a problem reaching the server.
               <button class="btn-link retry-embed" type="button">
                Try again?
               </button>
              </p>
             </div>
             <textarea class="embed-destination js-initial-focus"></textarea>
             <div class="embed-options">
              <div class="embed-include-parent-tweet">
               <label class="t1-label" for="include-parent-tweet">
                <input checked="" class="include-parent-tweet" id="include-parent-tweet" type="checkbox"/>
                Include parent Tweet
               </label>
              </div>
              <div class="embed-include-card">
               <label class="t1-label" for="include-card">
                <input checked="" class="include-card" id="include-card" type="checkbox"/>
                Include media
               </label>
              </div>
             </div>
            </div>
           </form>
           <p class="embed-tweet-description">
            By embedding Twitter content in your website or app, you are agreeing to the Twitter
            <a href="https://dev.twitter.com/overview/terms/agreement" rel="noopener">
             Developer Agreement
            </a>
            and
            <a href="https://dev.twitter.com/overview/terms/policy" rel="noopener">
             Developer Policy
            </a>
            .
           </p>
           <h3 class="embed-preview-header">
            Preview
           </h3>
           <div class="embed-preview">
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container why-this-ad-dialog" id="why-this-ad-dialog">
       <div class="modal modal-large draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title why-this-ad-title">
           Why you're seeing this ad
          </h3>
         </div>
         <div class="why-this-ad-content">
          <div class="why-this-ad-spinner">
           <div class="spinner-bigger">
           </div>
          </div>
          <iframe aria-hidden="true" class="hidden" id="why-this-ad-frame" scrolling="auto">
          </iframe>
         </div>
        </div>
       </div>
      </div>
      <div class="LoginDialog modal-container u-textCenter" id="login-dialog">
       <div class="modal modal-large draggable">
        <div class="LoginDialog-content modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Log in to Twitter
          </h3>
         </div>
         <div class="LoginDialog-body modal-body">
          <div class="LoginDialog-bird">
           <span class="Icon Icon--bird Icon--large">
           </span>
          </div>
          <div class="LoginDialog-form">
           <form action="https://twitter.com/sessions" class="LoginForm js-front-signin" data-component="dialog" data-element="login" method="post">
            <div class="LoginForm-input LoginForm-username">
             <input autocomplete="username" class="text-input email-input js-signin-email" name="session[username_or_email]" placeholder="Phone, email, or username" type="text">
             </input>
            </div>
            <div class="LoginForm-input LoginForm-password">
             <input autocomplete="current-password" class="text-input" name="session[password]" placeholder="Password" type="password"/>
            </div>
            <div class="LoginForm-rememberForgot">
             <label>
              <input checked="checked" name="remember_me" type="checkbox" value="1"/>
              <span>
               Remember me
              </span>
             </label>
             <span class="separator">
              ·
             </span>
             <a class="forgot" href="/account/begin_password_reset" rel="noopener">
              Forgot password?
             </a>
            </div>
            <input class="EdgeButton EdgeButton--primary EdgeButton--medium submit js-submit" type="submit" value="Log in"/>
            <input name="return_to_ssl" type="hidden" value="true"/>
            <input name="scribe_log" type="hidden"/>
            <input name="redirect_after_login" type="hidden" value="/marswxreport?lang=en"/>
            <input name="authenticity_token" type="hidden" value="127abef84d637ecd5578abab7ac0d383aebbc21a"/>
            <input autocomplete="off" name="ui_metrics" type="hidden"/>
            <script async="" src="/i/js_inst?c_name=ui_metrics">
            </script>
           </form>
          </div>
         </div>
         <div class="LoginDialog-footer modal-footer u-textCenter">
          Don't have an account?
          <a class="LoginDialog-signupLink" href="https://twitter.com/signup" rel="noopener">
           Sign up »
          </a>
         </div>
        </div>
       </div>
      </div>
      <div class="SignupDialog modal-container u-textCenter" id="signup-dialog">
       <div class="modal modal-large draggable">
        <div class="SignupDialog-content modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Sign up for Twitter
          </h3>
         </div>
         <div class="SignupDialog-body modal-body">
          <div class="SignupDialog-icon">
           <span class="Icon Icon--bird Icon--extraLarge">
           </span>
          </div>
          <h2 class="SignupDialog-heading">
           Not on Twitter? Sign up, tune into the things you care about, and get updates as they happen.
          </h2>
          <div class="SignupDialog-form">
           <div class="signup SignupForm ">
            <a class="EdgeButton EdgeButton--large EdgeButton--primary SignupForm-submit u-block js-signup " data-component="dialog" data-element="signup" href="https://twitter.com/signup" role="button">
             Sign up
            </a>
           </div>
          </div>
         </div>
         <div class="SignupDialog-footer modal-footer u-textCenter">
          Have an account?
          <a class="SignupDialog-signinLink" href="/login" rel="noopener">
           Log in »
          </a>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="sms-codes-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Two-way (sending and receiving) short codes:
          </h3>
         </div>
         <div class="modal-body">
          <table cellpadding="0" cellspacing="0" id="sms_codes">
           <thead>
            <tr>
             <th>
              Country
             </th>
             <th>
              Code
             </th>
             <th>
              For customers of
             </th>
            </tr>
           </thead>
           <tbody>
            <tr>
             <td>
              United States
             </td>
             <td>
              40404
             </td>
             <td>
              (any)
             </td>
            </tr>
            <tr>
             <td>
              Canada
             </td>
             <td>
              21212
             </td>
             <td>
              (any)
             </td>
            </tr>
            <tr>
             <td>
              United Kingdom
             </td>
             <td>
              86444
             </td>
             <td>
              Vodafone, Orange, 3, O2
             </td>
            </tr>
            <tr>
             <td>
              Brazil
             </td>
             <td>
              40404
             </td>
             <td>
              Nextel, TIM
             </td>
            </tr>
            <tr>
             <td>
              Haiti
             </td>
             <td>
              40404
             </td>
             <td>
              Digicel, Voila
             </td>
            </tr>
            <tr>
             <td>
              Ireland
             </td>
             <td>
              51210
             </td>
             <td>
              Vodafone, O2
             </td>
            </tr>
            <tr>
             <td>
              India
             </td>
             <td>
              53000
             </td>
             <td>
              Bharti Airtel, Videocon, Reliance
             </td>
            </tr>
            <tr>
             <td>
              Indonesia
             </td>
             <td>
              89887
             </td>
             <td>
              AXIS, 3, Telkomsel, Indosat, XL Axiata
             </td>
            </tr>
            <tr>
             <td rowspan="2">
              Italy
             </td>
             <td>
              4880804
             </td>
             <td>
              Wind
             </td>
            </tr>
            <tr>
             <td>
              3424486444
             </td>
             <td>
              Vodafone
             </td>
            </tr>
           </tbody>
           <tfoot>
            <tr>
             <td colspan="3">
              »
              <a class="js-initial-focus" href="http://support.twitter.com/articles/14226-how-to-find-your-twitter-short-code-or-long-code" rel="noopener" target="_blank">
               See SMS short codes for other countries
              </a>
             </td>
            </tr>
           </tfoot>
          </table>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="leadgen-confirm-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Confirmation
          </h3>
         </div>
         <div class="modal-body">
          <div class="leadgen-card-container">
           <div class="media">
            <iframe class="cards2-promotion-iframe" frameborder="0" scrolling="no" src="">
            </iframe>
           </div>
          </div>
          <div class="js-macaw-cards-iframe-container" data-card-name="promotion">
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="AuthWebViewDialog modal-container" id="auth-webview-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close modal-close-fixed js-close" type="button">
          <span class="Icon Icon--close Icon--large">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
          </h3>
         </div>
         <div class="modal-body">
          <div class="auth-webview-view-container">
           <div class="media">
            <iframe class="auth-webview-card-iframe js-initial-focus" frameborder="0" height="500px" scrolling="no" src="" width="590px">
            </iframe>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="promptbird-modal-prompt">
       <div class="modal">
        <button class="modal-btn js-promptDismiss modal-close js-close" type="button">
         <span class="Icon Icon--close Icon--medium">
          <span class="visuallyhidden">
           Close
          </span>
         </span>
        </button>
        <div class="modal-content">
        </div>
       </div>
      </div>
      <div class="modal-container UIWalkthrough" id="ui-walkthrough-dialog">
       <div class="UIWalkthrough-clickBlocker">
       </div>
       <div class="modal modal-small">
        <div class="UIWalkthrough-caret">
        </div>
        <div class="modal-content">
         <div class="modal-body">
          <div class="UIWalkthrough-header">
           <span class="UIWalkthrough-stepProgress">
           </span>
           <button class="UIWalkthrough-skip js-close">
            Skip all
           </button>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--welcome">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--home UIWalkthrough-icon">
            </span>
            Welcome home!
           </h3>
           <p class="UIWalkthrough-message">
            This timeline is where you’ll spend most of your time, getting instant updates about what matters to you.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--unfollow">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--smileRating1Fill UIWalkthrough-icon">
            </span>
            Tweets not working for you?
           </h3>
           <p class="UIWalkthrough-message">
            Hover over the profile pic and click the Following button to unfollow any account.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--like">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--heart UIWalkthrough-icon">
            </span>
            Say a lot with a little
           </h3>
           <p class="UIWalkthrough-message">
            When you see a Tweet you love, tap the heart — it lets  the person who wrote it know you shared the love.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--retweet">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--retweet UIWalkthrough-icon">
            </span>
            Spread the word
           </h3>
           <p class="UIWalkthrough-message">
            The fastest way to share someone else’s Tweet with your followers is with a Retweet. Tap the icon to send it instantly.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--reply">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--reply UIWalkthrough-icon">
            </span>
            Join the conversation
           </h3>
           <p class="UIWalkthrough-message">
            Add your thoughts about any Tweet with a Reply. Find a topic you’re passionate about, and jump right in.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--trends">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--discover UIWalkthrough-icon">
            </span>
            Learn the latest
           </h3>
           <p class="UIWalkthrough-message">
            Get instant insight into what people are talking about now.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--wtf">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--follow UIWalkthrough-icon">
            </span>
            Get more of what you love
           </h3>
           <p class="UIWalkthrough-message">
            Follow more accounts to get instant updates about topics you care about.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--search">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--search UIWalkthrough-icon">
            </span>
            Find what's happening
           </h3>
           <p class="UIWalkthrough-message">
            See the latest conversations about any topic instantly.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--moments">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--lightning UIWalkthrough-icon">
            </span>
            Never miss a Moment
           </h3>
           <p class="UIWalkthrough-message">
            Catch up instantly on the best stories happening as they unfold.
           </p>
          </div>
         </div>
         <div class="modal-footer">
          <button class="EdgeButton EdgeButton--tertiary u-floatLeft plain-btn UIWalkthrough-button js-previous-step">
           Back
          </button>
          <button class="EdgeButton EdgeButton--secondary UIWalkthrough-button js-next-step js-initial-focus">
           Next
          </button>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="create-custom-timeline-dialog">
      </div>
      <div class="modal-container" id="edit-custom-timeline-dialog">
      </div>
      <div class="modal-container" id="curate-dialog">
      </div>
      <div class="modal-container" id="media-edit-dialog">
      </div>
      <div class="PermalinkOverlay PermalinkOverlay-with-background " id="permalink-overlay">
       <div class="PermalinkProfile-dismiss modal-close-fixed">
        <span class="Icon Icon--close">
        </span>
       </div>
       <button class="PermalinkOverlay-next PermalinkOverlay-button u-posFixed js-next" type="button">
        <span class="Icon Icon--caretLeft Icon--large">
        </span>
        <span class="u-hiddenVisually">
         Next Tweet from user
        </span>
       </button>
       <div class="PermalinkOverlay-modal">
        <div class="PermalinkOverlay-spinnerContainer u-hidden">
         <div class="PermalinkOverlay-spinner">
         </div>
        </div>
        <div class="PermalinkOverlay-content">
         <div class="PermalinkOverlay-body">
         </div>
        </div>
       </div>
      </div>
      <div class="hidden" id="hidden-content">
       <iframe aria-hidden="true" class="tweet-post-iframe" name="tweet-post-iframe">
       </iframe>
       <iframe aria-hidden="true" class="dm-post-iframe" name="dm-post-iframe">
       </iframe>
      </div>
      <input class="json-data" id="init-data" type="hidden" value='{"keyboardShortcuts":[{"name":"Actions","description":"Shortcuts for common actions.","shortcuts":[{"keys":["Enter"],"description":"Open Tweet details"},{"keys":["o"],"description":"Expand photo"},{"keys":["\/"],"description":"Search"}]},{"name":"Navigation","description":"Shortcuts for navigating between items in timelines.","shortcuts":[{"keys":["?"],"description":"This menu"},{"keys":["j"],"description":"Next Tweet"},{"keys":["k"],"description":"Previous Tweet"},{"keys":["Space"],"description":"Page down"},{"keys":["."],"description":"Load new Tweets"}]},{"name":"Timelines","description":"Shortcuts for navigating to different timelines or pages.","shortcuts":[{"keys":["g","u"],"description":"Go to user\u2026"}]}],"baseFoucClass":"swift-loading","bodyFoucClassNames":"swift-loading no-nav-banners","assetsBasePath":"https:\/\/abs.twimg.com\/a\/1527811926\/","assetVersionKey":"969049","emojiAssetsPath":"https:\/\/abs.twimg.com\/emoji\/v2\/72x72\/","environment":"production","formAuthenticityToken":"127abef84d637ecd5578abab7ac0d383aebbc21a","loggedIn":false,"screenName":null,"fullName":null,"userId":null,"guestId":"152798310595391500","createdAt":null,"needsPhoneVerification":false,"allowAdsPersonalization":true,"scribeBufferSize":3,"pageName":"profile","sectionName":"profile","scribeParameters":{},"recaptchaApiUrl":"https:\/\/www.google.com\/recaptcha\/api\/js\/recaptcha_ajax.js","internalReferer":null,"geoEnabled":false,"typeaheadData":{"accounts":{"enabled":true,"localQueriesEnabled":false,"remoteQueriesEnabled":true,"limit":6},"trendLocations":{"enabled":true},"dmConversations":{"enabled":false},"followedSearches":{"enabled":false},"savedSearches":{"enabled":false,"items":[]},"dmAccounts":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":false,"onlyDMable":true},"mediaTagAccounts":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":false,"onlyShowUsersWithCanMediaTag":false,"currentUserId":-1},"selectedUsers":{"enabled":false},"prefillUsers":{"enabled":false},"topics":{"enabled":true,"localQueriesEnabled":false,"remoteQueriesEnabled":true,"prefetchLimit":500,"limit":4},"concierge":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":false,"prefetchLimit":500,"limit":6},"recentSearches":{"enabled":false},"hashtags":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":true,"prefetchLimit":500},"useIndexedDB":false,"showSearchAccountSocialContext":false,"showDebugInfo":false,"useThrottle":true,"accountsOnTop":false,"remoteDebounceInterval":300,"remoteThrottleInterval":300,"tweetContextEnabled":false,"fullNameMatchingInCompose":true,"topicsWithFiltersEnabled":false},"shellReferrer":null,"dm":{"notifications":false,"usePushForNotifications":false,"participant_max":50,"welcome_message_add_to_conversation_enabled":true,"poll_options":{"foreground_poll_interval":3000,"burst_poll_interval":3000,"burst_poll_duration":300000,"max_poll_interval":60000},"card_prefetch":true,"card_prefetch_interval_in_seconds":2000,"dm_quick_reply_options_panel_dismiss_in_ms":2000,"open_dm_enabled":false},"autoplayDisabled":false,"pushStatePageLimit":500000,"routes":{"profile":"\/"},"pushState":true,"viewContainer":"#page-container","href":"\/marswxreport?lang=en","searchPathWithQuery":"\/search?q=query&amp;src=typd","composeAltText":false,"night_mode_activated":false,"user_color":null,"deciders":{"gdprAgeGateDialog":true,"gdprSoftBounceDialog":true,"geo_picker_incident_reset":true,"custom_timeline_curation":false,"native_notifications":true,"disable_ajax_datatype_default_to_text":false,"dm_polling_frequency_in_seconds":3000,"dm_granular_mute_controls":true,"enable_media_tag_prefetch":true,"enableMacawNymizerConversionLanding":false,"hqImageUploads":false,"live_pipeline_consume":true,"mqImageUploads":false,"partnerIdSyncEnabled":true,"sruMediaCategory":true,"photoSruGifLimitMb":15,"promoted_logging_force_post":true,"promoted_video_logging_enabled":true,"pushState":true,"emojiNewCategory":false,"contentEditablePlainTextOnly":false,"web_client_api_stats":false,"web_perftown_stats":true,"web_perftown_ttft":false,"web_client_events_ttft":false,"log_push_state_ttft_metrics":false,"web_sru_stats":false,"web_upload_video":true,"web_upload_video_advanced":false,"upload_video_size":500,"useVmapVariants":false,"autoplayPreviewPreroll":true,"moments_home_module":false,"moments_lohp_enabled":true,"enableNativePush":false,"autoSubscribeNativePush":false,"allowWebPushVapidUpgrade":true,"stickersInteractivity":true,"stickersInteractivityDuringLoading":true,"stickersExperience":true,"dynamic_video_ads_include_long_videos":true,"push_state_size":1000,"live_video_media_control_enabled":false,"cards2_enable_periscope_card_transition":true,"use_api_for_retweet_and_unretweet":false,"use_api_for_follow_and_unfollow":true,"edge_probe_enabled":false,"like_over_http_client":true,"enable_inline_location":true,"enable_tweetstorm_creation":true,"enable_tweetstorm_drafts":false,"enable_tweetstorm_tooltip":true,"text_length_for_tweetstorm_tooltip":50,"dm_report_webview_macaw_swift_enabled":true,"page_title_unread_notification_count":false,"page_title_badge_after_unread_tweets":20},"experiments":{},"toasts_dm":false,"toasts_timeline":false,"toasts_dm_poll_scale":60,"defaultNotificationIcon":"https:\/\/abs.twimg.com\/a\/1527811926\/img\/t1\/mobile\/wp7_app_icon.png","promptbirdData":{"promptbirdEnabled":false,"immediateTriggers":["PullToRefresh","Navigate"],"format":"ProfileOther"},"pageContext":"profile","passwordResetAdvancedLoginForm":true,"skipAutoSignupDialog":false,"shouldReplaceSignupWithLogin":false,"hashflagBaseUrl":"https:\/\/abs.twimg.com\/hashflags\/","activeHashflags":{"growtogether":"GrowTogether_v4\/GrowTogether_v4.png","타노스":"Thanos2018_v3\/Thanos2018_v3.png","infinitygauntlet":"Thanos2018_v3\/Thanos2018_v3.png","beashinboner":"BeAShinboner\/BeAShinboner.png","مسابقة_العربية_للعود":"ArabianOud2018\/ArabianOud2018.png","jurassicworldfallenkingdom":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","bemorepirate":"seaofthieves\/seaofthieves.png","thanos":"Thanos2018_v3\/Thanos2018_v3.png","स्वाभिमान_जुलूस":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","cmtmusicawards":"CMTAwards2018_v2\/CMTAwards2018_v2.png","mymammamia":"MammaMia2_v3\/MammaMia2_v3.png","cabelopantene":"CabeloPanten\/CabeloPanten.png","سديم_عالمي":"digitallabsUAE\/digitallabsUAE.png","incrediblesevent":"incredibles2_v5\/incredibles2_v5.png","justask":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","kathnielforvivo":"Kathniel\/Kathniel.png","blindal":"Deadpool2_BlindAl\/Deadpool2_BlindAl.png","バチェラージャパン":"BachelorJapanS2_v2\/BachelorJapanS2_v2.png","freesmurf":"TNTAnimalKingdomS3\/TNTAnimalKingdomS3.png","abrazodegoles":"ClaroPeru2018\/ClaroPeru2018.png","スクフェスシリーズ5周年":"Klabemoji\/Klabemoji.png","環境の日":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","प्यार_की_जीत":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","wherewereyouinthemorning":"ShawnMendes2018_Flower\/ShawnMendes2018_Flower.png","debatedeldebate":"MXDebates2018\/MXDebates2018.png","teamjurassic":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","debateine":"MXDebates2018\/MXDebates2018.png","heretheycome":"NBA_2017_18_PHI\/NBA_2017_18_PHI.png","frozone":"Frozone\/Frozone.png","츄바카":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","রমজান":"Ramadan2018_Main\/Ramadan2018_Main.png","porcinet":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","okuldışarıdagünü":"DirtIsGood_Persil\/DirtIsGood_Persil.png","desfileorgullo":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","ballparkburger":"BallparkHotDog2018\/BallparkHotDog2018.png","ballparkhotdog":"BallparkHotDog2018\/BallparkHotDog2018.png","에드나모드":"Ednamode_v3\/Ednamode_v3.png","timesup":"TimesUp_v2\/TimesUp_v2.png","thealienist":"TNT-Alienist\/TNT-Alienist.png","labarramaspower":"Entel_Mundial_Peru_v2\/Entel_Mundial_Peru_v2.png","ハンソロ":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","noonlovesmums":"noon_v3\/noon_v3.png","fearthewalkingdead":"FearTWD\/FearTWD.png","eljettadetuvida":"ElJettaDeTuVida\/ElJettaDeTuVida.png","613투표":"KoreanLocalElections2018\/KoreanLocalElections2018.png","totalbedlam":"Deadpool2_Bedlam\/Deadpool2_Bedlam.png","イラストリアス生誕祭":"JapanAzurlane2018_v3\/JapanAzurlane2018_v3.png","イーヨー":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","kaala":"Kaala2018\/Kaala2018.png","프라이드2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","thanosdemandsyoursilence":"Thanos2018_v3\/Thanos2018_v3.png","dirtywater":"redsox2018_v2\/redsox2018_v2.png","suncoastproud":"SuperNetball_SunCoastProud\/SuperNetball_SunCoastProud.png","flickertourlive":"NiallHoran2018\/NiallHoran2018.png","بصمة":"ArabianOud2018\/ArabianOud2018.png","animalkingdomtnt":"TNTAnimalKingdomS3\/TNTAnimalKingdomS3.png","hereditary":"A24_Hereditary2018\/A24_Hereditary2018.png","mntwins":"MinnesotaTwins2018\/MinnesotaTwins2018.png","インクレディブルファミリー":"incredibles2_v5\/incredibles2_v5.png","نصيحة_ناس":"Flynas2018_v2\/Flynas2018_v2.png","pridemonth":"TwitterOpen_Pride2018_PrideMonth\/TwitterOpen_Pride2018_PrideMonth.png","owlmvp":"TmobileOWLMVP\/TmobileOWLMVP.png","プーさん":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","yovotoporque":"MexicoCityElections18\/MexicoCityElections18.png","superflymovie":"SuperflyMovie2018\/SuperflyMovie2018.png","ió":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","infinitywar":"Thanos2018_v3\/Thanos2018_v3.png","dopinder":"Deadpool2_Dopinder\/Deadpool2_Dopinder.png","amoréamor":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","gobolts":"NHL_2017_2018_Lightning_v2\/NHL_2017_2018_Lightning_v2.png","hinchasincondicionales":"MundialMovistar2018\/MundialMovistar2018.png","weareresourcers":"MarqueemployeurVeolia\/MarqueemployeurVeolia.png","vidastarz":"vidaemoji\/vidaemoji.png","beingserena":"SerenaWilliams2018\/SerenaWilliams2018.png","wnba":"WNBALeagueEmoji\/WNBALeagueEmoji.png","juegaméxico":"coronafutbol2018\/coronafutbol2018.png","periscope":"Periscope\/Periscope.png","jurassiclondon":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","dashparr":"incredibles2_v5\/incredibles2_v5.png","gokingsgo":"NHL_2017_2018_LAKings_v2\/NHL_2017_2018_LAKings_v2.png","アズレンtv":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","فانوس":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","chewbacca":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","ifeelprettyfilm":"feelpretty_v2\/feelpretty_v2.png","jbfa":"JamesBeardAwards2018\/JamesBeardAwards2018.png","orgullo":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","testingalbum":"ASAPRocky2018\/ASAPRocky2018.png","violetaparr":"incredibles2_v5\/incredibles2_v5.png","britainsgottalent2018":"BGT2018\/BGT2018.png","bestoftweets":"BestofTweets2018\/BestofTweets2018.png","whatisfly":"SuperflyMovie2018\/SuperflyMovie2018.png","nialllive":"NiallHoran2018\/NiallHoran2018.png","superflylook":"SuperflyMovie2018\/SuperflyMovie2018.png","animalifantastici":"fantasticbeasts_v2\/fantasticbeasts_v2.png","jackjackparr":"JackJack_2\/JackJack_2.png","animauxfantastiques":"fantasticbeasts_v2\/fantasticbeasts_v2.png","真爱无敌":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","rolltide":"Alabama_CFBPlayoff_Teamv3\/Alabama_CFBPlayoff_Teamv3.png","بطل_جنب_بطلة":"HeroNextToHero\/HeroNextToHero.png","lovetwitter":"LoveTwitter\/LoveTwitter.png","mrtvatisina":"aqp2018_v3\/aqp2018_v3.png","суперсемейка2":"incredibles2_v5\/incredibles2_v5.png","firstnations":"IndigenousPeoplesDayCA_2018_v3\/IndigenousPeoplesDayCA_2018_v3.png","endalz":"AlzheimersAssociation2018_v2\/AlzheimersAssociation2018_v2.png","detroitbasketball":"NBA_2017_18_DET\/NBA_2017_18_DET.png","тигруля":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","scotiarewardsyou":"scotiabankswish\/scotiabankswish.png","demuestraquecrees":"CocaColaMXWorldCup2018\/CocaColaMXWorldCup2018.png","rootedinoakland":"OaklandAthletics2018\/OaklandAthletics2018.png","texasrangers":"TexasRangers2018\/TexasRangers2018.png","volvooceanrace":"VolvoOceanRace\/VolvoOceanRace.png","mammamia":"MammaMia2_v3\/MammaMia2_v3.png","cbj":"NHL_2017_2018_BlueJackets_v2\/NHL_2017_2018_BlueJackets_v2.png","piensoyvoto":"MXvoterengagement2018\/MXvoterengagement2018.png","harryandmeghan":"royalwedding2018\/royalwedding2018.png","인크레더블2":"incredibles2_v5\/incredibles2_v5.png","espejopublico":"EspejoPublico_2017_2018\/EspejoPublico_2017_2018.png","骄傲游行":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","badisbred":"TNTAnimalKingdomS3\/TNTAnimalKingdomS3.png","losincreíbles2":"incredibles2_v5\/incredibles2_v5.png","suhurramadan":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","nowwerise":"NHL_2017_2018_NJDevils_v2\/NHL_2017_2018_NJDevils_v2.png","روزنامة_رمضان":"GeneralEntertainmentAuthority2018_v2\/GeneralEntertainmentAuthority2018_v2.png","amazonecho":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","chewie":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","stanleycup":"StanleyCup2018\/StanleyCup2018.png","soloastarwarsstory":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","nba":"NBA_2017_18_NBA\/NBA_2017_18_NBA.png","rockies25th":"ColoradoRockies2018\/ColoradoRockies2018.png","медвежоноквинни":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","nocapes":"Ednamode_v3\/Ednamode_v3.png","billions":"billions-showtime\/billions-showtime.png","bethechange":"BeTheChange_v2\/BeTheChange_v2.png","лэндо":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","canadiandream":"ChevroletCanadianDream2018\/ChevroletCanadianDream2018.png","followtheball":"waltdisneyoscars2018\/waltdisneyoscars2018.png","valla":"FranceBlizzardOWL_LAValiant\/FranceBlizzardOWL_LAValiant.png","teamaxe":"billions-showtime\/billions-showtime.png","افطار":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","tigro":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","statebankofindia":"SBIBank_v3\/SBIBank_v3.png","movietvawards":"MTVMovieAwards2018\/MTVMovieAwards2018.png","출동준비완료":"incredibles2_v5\/incredibles2_v5.png","shieldsup":"FranceBlizzardOWL_LAGladiators\/FranceBlizzardOWL_LAGladiators.png","lafamaviveenti":"movistar\/movistar.png","millenniumfalcon":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","senhorincrível":"MrIncredible\/MrIncredible.png","صقورنا_قدها":"SaudiAirline_2018\/SaudiAirline_2018.png","eleccionescolombia":"colombianelection2018\/colombianelection2018.png","elastigirl":"MrsIncredible\/MrsIncredible.png","infinitystones":"Thanos2018_v3\/Thanos2018_v3.png","goavsgo":"NHL_2017_2018_COAvalanche_v2\/NHL_2017_2018_COAvalanche_v2.png","wannasprite":"q2spriteemoji\/q2spriteemoji.png","somosnuevaraza":"Bancolombia_SomosNuevaRaza\/Bancolombia_SomosNuevaRaza.png","onurhaftası":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","mercwithamouth":"Deadpool2_Deadpool\/Deadpool2_Deadpool.png","labarramáspower":"Entel_Mundial_Peru_v2\/Entel_Mundial_Peru_v2.png","mcdbreakfast":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","7afl":"AFL2018\/AFL2018.png","فوانيس_رمضان":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","amtodmbfn":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","beatplasticpollution":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","bachelorjapan":"BachelorJapanS2_v2\/BachelorJapanS2_v2.png","produitsbio":"FranceFleuryMichon\/FranceFleuryMichon.png","torcidan1":"brahma\/brahma.png","sxswestworld":"Westworld2MidSeason\/Westworld2MidSeason.png","asksweetbitter":"STARZSweetbitter18\/STARZSweetbitter18.png","mammamia2movie":"MammaMia2_v3\/MammaMia2_v3.png","juntosmiami":"MiamiMarlins2018\/MiamiMarlins2018.png","爱就是爱":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","suhour":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","myxmusicawards2018":"MYXMusicAwards2018\/MYXMusicAwards2018.png","ekstracashback":"TokopediaRamadan2018_v2\/TokopediaRamadan2018_v2.png","toystoryland":"waltdisneyoscars2018\/waltdisneyoscars2018.png","onthebus":"NRLTigers2018\/NRLTigers2018.png","allontheline":"SuperNetball_Allontheline\/SuperNetball_Allontheline.png","btsxspotify":"SpotifyBTS2018_v2\/SpotifyBTS2018_v2.png","fallenkingdom":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","onurhaftası2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","613지방선거":"KoreanLocalElections2018\/KoreanLocalElections2018.png","jurassicnight":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","letsgobucs":"PittsburghPirates2018\/PittsburghPirates2018.png","مسابقة_طيران_ناس":"Flynas2018_v2\/Flynas2018_v2.png","اثراء_الرياضة":"ArabLeadersSummit2018_v3\/ArabLeadersSummit2018_v3.png","يوم_البيئة_العالمي":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","фиалкапарр":"incredibles2_v5\/incredibles2_v5.png","seaofthieves":"seaofthieves\/seaofthieves.png","ittakeseverything":"NBA_2017_18_LAC\/NBA_2017_18_LAC.png","shineeisback":"SHINee10thAnniversary_Extension_v2\/SHINee10thAnniversary_Extension_v2.png","journeemondialeenvironnement":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","स्वाभिमान":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","mammamiaherewegoagain":"MammaMia2_v3\/MammaMia2_v3.png","gliincredibili2":"incredibles2_v5\/incredibles2_v5.png","3lionsroar":"WilliamHillWorldCup2018\/WilliamHillWorldCup2018.png","투표인증":"KoreanLocalElections2018\/KoreanLocalElections2018.png","amtodm":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","maythefourth":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","qira":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","bukapuasa":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","estesíesdebate":"MXcitydebate2018\/MXcitydebate2018.png","doitbigger":"NBAPelicans2018\/NBAPelicans2018.png","танос":"Thanos2018_v3\/Thanos2018_v3.png","thematriline":"A24_Hereditary2018\/A24_Hereditary2018.png","اثراء":"ArabLeadersSummit2018_v3\/ArabLeadersSummit2018_v3.png","orgulholgbt":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","aquietplacethailand":"aqp2018_v3\/aqp2018_v3.png","sienteelsabor":"CocaColaMXWorldCup2018\/CocaColaMXWorldCup2018.png","iamopl":"iamopl_v2\/iamopl_v2.png","shocktheworld":"FranceBlizzardOWL_SanFrancisco\/FranceBlizzardOWL_SanFrancisco.png","vidafinale":"vidaemoji\/vidaemoji.png","fearthedeer":"NBA_2017_18_MIL\/NBA_2017_18_MIL.png","am2dmbf":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","thevoiceau":"TheVoiceAU2018\/TheVoiceAU2018.png","mrincreíble":"MrIncredible\/MrIncredible.png","stayquiet":"aqp2018_v3\/aqp2018_v3.png","rêvecanadien":"ChevroletCanadianDream2018\/ChevroletCanadianDream2018.png","ramadan_lanterns":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","itseeyore":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","дэшпарр":"incredibles2_v5\/incredibles2_v5.png","sahur":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","hansolo":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","赤城爆誕祭":"JapanAzurlane2018_v4\/JapanAzurlane2018_v4.png","tictocnews":"bloombergtictoc2018\/bloombergtictoc2018.png","winniepuuh":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","violetparr":"incredibles2_v5\/incredibles2_v5.png","любовьэтолюбовь":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","ramadanekstra":"TokopediaRamadan2018_v2\/TokopediaRamadan2018_v2.png","ガチ勢応援":"GatsbyDeo2018\/GatsbyDeo2018.png","sharkteam":"Sharkteam\/Sharkteam.png","manbooker50":"ManBookerPrize50\/ManBookerPrize50.png","hereditarymovie":"A24_Hereditary2018\/A24_Hereditary2018.png","alômãe":"BrazilWorldCup2018_AloMae_v3\/BrazilWorldCup2018_AloMae_v3.png","amorgana":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","sorrytobotheryou":"SorryToBotherYou2018\/SorryToBotherYou2018.png","amoresamor":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","royalwedding":"royalwedding2018\/royalwedding2018.png","lingkunganhidup":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","kraftbearhugs":"KraftPeanutButterBears_Flight2\/KraftPeanutButterBears_Flight2.png","jurassic":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","beardawards":"JamesBeardAwards2018\/JamesBeardAwards2018.png","supertroopers":"SuperTroopers2\/SuperTroopers2.png","walk2endalz":"AlzheimersAssociation2018_v2\/AlzheimersAssociation2018_v2.png","endalzheimers":"AlzheimersAssociation2018_v2\/AlzheimersAssociation2018_v2.png","sevgikazanır":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","nationaldinoday":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","zeitgeist116":"Deadpool2_Zeitgeist\/Deadpool2_Zeitgeist.png","violettaparr":"incredibles2_v5\/incredibles2_v5.png","piedpiper":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","premiosmtvmiaw":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","aquietplace":"aqp2018_v3\/aqp2018_v3.png","shawnmendesnervous":"ShawnMendes2018_Flower\/ShawnMendes2018_Flower.png","incrediblesday":"incredibles2_v5\/incredibles2_v5.png","knicks":"NBA_2017_18_NYK\/NBA_2017_18_NYK.png","アナザーエデン1周年":"catemoji_v2\/catemoji_v2.png","chaostakescontrol":"westworldpremiere2018\/westworldpremiere2018.png","アズレンタンブラー":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","fantasticbeasts":"fantasticbeasts_v2\/fantasticbeasts_v2.png","प्यार_तो_प्यार_है":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","scratchoftheday":"WilliamHillWorldCup2018\/WilliamHillWorldCup2018.png","bluejays":"TorontoBlueJays2018_v3\/TorontoBlueJays2018_v3.png","مفاجات_وااو":"SAIB\/SAIB.png","thatssuperfly":"SuperflyMovie2018\/SuperflyMovie2018.png","adoptadino":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","winniethepooh":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","mammamiafilm":"MammaMia2_v3\/MammaMia2_v3.png","iaytsa":"tecatemundial_v2\/tecatemundial_v2.png","sansunbruit":"aqp2018_v3\/aqp2018_v3.png","siliconhbo":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","doitbig":"NBA_2017_18_NOP\/NBA_2017_18_NOP.png","prixbestoftweets":"BestofTweets2018\/BestofTweets2018.png","ವಿಶ್ವಪರಿಸರದಿನ":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","ballparkgrillin":"BallparkHotDog2018\/BallparkHotDog2018.png","maythefourthbewithyou":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","debatechilango":"MXcitydebate2018\/MXcitydebate2018.png","landocalrissian":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","finaisnbb":"NBBFinais2018\/NBBFinais2018.png","みんなでシャンシャン5周年":"LoveLiveKlab2018\/LoveLiveKlab2018.png","redv":"NRLRedV2018\/NRLRedV2018.png","прайд2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","sweetbittertv":"STARZSweetbitter18\/STARZSweetbitter18.png","rallytogether":"Cleveland2018\/Cleveland2018.png","mentellall":"TheBachelorette2018\/TheBachelorette2018.png","suhur":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","westworld":"Westworld2MidSeason\/Westworld2MidSeason.png","starwarsday":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","buzzcity":"NBA_2017_18_CHA\/NBA_2017_18_CHA.png","mrindestructible":"MrIncredible\/MrIncredible.png","bostonup":"FranceBlizzardOWL_Boston\/FranceBlizzardOWL_Boston.png","everybodyin":"ChicagoCubs2018\/ChicagoCubs2018.png","snowapp":"snowcorp\/snowcorp.png","bestoftweetsawards":"BestofTweets2018\/BestofTweets2018.png","golalazo":"Golalazo2018\/Golalazo2018.png","avancamos":"BrazillianFederalGov_Avancamos\/BrazillianFederalGov_Avancamos.png","رمضان_كريم":"Ramadan2018_Main\/Ramadan2018_Main.png","indigenouspeoplesday":"IndigenousPeoplesDayCA_2018_v3\/IndigenousPeoplesDayCA_2018_v3.png","รักก็คือรัก":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","rockets":"NBA_2017_18_HOU\/NBA_2017_18_HOU.png","プリコネ":"PriconneRedive2018\/PriconneRedive2018.png","myincrediblesreview":"incredibles2_v5\/incredibles2_v5.png","diadomeioambiente":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","gotitfrommymom":"A24_Hereditary2018\/A24_Hereditary2018.png","tonicollette":"A24_Hereditary2018\/A24_Hereditary2018.png","bgt2018":"BGT2018\/BGT2018.png","flynas":"Flynas2018_v2\/Flynas2018_v2.png","фреон":"Frozone\/Frozone.png","прайдпарад":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","jurassicpark":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","kandil":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","dominomf":"Deadpool2_Domino\/Deadpool2_Domino.png","이요르":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","위니더푸":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","koreanelection":"KoreanLocalElections2018\/KoreanLocalElections2018.png","dodgers":"LADodgers2018\/LADodgers2018.png","avançamos":"BrazillianFederalGov_Avancamos\/BrazillianFederalGov_Avancamos.png","faisonsgrandirlebio":"FranceFleuryMichon\/FranceFleuryMichon.png","wpgwhiteout":"NHL_2017_2018_Jets_v2\/NHL_2017_2018_Jets_v2.png","aquietplaceinmy":"aqp2018_v3\/aqp2018_v3.png","violetteparr":"incredibles2_v5\/incredibles2_v5.png","iftarramadan":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","shinee10thanniversary":"SHINee10thAnniversary_Extension_v2\/SHINee10thAnniversary_Extension_v2.png","cable":"Deadpool2_Cable\/Deadpool2_Cable.png","onepursuit":"WashingtonNationals2018\/WashingtonNationals2018.png","wearegeelong":"WeAreGeelong_v2\/WeAreGeelong_v2.png","proudibmer":"IBMThink2018_extension\/IBMThink2018_extension.png","wethenorth":"NBA_2017_18_TOR\/NBA_2017_18_TOR.png","nationaldinosaurday":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","ih-oh":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","sbinews":"SBIBank_v3\/SBIBank_v3.png","deadpool2":"Deadpool2_Deadpool\/Deadpool2_Deadpool.png","lafamaviveenmi":"movistar\/movistar.png","happymammasday":"MammaMia2_v3\/MammaMia2_v3.png","lvcruise":"LouisVuittonFashionShow_May28_v2\/LouisVuittonFashionShow_May28_v2.png","mammamiamovie":"MammaMia2_v3\/MammaMia2_v3.png","halamadrid":"realmadrid\/realmadrid.png","ڤيمتو":"Vimto2018\/Vimto2018.png","gorabbitohs":"NRLsouths2018\/NRLsouths2018.png","gospursgo":"NBA_2017_18_SAS\/NBA_2017_18_SAS.png","سحور_رمضان":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","إفطار_رمضان":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","чубакка":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","dubnation":"NBA_2017_18_GSW\/NBA_2017_18_GSW.png","beautyinai":"HuaweiHonorQ2GlobalLaunch_v2\/HuaweiHonorQ2GlobalLaunch_v2.png","والله_مسامحين":"AlmaraiRamadan2018\/AlmaraiRamadan2018.png","برنامج_أصيل":"SAIB\/SAIB.png","lovewins":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","starwars":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","takenote":"NBA_2017_18_UTA\/NBA_2017_18_UTA.png","generationdbacks":"ArizonaDBacks_v2\/ArizonaDBacks_v2.png","niallhoranlive":"NiallHoran2018\/NiallHoran2018.png","summergrilling":"BallparkHotDog2018\/BallparkHotDog2018.png","sweetbitterstarz":"STARZSweetbitter18\/STARZSweetbitter18.png","puasa":"Ramadan2018_Main\/Ramadan2018_Main.png","ifeelprettymovie":"feelpretty_v2\/feelpretty_v2.png","кира":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","쇼미더기프트":"ShowMeTheGift2018_v2\/ShowMeTheGift2018_v2.png","juntossomos10":"MastercardSoccer\/MastercardSoccer.png","ジャックジャック":"JackJack_2\/JackJack_2.png","juegamexico":"coronafutbol2018\/coronafutbol2018.png","negasonicteenagewarhead":"Deadpool2_Negasonic\/Deadpool2_Negasonic.png","afl":"AFL18\/AFL18.png","チューバッカ":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","pdomjnate":"FranceBlizzardOWL_Philadelphia\/FranceBlizzardOWL_Philadelphia.png","افطارا_شهيا":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","크리스토퍼로빈과곰돌이푸":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","espiglet":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","pimpi":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","iftar_ramadan":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","thedynastybegins":"FranceBlizzardOWL_Seoul\/FranceBlizzardOWL_Seoul.png","asapforever":"ASAPRocky2018\/ASAPRocky2018.png","hiljainenpaikka":"aqp2018_v3\/aqp2018_v3.png","díamundialdelmedioambiente":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","zezé":"JackJack_2\/JackJack_2.png","ifeelpretty":"feelpretty_v2\/feelpretty_v2.png","ngabuburit":"Ramadan2018_Main\/Ramadan2018_Main.png","nowruz":"nowruz2018_v4\/nowruz2018_v4.png","vidalia":"vidaemoji\/vidaemoji.png","cgb41":"AsahiGroupFoods\/AsahiGroupFoods.png","pacers":"NBA_2017_18_IND\/NBA_2017_18_IND.png","dinosaurday":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","mexicanelection":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","برنامج_وااو":"SAIB\/SAIB.png","デレステ":"ImagscgStage2018\/ImagscgStage2018.png","tigrou":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","thisismycrew":"MilwaukeeBrewers2018\/MilwaukeeBrewers2018.png","cmtawards2018":"CMTAwards2018_v2\/CMTAwards2018_v2.png","shatterstar":"Deadpool2_Shatterstar\/Deadpool2_Shatterstar.png","teampeter":"Deadpool2_PeterW\/Deadpool2_PeterW.png","कालाकरिकालन":"Kaala2018\/Kaala2018.png","contigoperú":"MundialMovistar2018\/MundialMovistar2018.png","فطور":"Ramadan2018_Iftar_fix\/Ramadan2018_Iftar_fix.png","tagderumwelt":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","codyboys":"TNTAnimalKingdomS3\/TNTAnimalKingdomS3.png","eeyore":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","프로존":"Frozone\/Frozone.png","whateverittakes":"NBA_2017_18_CLE_v2\/NBA_2017_18_CLE_v2.png","blackanda":"BETAwards2018\/BETAwards2018.png","askvida":"vidaemoji\/vidaemoji.png","solostarwars":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","shinee_thestoryoflight":"SHINee10thAnniversary_Extension_v2\/SHINee10thAnniversary_Extension_v2.png","govixens":"SuperNetball_GoVixens\/SuperNetball_GoVixens.png","ariaster":"A24_Hereditary2018\/A24_Hereditary2018.png","mytwitteranniversary":"MyTwitterAnniversary\/MyTwitterAnniversary.png","askalexa":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","thrunthru":"NRLtitans2018\/NRLtitans2018.png","pride2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","statebank":"SBIBank_v3\/SBIBank_v3.png","diamundialdomeioambiente":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","eleccionchilanga":"MexicoCityElections18\/MexicoCityElections18.png","thisisjustatest":"ASAPRocky2018\/ASAPRocky2018.png","iaah":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","ogprofilepic":"lastOG_v2\/lastOG_v2.png","nbbnotwitter":"Emoji_NBB_2017_2018\/Emoji_NBB_2017_2018.png","forvida":"vidaemoji\/vidaemoji.png","betawards2018":"BETAwards2018\/BETAwards2018.png","marvelfansunited":"Thanos2018_v3\/Thanos2018_v3.png","yaytza":"tecatemundial_v2\/tecatemundial_v2.png","hatsoff4heroes":"TMobile_HatsOff4Heroes\/TMobile_HatsOff4Heroes.png","cheddarlive":"Cheddar_Emoji_v4\/Cheddar_Emoji_v4.png","ferkel":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","프라이드퍼레이드":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","prideparade":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","hatsoffforheroes":"TMobile_HatsOff4Heroes\/TMobile_HatsOff4Heroes.png","フロゾン":"Frozone\/Frozone.png","エドナ":"Ednamode_v3\/Ednamode_v3.png","mnwild":"NHL_2017_2018_MNwild_v2\/NHL_2017_2018_MNwild_v2.png","ティガー":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","peterw":"Deadpool2_PeterW\/Deadpool2_PeterW.png","turtlerat":"capitolonemarchmadness\/capitolonemarchmadness.png","métis":"IndigenousPeoplesDayCA_2018_v3\/IndigenousPeoplesDayCA_2018_v3.png","letsmarchnova":"VillanovaYearLong\/VillanovaYearLong.png","alomae":"BrazilWorldCup2018_AloMae_v3\/BrazilWorldCup2018_AloMae_v3.png","haloson":"haloson\/haloson.png","綾鷹ほうじ茶":"cocacolaAyataka3\/cocacolaAyataka3.png","프라이드":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","letsgoducks":"NHL_2017_2018_Ducks_v2\/NHL_2017_2018_Ducks_v2.png","hinchaincondicional":"MundialMovistar2018\/MundialMovistar2018.png","fortheloveofhotdogs":"OscarMayer_Weinermobile\/OscarMayer_Weinermobile.png","tecnomobile":"TranssionTecno2018\/TranssionTecno2018.png","スターウォーズ":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","realmadrid":"realmadrid\/realmadrid.png","காலா":"Kaala2018\/Kaala2018.png","hansolostarwars":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","रमजान":"Ramadan2018_Main\/Ramadan2018_Main.png","ランドカルリジアン":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","whitetina":"vidaemoji\/vidaemoji.png","spotifyloveyourself":"SpotifyBTS2018_v2\/SpotifyBTS2018_v2.png","motog6":"MotorolaG62018\/MotorolaG62018.png","vivoxkathniel":"Kathniel\/Kathniel.png","dirtyfrida":"vidaemoji\/vidaemoji.png","джекджек":"JackJack_2\/JackJack_2.png","orgullo2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","noonwomen":"noon_v3\/noon_v3.png","tvoshortdoc":"TVOShortDocs\/TVOShortDocs.png","rg18":"FrenchOpen2018\/FrenchOpen2018.png","itspiglet":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","weflyasone":"weflyasone_v2\/weflyasone_v2.png","loveislove":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","familyoftheyear":"ArrestedDevelopment2018\/ArrestedDevelopment2018.png","allforone":"NBA_2017_18_CLE\/NBA_2017_18_CLE.png","flyeaglesfly":"Eaglesv4\/Eaglesv4.png","violetapêra":"incredibles2_v5\/incredibles2_v5.png","티거":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","نون_للمرأة":"noon_v3\/noon_v3.png","20cents":"REDEmoji2018\/REDEmoji2018.png","umlugarsilencioso":"aqp2018_v3\/aqp2018_v3.png","ftwd":"FearTWD\/FearTWD.png","잭잭":"JackJack_2\/JackJack_2.png","vungdatcamlang":"aqp2018_v3\/aqp2018_v3.png","미스터인크레더블":"MrIncredible\/MrIncredible.png","613투표했어요":"KoreanLocalElections2018\/KoreanLocalElections2018.png","alienisttnt":"TNT-Alienist\/TNT-Alienist.png","myogprofilepic":"lastOG_v2\/lastOG_v2.png","イラスティガール":"MrsIncredible\/MrsIncredible.png","lallavedelmundial":"ClaroCAM\/ClaroCAM.png","westworldhbo":"Westworld2MidSeason\/Westworld2MidSeason.png","espooh":"ChristopherRobin_ItsPooh2018\/ChristopherRobin_ItsPooh2018.png","mangerbio":"FranceFleuryMichon\/FranceFleuryMichon.png","orgullo18":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","mcdonaldsmorning":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","netneutrality":"Net_Emoji_v3\/Net_Emoji_v3.png","battleswon":"USMC2018_V2\/USMC2018_V2.png","кристоферробин":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","wheresbaz":"TNTAnimalKingdomS3\/TNTAnimalKingdomS3.png","thealienisttnt":"TNT-Alienist\/TNT-Alienist.png","yonobysbi":"SBIBank_v3\/SBIBank_v3.png","paradadoorgulho":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","breakfastatmcdonalds":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","स्वाभिमान_2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","613투표하세요":"KoreanLocalElections2018\/KoreanLocalElections2018.png","綾鷹":"cocacolaAyataka3\/cocacolaAyataka3.png","amtodmbf":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","llavemundialista":"ClaroCAM\/ClaroCAM.png","yaytsa":"tecatemundial_v2\/tecatemundial_v2.png","internetpower":"Entel_Mundial_Peru_v2\/Entel_Mundial_Peru_v2.png","mtvmiaw18":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","orgullgai2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","supertroopers420":"SuperTroopers2\/SuperTroopers2.png","מקוםשקט":"aqp2018_v3\/aqp2018_v3.png","schinnonordestão":"SchinNordestao2018\/SchinNordestao2018.png","frenchopen":"FrenchOpen2018\/FrenchOpen2018.png","whitehot":"NBAHeat2018\/NBAHeat2018.png","プリ米":"PriconneRedive2018\/PriconneRedive2018.png","cichemiejsce":"aqp2018_v3\/aqp2018_v3.png","makeamericabluthagain":"ArrestedDevelopment2018\/ArrestedDevelopment2018.png","любовьпобеждает":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","osincríveis2":"incredibles2_v5\/incredibles2_v5.png","お茶にしましょう綾鷹":"cocacolaAyataka3\/cocacolaAyataka3.png","sacramentoproud":"NBA_2017_18_SAC\/NBA_2017_18_SAC.png","thunderup":"NBA_2017_18_OKC\/NBA_2017_18_OKC.png","nbatwitter":"NBATwitter_Emoji___v4\/NBATwitter_Emoji___v4.png","gelado":"Frozone\/Frozone.png","アズールレーン":"JapanAzurlane2018_v4\/JapanAzurlane2018_v4.png","upupcronulla":"NRLsharks2018\/NRLsharks2018.png","inplaywithray":"bet365RayWinstone_v2\/bet365RayWinstone_v2.png","weltumwelttag":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","dcfamily":"NBA_2017_18_WAS\/NBA_2017_18_WAS.png","bebold":"PhiladelphiaPhillies2018\/PhiladelphiaPhillies2018.png","tvoshortdocs":"TVOShortDocs\/TVOShortDocs.png","نون_صديق_الأم":"noon_v3\/noon_v3.png","flyfridays":"SuperflyMovie2018\/SuperflyMovie2018.png","torcedorfanatico":"RexonaWorldCupEmoji\/RexonaWorldCupEmoji.png","ピグレット":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","billionspremiere":"billions-showtime\/billions-showtime.png","prixbestoftweet":"BestofTweets2018\/BestofTweets2018.png","flashparr":"incredibles2_v5\/incredibles2_v5.png","wadewilson":"Deadpool2_Deadpool\/Deadpool2_Deadpool.png","outdoorclassroomday":"DirtIsGood_Persil\/DirtIsGood_Persil.png","sessizbiryer":"aqp2018_v3\/aqp2018_v3.png","celtics":"NBA_2017_18_BOS\/NBA_2017_18_BOS.png","twdxfeartwd":"FearTWD\/FearTWD.png","بطله_جنب_بطل":"HeroNextToHero_v2\/HeroNextToHero_v2.png","echoindia":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","jamesbeard":"JamesBeardAwards2018\/JamesBeardAwards2018.png","骄傲":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","philaunite":"NBASixers2018\/NBASixers2018.png","standwithus":"NHL_2017_2018_Preds_v2\/NHL_2017_2018_Preds_v2.png","diadeaprenderbrincando":"DirtIsGood_Persil\/DirtIsGood_Persil.png","ekstraflashsale":"TokopediaRamadan2018_v2\/TokopediaRamadan2018_v2.png","осликушастик":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","votamexico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","مركز_الملك_عبدالعزيز_الثقافي":"ArabLeadersSummit2018_v3\/ArabLeadersSummit2018_v3.png","billionsfinale":"billions-showtime\/billions-showtime.png","прайд":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","pilasconelvoto":"colombianelection2018\/colombianelection2018.png","bobparr":"MrIncredible\/MrIncredible.png","orgullgai":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","tigger":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","ogtracy":"ogtracy\/ogtracy.png","begiant":"GWSGIANTS\/GWSGIANTS.png","bourriquet":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","サノス":"Thanos2018_v3\/Thanos2018_v3.png","sweetbitter":"STARZSweetbitter18\/STARZSweetbitter18.png","wcclassics":"WilliamHillWorldCup2018\/WilliamHillWorldCup2018.png","melbourneproud":"NRLmelbourne2018\/NRLmelbourne2018.png","siberius":"Frozone\/Frozone.png","mtvawards":"MTVMovieAwards2018\/MTVMovieAwards2018.png","mtvmiaw2018":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","mffl":"NBA_2017_18_DAL\/NBA_2017_18_DAL.png","sweetbitterpremiere":"STARZSweetbitter18\/STARZSweetbitter18.png","فطور_رمضان":"Ramadan2018_Iftar_fix\/Ramadan2018_Iftar_fix.png","vidapremiere":"vidaemoji\/vidaemoji.png","freshevents":"freshevents2018Q2\/freshevents2018Q2.png","lamamámáspower":"Entel_Mundial_Peru_v2\/Entel_Mundial_Peru_v2.png","leitão":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","paradadoorgulholgbt":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","wakandaweekend":"BlackPantherHomeEnt2018\/BlackPantherHomeEnt2018.png","lamorguanya":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","takjil":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","lesindestructibles2":"incredibles2_v5\/incredibles2_v5.png","sfgiants":"SFGiants2018\/SFGiants2018.png","incondicionales":"MundialMovistar2018\/MundialMovistar2018.png","directorx":"SuperflyMovie2018\/SuperflyMovie2018.png","am2dm":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","骄傲2018":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","showmethegift":"ShowMeTheGift2018_v2\/ShowMeTheGift2018_v2.png","earntomorrow":"NHL_2017_2018_PhillyFlyers_v2\/NHL_2017_2018_PhillyFlyers_v2.png","whatblackpanthermeanstome":"BlackPantherHomeEnt2018\/BlackPantherHomeEnt2018.png","todoestáporver":"vodafone2018\/vodafone2018.png","shinee":"SHINee10thAnniversary_Extension_v2\/SHINee10thAnniversary_Extension_v2.png","elecciones2018":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","ramazan":"Ramadan2018_Main\/Ramadan2018_Main.png","bachelornation":"TheBachelorette2018\/TheBachelorette2018.png","wnbatakesastand":"WNBATakesAStand3\/WNBATakesAStand3.png","surlechemindubio":"FranceFleuryMichon\/FranceFleuryMichon.png","suhoor":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","tuiteratura":"FeriaDelHilo\/FeriaDelHilo.png","burnblue":"FranceBlizzardOWL_Dallas\/FranceBlizzardOWL_Dallas.png","uclfinal":"ChampionsLeagueFinal2018\/ChampionsLeagueFinal2018.png","gotgrit":"SuperNetball_gotgrit\/SuperNetball_gotgrit.png","iamfirebird":"SuperNetball_IAMFIREBIRD\/SuperNetball_IAMFIREBIRD.png","soychilangoyosivoto":"MexicoCityElections18\/MexicoCityElections18.png","grindcity":"NBA_2017_18_MEM\/NBA_2017_18_MEM.png","فوانيس":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","igór":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","sliceline":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","kurma":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","ramadan_lantern":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","redscountry":"CincinnatiReds2018\/CincinnatiReds2018.png","sincontaminación":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","votolibre":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","mrincredible":"MrIncredible\/MrIncredible.png","プリコネ無料10連ガチャ":"PriconneRedive2018\/PriconneRedive2018.png","superflysoundtrack":"SuperflyMovie2018\/SuperflyMovie2018.png","flechapêra":"incredibles2_v5\/incredibles2_v5.png","loveyourselfxspotify":"SpotifyBTS2018_v2\/SpotifyBTS2018_v2.png","votebluth":"ArrestedDevelopment2018\/ArrestedDevelopment2018.png","satanicgrandma":"A24_Hereditary2018\/A24_Hereditary2018.png","cmtawards":"CMTAwards2018_v2\/CMTAwards2018_v2.png","jurassicjune":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","thelastog":"lastOG_v2\/lastOG_v2.png","3elieve":"NHL_2017_2018_Penguins_v2\/NHL_2017_2018_Penguins_v2.png","jurassicpark25":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","ontariovotes":"OntarioElection2018\/OntarioElection2018.png","cmtawards18":"CMTAwards2018_v2\/CMTAwards2018_v2.png","mrインクレディブル":"MrIncredible\/MrIncredible.png","siliconvalleyhbo":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","listospara":"CocaColaMXWorldCup2018\/CocaColaMXWorldCup2018.png","13の理由":"NetflixJapan_13ReasonsWHy\/NetflixJapan_13ReasonsWHy.png","ramadanlanterns":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","푸":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","gotiges":"gotiges\/gotiges.png","thesecondcoming":"Deadpool2_Deadpool\/Deadpool2_Deadpool.png","journeemondialedelenvironnement":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","journéemondialedelenvironnement":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","эднамод":"Ednamode_v3\/Ednamode_v3.png","mamamia2":"MammaMia2_v3\/MammaMia2_v3.png","estigger":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","askanobel":"askanobel\/askanobel.png","ridemcowboys":"NRLcowboys2018_v2\/NRLcowboys2018_v2.png","mcdonaldsbreakfast":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","طيب_الله_فالك":"ArabianOud2018\/ArabianOud2018.png","letsgonewarriors":"LetsGoneWarriors_v2\/LetsGoneWarriors_v2.png","betawards18":"BETAwards2018\/BETAwards2018.png","ramadan":"Ramadan2018_Main\/Ramadan2018_Main.png","flexweave":"reebokflexweave_v2\/reebokflexweave_v2.png","myincredibles2review":"incredibles2_v5\/incredibles2_v5.png","mulherelástica":"MrsIncredible\/MrsIncredible.png","mcdmorning":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","colombiadecide":"colombianelection2018\/colombianelection2018.png","피글렛":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","journéemondialeenvironnement":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","eatlikeapro":"EatLikeAPro2018V2\/EatLikeAPro2018V2.png","truetoatlanta":"NBA_2017_18_ATL\/NBA_2017_18_ATL.png","goldenbuzzer":"BGT2018\/BGT2018.png","الخطوط_توديك_روسيا":"SaudiAirline_2018\/SaudiAirline_2018.png","schinnonordestao":"SchinNordestao2018\/SchinNordestao2018.png","harilingkungan":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","bgt":"BGT2018\/BGT2018.png","thedarkorder":"Thanos2018_v3\/Thanos2018_v3.png","한솔로":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","unpostotranquillo":"aqp2018_v3\/aqp2018_v3.png","christopherrobin":"ChristopherRobin_ChristopherRobinfix\/ChristopherRobin_ChristopherRobinfix.png","lamamamaspower":"Entel_Mundial_Peru_v2\/Entel_Mundial_Peru_v2.png","키라":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","winnielourson":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","luckydomino":"Deadpool2_Domino\/Deadpool2_Domino.png","marchforourlives":"marchforourlives\/marchforourlives.png","sjsharks":"NHL_2017_2018_SJSharks_v2\/NHL_2017_2018_SJSharks_v2.png","vivov9kathniel":"Kathniel\/Kathniel.png","rusianosharáhéroes":"tecatemundial_v2\/tecatemundial_v2.png","onuryürüyüşü":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","theincredibles":"incredibles2_v5\/incredibles2_v5.png","teamchuck":"billions-showtime\/billions-showtime.png","sunsat50":"NBA_2017_18_PHX\/NBA_2017_18_PHX.png","okuldisaridagunu":"DirtIsGood_Persil\/DirtIsGood_Persil.png","일라스티걸":"MrsIncredible\/MrsIncredible.png","jurassicworld":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","thebachelorette":"TheBachelorette2018\/TheBachelorette2018.png","esigor":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","shareyourmeal":"ShareYourMeal2018\/ShareYourMeal2018.png","アズレン傘":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","motog6play":"MotorolaG62018\/MotorolaG62018.png","famaabailar":"movistar\/movistar.png","debatecapital":"MXcitydebate2018\/MXcitydebate2018.png","お茶にしましょう":"cocacolaAyataka3\/cocacolaAyataka3.png","chopon":"atlantabraves2018\/atlantabraves2018.png","تحدي_الروزنامة":"GeneralEntertainmentAuthority2018_v2\/GeneralEntertainmentAuthority2018_v2.png","feriadehilos":"FeriaDelHilo\/FeriaDelHilo.png","سوا_لقدام":"HeroNextToHero\/HeroNextToHero.png","ibmer":"IBMThink2018_extension\/IBMThink2018_extension.png","stateofdecay2":"StateofDecay2\/StateofDecay2.png","liketobeyou":"ShawnMendes2018_Flower\/ShawnMendes2018_Flower.png","amazonfindsaway":"JurassicWorld_FallenKingdom_AmazonFindsAWay\/JurassicWorld_FallenKingdom_AmazonFindsAWay.png","qlder":"StateofOriginAU_2018_QLDER\/StateofOriginAU_2018_QLDER.png","lafamaviveenmí":"movistar\/movistar.png","asaprocky":"ASAPRocky2018\/ASAPRocky2018.png","nyxl":"FranceBlizzardOWL_NY\/FranceBlizzardOWL_NY.png","masterchefbr":"MasterChefBR2018\/MasterChefBR2018.png","فطور\"فطور_رمضان":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","خلنا_نجتمع":"Vimto2018\/Vimto2018.png","mmas2018":"MYXMusicAwards2018\/MYXMusicAwards2018.png","nuevojetta":"ElJettaDeTuVida\/ElJettaDeTuVida.png","バチェラー見てる人と語りたい":"BachelorJapanS2_v2\/BachelorJapanS2_v2.png","proudtobeabulldog":"NRLbulldogs2018\/NRLbulldogs2018.png","freshempire":"freshevents2018Q2\/freshevents2018Q2.png","alomãe":"BrazilWorldCup2018_AloMae_v3\/BrazilWorldCup2018_AloMae_v3.png","megustaquevotes":"MXvoterengagement2018\/MXvoterengagement2018.png","koreanelection2018":"KoreanLocalElections2018\/KoreanLocalElections2018.png","فيمتو":"Vimto2018\/Vimto2018.png","abrazosdegol":"ClaroPeru2018\/ClaroPeru2018.png","эластика":"MrsIncredible\/MrsIncredible.png","igor":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","gatsbyロールオン":"GatsbyDeo2018\/GatsbyDeo2018.png","hammerseries":"HammerSeries2018\/HammerSeries2018.png","heforshe":"HeForShe_fixed\/HeForShe_fixed.png","サノスは沈黙を求める":"Thanos2018_v3\/Thanos2018_v3.png","proudlysydney":"sydneyswans\/sydneyswans.png","askbtsxspotify":"SpotifyBTS2018_v2\/SpotifyBTS2018_v2.png","alômae":"BrazilWorldCup2018_AloMae_v3\/BrazilWorldCup2018_AloMae_v3.png","綾鷹茶葉のあまみ":"cocacolaAyataka3\/cocacolaAyataka3.png","theonlywayisessex":"TOWIE\/TOWIE.png","hereweare":"HereWeAre_v3\/HereWeAre_v3.png","heatculture":"NBA_2017_18_MIA\/NBA_2017_18_MIA.png","ligadia":"LigaDia_Emoji_v2\/LigaDia_Emoji_v2.png","tracymorgan":"ogtracy\/ogtracy.png","uptheante":"FranceBlizzardOWL_Houston\/FranceBlizzardOWL_Houston.png","البنك_السعودي_للاستثمار":"SAIB\/SAIB.png","vimto":"Vimto2018\/Vimto2018.png","helloyou":"MotorolaG62018\/MotorolaG62018.png","twd":"FearTWD\/FearTWD.png","ガチ勢の日":"GatsbyDeo2018\/GatsbyDeo2018.png","クリーム玄米ブラン":"AsahiGroupFoods\/AsahiGroupFoods.png","روزنامة_الترفيه":"GeneralEntertainmentAuthority2018_v2\/GeneralEntertainmentAuthority2018_v2.png","incrediblespremiere":"incredibles2_v5\/incredibles2_v5.png","jointhehuddle":"AFLWestCoast\/AFLWestCoast.png","lasuertenojuega":"La_Suerte_No_Juega_v2\/La_Suerte_No_Juega_v2.png","샤이니_데리러가":"SHINee10thAnniversary_Extension_v2\/SHINee10thAnniversary_Extension_v2.png","jeanchristopheetwinnie":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","قدومك_يسعدن":"GeneralEntertainmentAuthority2018_v2\/GeneralEntertainmentAuthority2018_v2.png","strengthinnumbers":"NBA_2017_18_GSW_v2\/NBA_2017_18_GSW_v2.png","welcometowestworld":"Westworld2MidSeason\/Westworld2MidSeason.png","donthesash":"EssendonFC\/EssendonFC.png","whywewearblack":"TimesUp_v2\/TimesUp_v2.png","spotifyxbts":"SpotifyBTS2018_v2\/SpotifyBTS2018_v2.png","eleccionesmexico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","lgm":"NYMets2018\/NYMets2018.png","alienist":"TNT-Alienist\/TNT-Alienist.png","blackandaforever":"BETAwards2018\/BETAwards2018.png","helenparr":"MrsIncredible\/MrsIncredible.png","тихемісце":"aqp2018_v3\/aqp2018_v3.png","عطر_أبيات":"ArabianOud2018\/ArabianOud2018.png","aquietplaceid":"aqp2018_v3\/aqp2018_v3.png","walkonminks":"SuperflyMovie2018\/SuperflyMovie2018.png","showyouremotions":"laysshowyouremotions\/laysshowyouremotions.png","indigenoushistorymonth":"IndigenousPeoplesDayCA_2018_v3\/IndigenousPeoplesDayCA_2018_v3.png","snozberries":"SuperTroopers2\/SuperTroopers2.png","thealamode":"capitolonemarchmadness\/capitolonemarchmadness.png","heronexttohero":"HeroNextToHero\/HeroNextToHero.png","threelions":"ThreeLions2018\/ThreeLions2018.png","اثراء_رمضان":"ArabLeadersSummit2018_v3\/ArabLeadersSummit2018_v3.png","女のバトル":"BachelorJapanS2_v2\/BachelorJapanS2_v2.png","افطار_رمضان":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","هي_وحدة":"Vimto2018\/Vimto2018.png","simplyamazing":"NissanESLeaf2018\/NissanESLeaf2018.png","metis":"IndigenousPeoplesDayCA_2018_v3\/IndigenousPeoplesDayCA_2018_v3.png","colossus":"Deadpool2_Colossus\/Deadpool2_Colossus.png","unlugartranquilo":"aqp2018_v3\/aqp2018_v3.png","キーラ":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","unlugarensilencio":"aqp2018_v3\/aqp2018_v3.png","ناس":"Flynas2018_v2\/Flynas2018_v2.png","wakandaforever":"BlackPantherHomeEnt2018\/BlackPantherHomeEnt2018.png","نوروز":"nowruz2018_v4\/nowruz2018_v4.png","ファンタビ":"fantasticbeasts_v2\/fantasticbeasts_v2.png","onlywayisessex":"TOWIE\/TOWIE.png","bringthemayhem":"FranceBlizzardOWL_Florida\/FranceBlizzardOWL_Florida.png","aşkaşktır":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","nhlbruins":"NHL_2017_2018_NHLBruins_v4\/NHL_2017_2018_NHLBruins_v4.png","ednamoda":"Ednamode_v3\/Ednamode_v3.png","iftar":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","blackhistorymonth":"BlackHistoryMonth\/BlackHistoryMonth.png","velvetyvoice":"capitolonemarchmadness\/capitolonemarchmadness.png","クリストファーロビン":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","superflymusic":"SuperflyMovie2018\/SuperflyMovie2018.png","رمضان":"Ramadan2018_Main\/Ramadan2018_Main.png","electrifytheworld":"NissanESLeaf2018\/NissanESLeaf2018.png","joguejunto":"BrazilWorldCup_JogueJunto_v3\/BrazilWorldCup_JogueJunto_v3.png","adoptadinosaur":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","vegasborn":"NHL_2017_2018_VegasKnights_v3\/NHL_2017_2018_VegasKnights_v3.png","vivov9malltour":"Kathniel\/Kathniel.png","metoo":"MeToo_v3\/MeToo_v3.png","negasonic":"Deadpool2_Negasonic\/Deadpool2_Negasonic.png","desfiledelorgullo":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","thebachelorettefinale":"TheBachelorette2018\/TheBachelorette2018.png","wemetontwitter":"WeMetOnt_Emoji\/WeMetOnt_Emoji.png","colombia2018":"colombianelection2018\/colombianelection2018.png","jackjack":"JackJack_2\/JackJack_2.png","maythe4thbewithyou":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","0427ガチ全滅":"Thanos2018_v3\/Thanos2018_v3.png","hazmatch":"colombianelection2018\/colombianelection2018.png","赤城":"JapanAzurlane2018_v4\/JapanAzurlane2018_v4.png","kathnielforvivov9":"Kathniel\/Kathniel.png","niallhoranflicker":"NiallHoran2018\/NiallHoran2018.png","bestoftweet":"BestofTweets2018\/BestofTweets2018.png","jw2":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","ramadanlantern":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","puuh":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","arresteddevelopment":"ArrestedDevelopment2018\/ArrestedDevelopment2018.png","accesomundialista":"ClaroCAM\/ClaroCAM.png","itspooh":"ChristopherRobin_ItsPooh2018\/ChristopherRobin_ItsPooh2018.png","inmyblood":"ShawnMendes2018_Flower\/ShawnMendes2018_Flower.png","feelpretty":"feelpretty_v2\/feelpretty_v2.png","قدومك_يسعدنا":"GeneralEntertainmentAuthority2018_v2\/GeneralEntertainmentAuthority2018_v2.png","westworlds2":"Westworld2MidSeason\/Westworld2MidSeason.png","deadpool":"Deadpool2_Deadpool\/Deadpool2_Deadpool.png","animaisfantasticos":"fantasticbeasts_v2\/fantasticbeasts_v2.png","bulanpuasa":"Ramadan2018_Main\/Ramadan2018_Main.png","greatestseasonever":"FlonaseQ1_v2\/FlonaseQ1_v2.png","wearemanly":"NRLmanly2018\/NRLmanly2018.png","イラストリアス":"JapanAzurlane2018_v3\/JapanAzurlane2018_v3.png","wegohard":"NBA_2017_18_BKLYN\/NBA_2017_18_BKLYN.png","shareacoke":"ShareACoke2018\/ShareACoke2018.png","jp25":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","supertroopers2":"SuperTroopers2\/SuperTroopers2.png","atfr":"TheBachelorette2018\/TheBachelorette2018.png","тихоеместо":"aqp2018_v3\/aqp2018_v3.png","신비한동물사전":"fantasticbeasts_v2\/fantasticbeasts_v2.png","neversettle":"Astros2018\/Astros2018.png","콰이어트플레이스":"aqp2018_v3\/aqp2018_v3.png","solomovie":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","ibm":"IBMThink2018_extension\/IBMThink2018_extension.png","デッドプール":"deadpooljapan18_v2\/deadpooljapan18_v2.png","sbi":"SBIBank_v3\/SBIBank_v3.png","bhm":"BlackHistoryMonth\/BlackHistoryMonth.png","capitalstb":"GlobalCapitalSummertimeBall2018\/GlobalCapitalSummertimeBall2018.png","masterchef":"spainmasterchef\/spainmasterchef.png","くまのプーさん":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","cusrise":"NBACeltics2018\/NBACeltics2018.png","eleccionesméxico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","flècheparr":"incredibles2_v5\/incredibles2_v5.png","звёздныевойны":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","mcdsbreakfast":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","إفطارًا_شهيًا":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","newmotog":"MotorolaG62018\/MotorolaG62018.png","dinoday":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","esigór":"ChristopherRobin_Eeyore2018\/ChristopherRobin_Eeyore2018.png","betawards":"BETAwards2018\/BETAwards2018.png","بطاقة_السفر":"SAIB\/SAIB.png","royalwedding2018":"royalwedding2018\/royalwedding2018.png","championsleaguefinal":"ChampionsLeagueFinal2018\/ChampionsLeagueFinal2018.png","bullsnation":"NBA_2017_18_CHI\/NBA_2017_18_CHI.png","orgull":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","nrl":"NRL2018\/NRL2018.png","jepa":"DirtIsGood_Persil\/DirtIsGood_Persil.png","fanantonio":"capitolonemarchmadness\/capitolonemarchmadness.png","랜도":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","بطلة_جنب_بطل":"HeroNextToHero\/HeroNextToHero.png","mammamia2":"MammaMia2_v3\/MammaMia2_v3.png","2018지방선거":"KoreanLocalElections2018\/KoreanLocalElections2018.png","britainsgottalent":"BGT2018\/BGT2018.png","marchedesfiertés":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","worldenvironmentday":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","herecomethegiants":"SuperNetball_HereComeTheGiants\/SuperNetball_HereComeTheGiants.png","المستقبل_هو":"noon_v3\/noon_v3.png","feartwd":"FearTWD\/FearTWD.png","jurassicworld2":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","blacklivesmatter":"BlackHistoryMonth\/BlackHistoryMonth.png","shawnmendesthealbumoutnow":"ShawnMendes2018_Flower2\/ShawnMendes2018_Flower2.png","ad5":"ArrestedDevelopment2018\/ArrestedDevelopment2018.png","pinkcarpetmtvmiaw":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","shawnmendesthealbum":"ShawnMendes2018_Flower2\/ShawnMendes2018_Flower2.png","breyersdelights":"impossiblepossiblebreyers\/impossiblepossiblebreyers.png","pooh":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","fightingforglory":"FranceBlizzardOWL_Shanghai\/FranceBlizzardOWL_Shanghai.png","jurassicworldnight":"JurassicWorld_FallenKingdom_DinoDay_v2\/JurassicWorld_FallenKingdom_DinoDay_v2.png","westworldseason2":"Westworld2MidSeason\/Westworld2MidSeason.png","feriadelhilo":"FeriaDelHilo\/FeriaDelHilo.png","diamundialdelmedioambiente":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","العربية_للعود":"ArabianOud2018\/ArabianOud2018.png","allcaps":"NHL_2017_2018_Caps_v2\/NHL_2017_2018_Caps_v2.png","eaststowin":"NRLRoosters2018\/NRLRoosters2018.png","dünyaçevregünü":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","darkorder":"Thanos2018_v3\/Thanos2018_v3.png","haypower":"PoweradeMXWorldCup\/PoweradeMXWorldCup.png","oamorvence":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","tigrão":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png","milehighbasketball":"NBA_2017_18_DEN_v2\/NBA_2017_18_DEN_v2.png","إفطار":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","serenawilliams":"SerenaWilliams2018\/SerenaWilliams2018.png","threemuskamigos":"capitolonemarchmadness\/capitolonemarchmadness.png","pride":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","bronxnation":"NRLBroncos2018\/NRLBroncos2018.png","votaméxico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","supersuit":"Frozone\/Frozone.png","animalesfantásticos":"fantasticbeasts_v2\/fantasticbeasts_v2.png","onpoli":"OntarioElection2018\/OntarioElection2018.png","hilanderos":"FeriaDelHilo\/FeriaDelHilo.png","flackoseason":"ASAPRocky2018\/ASAPRocky2018.png","inuit":"IndigenousPeoplesDayCA_2018_v3\/IndigenousPeoplesDayCA_2018_v3.png","suerteono":"La_Suerte_No_Juega_v2\/La_Suerte_No_Juega_v2.png","hangnélkül":"aqp2018_v3\/aqp2018_v3.png","ithra":"ArabLeadersSummit2018_v3\/ArabLeadersSummit2018_v3.png","mtvaward":"MTVMovieAwards2018\/MTVMovieAwards2018.png","رمضان_مبارك":"Ramadan2018_Main\/Ramadan2018_Main.png","хрюня":"ChristopherRobin_Piglet2018\/ChristopherRobin_Piglet2018.png","puremagic":"NBA_2017_18_ORL\/NBA_2017_18_ORL.png","세계환경의날":"WorldEnvironmentDay2018_Korean\/WorldEnvironmentDay2018_Korean.png","كامل_الأوصاف":"NewChanganCar2018\/NewChanganCar2018.png","biobox":"FranceFleuryMichon\/FranceFleuryMichon.png","porvida":"vidaemoji\/vidaemoji.png","letsgopadres":"SDPadres2018\/SDPadres2018.png","バチェラー":"BachelorJapanS2_v2\/BachelorJapanS2_v2.png","incredibles2":"incredibles2_v5\/incredibles2_v5.png","thelastogtbs":"lastOG_v2\/lastOG_v2.png","噤界":"aqp2018_v3\/aqp2018_v3.png","ripcity":"NBA_2017_18_POR\/NBA_2017_18_POR.png","detroitsummers":"DetroitTigers2018\/DetroitTigers2018.png","mrincredibile":"MrIncredible\/MrIncredible.png","frozono":"Frozone\/Frozone.png","스타워즈":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","jamesbeardawards":"JamesBeardAwards2018\/JamesBeardAwards2018.png","lakeshow":"NBA_2017_18_LAL\/NBA_2017_18_LAL.png","giornatamondialedellambiente":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","fastestfeet":"reebokflexweave_v2\/reebokflexweave_v2.png","malibugames":"MalibuGamesSummer2018\/MalibuGamesSummer2018.png","onelxn":"OntarioElection2018\/OntarioElection2018.png","ittakesobsession":"TranssionTecno2018\/TranssionTecno2018.png","kohlscashsweepstakes":"kohlscash2v2\/kohlscash2v2.png","estamosenlachampions":"NissanUCL2018\/NissanUCL2018.png","cmtaward":"CMTAwards2018_v2\/CMTAwards2018_v2.png","sheinspiresme":"HereWeAre_v3\/HereWeAre_v3.png","винни":"ChristopherRobin_Pooh2018\/ChristopherRobin_Pooh2018.png","discoverwestworld":"Westworld2MidSeason\/Westworld2MidSeason.png","madetofly":"SuperNetball_MadetoFly\/SuperNetball_MadetoFly.png","アズレングッズ":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","divebartour":"BLDiveBar_v2\/BLDiveBar_v2.png","gonswswifts":"SuperNetball_GoNSWSwifts\/SuperNetball_GoNSWSwifts.png","howwillyousurvive":"StateofDecay2_HowWillYouSurvive\/StateofDecay2_HowWillYouSurvive.png","mrsincredible":"MrsIncredible\/MrsIncredible.png","torcedorfanático":"RexonaWorldCupEmoji\/RexonaWorldCupEmoji.png","కాలా":"Kaala2018\/Kaala2018.png","snowcam":"snowcorp\/snowcorp.png","lastog":"lastOG_v2\/lastOG_v2.png","电影寂静之地":"aqp2018_v3\/aqp2018_v3.png","boundbyblue":"AFLBoundbyBlue\/AFLBoundbyBlue.png","matriline":"A24_Hereditary2018\/A24_Hereditary2018.png","سحور":"Ramadan2018_Iftar_v2\/Ramadan2018_Iftar_v2.png","impossiblepossible":"impossiblepossiblebreyers\/impossiblepossiblebreyers.png","विश्वपर्यावरणदिवस":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","mcgriddles":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","lifefindsaway":"Jurassic_World_emoji_v3\/Jurassic_World_emoji_v3.png","هيئة_الترفيه":"GeneralEntertainmentAuthority2018_v2\/GeneralEntertainmentAuthority2018_v2.png","tmltalk":"NHL_2017_2018_MapleLeafs_v2\/NHL_2017_2018_MapleLeafs_v2.png","vidachallenge":"vidaemoji\/vidaemoji.png","nissanleaf":"NissanESLeaf2018\/NissanESLeaf2018.png","2018투표하세요":"KoreanLocalElections2018\/KoreanLocalElections2018.png","raisedroyal":"kcroyals2018\/kcroyals2018.png","クリーム玄米ブラン総選挙":"AsahiGroupFoods\/AsahiGroupFoods.png","nbafinals":"NBAFinals2018\/NBAFinals2018.png","raysup":"TampaBayRays2018\/TampaBayRays2018.png","weareraiders":"NRLraiders2018\/NRLraiders2018.png","maythe4th":"StarWarsSolo_Chewie_v2\/StarWarsSolo_Chewie_v2.png","بطل_جنب_بطله":"HeroNextToHero_v2\/HeroNextToHero_v2.png","uptheblues":"StateofOriginAU_2018_uptheblues\/StateofOriginAU_2018_uptheblues.png","truetotheblue":"SeattleMariners2018\/SeattleMariners2018.png","ednamode":"Ednamode_v3\/Ednamode_v3.png","amorésamor":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","superfly":"SuperflyMovie2018\/SuperflyMovie2018.png","honor10":"HuaweiHonorQ2GlobalLaunch_v2\/HuaweiHonorQ2GlobalLaunch_v2.png","فانوس_رمضان":"Ramadan2018_Lantern_v2\/Ramadan2018_Lantern_v2.png","pipercoin":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","towie":"TOWIE\/TOWIE.png","lando":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","хансоло":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","bestneverrest":"MercedesGermany_BestNeverRest\/MercedesGermany_BestNeverRest.png","aceshigh":"FranceBlizzardOWL_London\/FranceBlizzardOWL_London.png","persiannewyear":"nowruz2018_v4\/nowruz2018_v4.png","stlcards":"StLouisCardinals2018\/StLouisCardinals2018.png","itscominghome":"WilliamHillWorldCup2018\/WilliamHillWorldCup2018.png","satanicgrandmas":"A24_Hereditary2018\/A24_Hereditary2018.png","nbb":"Emoji_NBB_2017_2018\/Emoji_NBB_2017_2018.png","фантастическиетвари":"fantasticbeasts_v2\/fantasticbeasts_v2.png","世界環境デー":"WorldEnvironmentDay2018\/WorldEnvironmentDay2018.png","elamorgana":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","rolandgarros":"FrenchOpen2018\/FrenchOpen2018.png","whitesox":"whitesox2018\/whitesox2018.png","webringthunder":"SuperNetball_webringthunder\/SuperNetball_webringthunder.png","myvimto":"Vimto2018\/Vimto2018.png","yourodds":"WilliamHillWorldCup2018\/WilliamHillWorldCup2018.png","birdland":"orioles2018_v2\/orioles2018_v2.png","アナザーエデン":"catemoji_v2\/catemoji_v2.png","pinstripepride":"NYYankees2018\/NYYankees2018.png","86aids":"REDEmoji2018\/REDEmoji2018.png","hilanderas":"FeriaDelHilo\/FeriaDelHilo.png","طيران_ناس":"Flynas2018_v2\/Flynas2018_v2.png","giveusthealbumflacko":"ASAPRocky2018\/ASAPRocky2018.png","lostinjapan":"ShawnMendes2018_Flower\/ShawnMendes2018_Flower.png","todoestaporver":"vodafone2018\/vodafone2018.png","studentsstandup":"Parkland_Extension\/Parkland_Extension.png","testinginprogress":"ASAPRocky2018\/ASAPRocky2018.png","espejopúblico":"EspejoPublico_2017_2018\/EspejoPublico_2017_2018.png","thehaloway":"LAAngels2018\/LAAngels2018.png","axenolollabr":"AxeLollapalooza\/AxeLollapalooza.png","あなたの思いをそのまま聞かせて":"Adsforgood_Japan2018_v2\/Adsforgood_Japan2018_v2.png","dieunglaublichen2":"incredibles2_v5\/incredibles2_v5.png","ความรักชนะ":"TwitterOpen_Pride2018\/TwitterOpen_Pride2018.png","alleyesnorth":"NBA_2017_18_MIN\/NBA_2017_18_MIN.png","ramadhan":"Ramadan2018_Main\/Ramadan2018_Main.png","мистерисключительный":"MrIncredible\/MrIncredible.png","itstigger":"ChristopherRobin_Tigger2018\/ChristopherRobin_Tigger2018.png"},"profile_user":{"id":786939553,"id_str":"786939553","name":"Mars Weather","screen_name":"MarsWxReport","location":"Gale Crater, Mars","url":"http:\/\/mars.nasa.gov\/msl\/mission\/instruments\/environsensors\/rems\/","description":"Updates as avail from the REMS weather instrument aboard @MarsCuriosity.  Data credit: Centro deAstrobiologia, FMI, JPL\/NASA, Not an official acct.","protected":false,"followers_count":39885,"friends_count":53,"listed_count":301,"created_at":"Tue Aug 28 12:48:50 +0000 2012","favourites_count":196,"utc_offset":null,"time_zone":null,"geo_enabled":true,"verified":false,"statuses_count":1455,"lang":"en","contributors_enabled":false,"is_translator":false,"is_translation_enabled":false,"profile_background_color":"C0DEED","profile_background_image_url":"http:\/\/abs.twimg.com\/images\/themes\/theme1\/bg.png","profile_background_image_url_https":"https:\/\/abs.twimg.com\/images\/themes\/theme1\/bg.png","profile_background_tile":false,"profile_image_url":"http:\/\/pbs.twimg.com\/profile_images\/2552209293\/220px-Mars_atmosphere_normal.jpg","profile_image_url_https":"https:\/\/pbs.twimg.com\/profile_images\/2552209293\/220px-Mars_atmosphere_normal.jpg","profile_banner_url":"https:\/\/pbs.twimg.com\/profile_banners\/786939553\/1403835009","profile_link_color":"0084B4","profile_sidebar_border_color":"FFFFFF","profile_sidebar_fill_color":"DDEEF6","profile_text_color":"333333","profile_use_background_image":true,"has_extended_profile":false,"default_profile":false,"default_profile_image":false,"following":null,"follow_request_sent":null,"notifications":null,"business_profile_state":"none","translator_type":"none"},"profileEditingCSSBundle":"https:\/\/abs.twimg.com\/a\/1527811926\/css\/t1\/twitter_profile_editing.bundle.css","profile_id":786939553,"business_profile":false,"b2c_logged_out_support_indicators_enabled":true,"business_profile_featured_collections_complete":false,"cardsGallery":true,"injectComposedTweets":false,"inlineProfileEditing":false,"gdprSoftBounceEnabled":false,"isClusterFollowReplenishEnabled":false,"autoplayEnabled":true,"periscopeLiveStatusPollInterval":15000,"trendsCacheKey":null,"decider_personalized_trends":false,"trendsEndpoint":"\/i\/trends","wtfOptions":{"pc":true,"connections":true,"limit":3,"display_location":"profile-sidebar","dismissable":true,"similar_to_user_id":"786939553"},"showSensitiveContent":false,"autoPlayBalloonsAnimation":false,"momentsNuxTooltipsEnabled":false,"isCurrentUser":false,"isSensitiveProfile":false,"timeline_url":"\/i\/profiles\/show\/MarsWxReport\/timeline\/tweets","initialState":{"title":"Mars Weather (@MarsWxReport) | Twitter","section":null,"module":"app\/pages\/profile\/highline_landing","cache_ttl":300,"body_class_names":"three-col logged-out user-style-MarsWxReport enhanced-mini-profile ProfilePage ProfilePage--withWarning","doc_class_names":"route-profile","route_name":"profile","page_container_class_names":"AppContent","ttft_navigation":false}}'/>
      <input class="swift-boot-module" type="hidden" value="app/pages/profile/highline_landing"/>
      <input id="swift-module-path" type="hidden" value="https://abs.twimg.com/k/swift/en"/>
      <script async="" src="https://abs.twimg.com/k/en/init.en.ae62202c2e7a8c3978db.js">
      </script>
     </body>
    </html>
    
    


```python
#get the weather from the newest tweet
mars_weather = soup.find(class_='tweet-text').get_text()
mars_weather
```




    'Saturn’s planet-sized moon Titan, its encircling atmosphere backlit by the Sun, as seen 12 years ago today. Details: https://go.nasa.gov/2HadMcO\xa0 #SaturnSaturdaypic.twitter.com/zeVCa1N2vd'



### Mars Facts


```python
#Mars space facts url
facts_url = 'https://space-facts.com/mars/'

#use Pandas to scrape the planet profile
profile = pd.read_html(facts_url)
profile               
```




    [                      0                              1
     0  Equatorial Diameter:                       6,792 km
     1       Polar Diameter:                       6,752 km
     2                 Mass:  6.42 x 10^23 kg (10.7% Earth)
     3                Moons:            2 (Phobos & Deimos)
     4       Orbit Distance:       227,943,824 km (1.52 AU)
     5         Orbit Period:           687 days (1.9 years)
     6  Surface Temperature:                  -153 to 20 °C
     7         First Record:              2nd millennium BC
     8          Recorded By:           Egyptian astronomers]




```python
#make a df
profile_df = profile[0]

#set index to the 0 column
profile_df.set_index(0, inplace=True)

#delete the index name
profile_df.index.names = [None]

#delete the column name
profile_df.columns = ['']

profile_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Equatorial Diameter:</th>
      <td>6,792 km</td>
    </tr>
    <tr>
      <th>Polar Diameter:</th>
      <td>6,752 km</td>
    </tr>
    <tr>
      <th>Mass:</th>
      <td>6.42 x 10^23 kg (10.7% Earth)</td>
    </tr>
    <tr>
      <th>Moons:</th>
      <td>2 (Phobos &amp; Deimos)</td>
    </tr>
    <tr>
      <th>Orbit Distance:</th>
      <td>227,943,824 km (1.52 AU)</td>
    </tr>
    <tr>
      <th>Orbit Period:</th>
      <td>687 days (1.9 years)</td>
    </tr>
    <tr>
      <th>Surface Temperature:</th>
      <td>-153 to 20 °C</td>
    </tr>
    <tr>
      <th>First Record:</th>
      <td>2nd millennium BC</td>
    </tr>
    <tr>
      <th>Recorded By:</th>
      <td>Egyptian astronomers</td>
    </tr>
  </tbody>
</table>
</div>




```python
#convert the data to a HTML table string
html_table = profile_df.to_html()

#clean it up
html_table = html_table.replace('\n', '')

html_table
```




    '<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th></th>    </tr>  </thead>  <tbody>    <tr>      <th>Equatorial Diameter:</th>      <td>6,792 km</td>    </tr>    <tr>      <th>Polar Diameter:</th>      <td>6,752 km</td>    </tr>    <tr>      <th>Mass:</th>      <td>6.42 x 10^23 kg (10.7% Earth)</td>    </tr>    <tr>      <th>Moons:</th>      <td>2 (Phobos &amp; Deimos)</td>    </tr>    <tr>      <th>Orbit Distance:</th>      <td>227,943,824 km (1.52 AU)</td>    </tr>    <tr>      <th>Orbit Period:</th>      <td>687 days (1.9 years)</td>    </tr>    <tr>      <th>Surface Temperature:</th>      <td>-153 to 20 °C</td>    </tr>    <tr>      <th>First Record:</th>      <td>2nd millennium BC</td>    </tr>    <tr>      <th>Recorded By:</th>      <td>Egyptian astronomers</td>    </tr>  </tbody></table>'



### Mars Hemispheres


```python
#visit the USGS Astrogeology site here to obtain high resolution images for each of Mar's hemispheres

#USGS url
usgs_url = 'https://astrogeology.usgs.gov/search/results?q=hemisphere+enhanced&k1=target&v1=Mars'

#visit
browser.visit(usgs_url)

#create BeautifulSoup object and parse
soup = BeautifulSoup(browser.html, 'html.parser')
```


```python
print(soup.prettify())

```

    <!DOCTYPE html>
    <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
     <head>
      <link href="//ajax.googleapis.com/ajax/libs/jqueryui/1.11.3/themes/smoothness/jquery-ui.css" rel="stylesheet" type="text/css"/>
      <script async="" src="https://ssl.google-analytics.com/ga.js" type="text/javascript">
      </script>
      <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js" type="text/javascript">
      </script>
      <title>
       Astropedia Search Results | USGS Astrogeology Science Center
      </title>
      <meta content="USGS Astrogeology Science Center Astropedia search results." name="description"/>
      <meta content="USGS,Astrogeology Science Center,Cartography,Geology,Space,Geological Survey,Mapping" name="keywords"/>
      <meta content="IE=edge" http-equiv="X-UA-Compatible"/>
      <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
      <meta content="width=device-width, initial-scale=1, maximum-scale=1" name="viewport"/>
      <meta content="x61hXXVj7wtfBSNOPnTftajMsZ5yB2W-qRoyr7GtOKM" name="google-site-verification"/>
      <!--<link rel="stylesheet" href="http://fonts.googleapis.com/css?family=Open+Sans:400italic,400,bold"/>-->
      <link href="/css/main.css" media="screen" rel="stylesheet"/>
      <link href="/css/print.css" media="print" rel="stylesheet"/>
      <!--[if lt IE 9]>
    			<script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
    			<script src="/js/respond.min.js"></script>
    			<link rel="stylesheet" type="text/css" href="/css/ie.css"/>
                            <script>
                              document.createElement('header');
                              document.createElement('nav');
                              document.createElement('section');
                              document.createElement('article');
                              document.createElement('aside');
                              document.createElement('footer');
                              document.createElement('hgroup');
                            </script>
                      <![endif]-->
      <link href="/favicon.ico" rel="icon" type="image/x-ico"/>
     </head>
     <body id="results">
      <header>
       <h1>
        Astrogeology Science Center
       </h1>
       <a href="http://www.usgs.gov">
        <img alt="USGS: Science for a Changing World" class="logo" height="70" src="/images/usgs_logo_main_2x.png" width="180"/>
       </a>
      </header>
      <div class="wrapper">
       <nav>
        <a href="#" id="nav-toggle" title="Navigation Menu">
         Menu
        </a>
        <ul class="dropdown dropdown-horizontal" id="yw0">
         <li>
          <a href="/">
           Home
          </a>
         </li>
         <li>
          <a href="/about">
           About
          </a>
          <ul>
           <li>
            <a href="/about/careers">
             Careers
            </a>
           </li>
           <li>
            <a href="/contact">
             Contact
            </a>
           </li>
           <li>
            <a href="/about/events">
             Events
            </a>
           </li>
           <li>
            <a href="/site/glossary">
             Glossary
            </a>
           </li>
           <li>
            <a href="/about/mission">
             Mission
            </a>
           </li>
           <li>
            <a href="/news">
             News
            </a>
           </li>
           <li>
            <a href="/people">
             People
            </a>
           </li>
           <li>
            <a href="/about/using-our-images">
             Using Our Images
            </a>
           </li>
           <li>
            <a href="/about/visitors">
             Visitors
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/facilities">
           Labs / Facilities
          </a>
          <ul>
           <li>
            <a href="/facilities/flynn-creek-crater-sample-collection">
             Flynn Creek Crater Sample Collection
            </a>
           </li>
           <li>
            <a href="http://www.moon-cal.org">
             Lunar Calibration Project
            </a>
           </li>
           <li>
            <a href="/facilities/meteor-crater-sample-collection">
             Meteor Crater Sample Collection
            </a>
           </li>
           <li>
            <a href="/facilities/mrctr">
             MRCTR GIS Lab
            </a>
           </li>
           <li>
            <a href="/facilities/cartography-and-imaging-sciences-node-of-nasa-planetary-data-system">
             PDS Cartography and Imaging Sciences Node
            </a>
           </li>
           <li>
            <a href="/pds/annex">
             PDS IMG Annex
            </a>
           </li>
           <li>
            <a href="/facilities/photogrammetry-guest-facility">
             Photogrammetry Guest Facility
            </a>
           </li>
           <li>
            <a href="/rpif">
             Regional Planetary Information Facility (RPIF)
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/maps">
           Maps / Products
          </a>
          <ul>
           <li>
            <a href="/search">
             Product Search
            </a>
           </li>
           <li>
            <a href="http://planetarynames.wr.usgs.gov">
             Gazetteer of Planetary Nomenclature
            </a>
           </li>
           <li>
            <a href="http://planetarymapping.wr.usgs.gov">
             Geologic Mapping Program
            </a>
           </li>
           <li>
            <a href="http://pilot.wr.usgs.gov">
             Planetary Image Locator Tool (PILOT)
            </a>
           </li>
           <li>
            <a href="/search/planetary-index">
             Planetary Map Index
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/geology">
           Missions / Research
          </a>
          <ul>
           <li>
            <a href="/geology/mars-dunes">
             Mars Dunes
            </a>
           </li>
           <li>
            <a href="/geology/mars-ice">
             Mars Ice
            </a>
           </li>
           <li>
            <a href="/missions">
             Mission Support
            </a>
           </li>
           <li>
            <a href="/solar-system">
             Solar System
            </a>
           </li>
           <li>
            <a href="/groups">
             Working Groups
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/tools">
           Tools
          </a>
          <ul>
           <li>
            <a href="http://planetarynames.wr.usgs.gov">
             Gazetteer of Planetary Nomenclature
            </a>
           </li>
           <li>
            <a href="http://isis.astrogeology.usgs.gov">
             Integrated Software for Imagers and Spectrometers (ISIS)
            </a>
           </li>
           <li>
            <a href="http://astrogeology.usgs.gov/tools/map-a-planet-2">
             Map a Planet 2
            </a>
           </li>
           <li>
            <a href="http://pilot.wr.usgs.gov">
             Planetary Image Locator Tool (PILOT)
            </a>
           </li>
           <li>
            <a href="http://astrocloud.wr.usgs.gov/">
             Projection on the Web (POW)
            </a>
           </li>
          </ul>
         </li>
        </ul>
        <form action="/search/results" class="search" id="search" method="get">
         <input title="Search Astropedia" type="submit" value=""/>
         <input name="q" placeholder="Search" type="text"/>
         <input name="__ncforminfo" type="hidden" value="j_yMAIBTscKr8tI7tkjLqUwOBIFefc4oD8utdC0-YLWhUsZRB32VKTKdw0Pigogf9H9Kd99PYQXBmlk0D3yi8qzShdZzxccf5mE9c4dt5q4="/>
        </form>
       </nav>
       <div class="container">
        <form action="/search/results" class="bar widget block" id="search-bar">
         <input name="q" type="hidden" value="hemisphere-enhanced"/>
         <input name="target" type="hidden" value="Mars"/>
         <input name="__ncforminfo" type="hidden" value="j_yMAIBTscKr8tI7tkjLqUwOBIFefc4oD8utdC0-YLU4Dy89b5AvswwcjWdvhV9-Rrxi5Fw-NZsHe7tb0A83gb-6OMlek_Fx-ytuwHc36Yi02rkpW79KZw=="/>
        </form>
        <div class="full-content">
         <section class="block" id="results-accordian">
          <div class="result-list" data-section="product" id="product-section">
           <div class="accordian">
            <h2>
             Products
            </h2>
            <span class="count">
             4 Results
            </span>
            <span class="collapse">
             Collapse
            </span>
           </div>
           <div class="collapsible results">
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/cerberus_enhanced">
              <img alt="Cerberus Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/dfaf3849e74bf973b59eb50dab52b583_cerberus_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/cerberus_enhanced">
               <h3>
                Cerberus Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 21 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Cerberus hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. This mosaic is composed of 104 Viking Orbiter images acquired…
              </p>
             </div>
             <!-- end description -->
            </div>
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/schiaparelli_enhanced">
              <img alt="Schiaparelli Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/7677c0a006b83871b5a2f66985ab5857_schiaparelli_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/schiaparelli_enhanced">
               <h3>
                Schiaparelli Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 35 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Schiaparelli hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. The images were acquired in 1980 during early northern…
              </p>
             </div>
             <!-- end description -->
            </div>
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/syrtis_major_enhanced">
              <img alt="Syrtis Major Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/aae41197e40d6d4f3ea557f8cfe51d15_syrtis_major_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/syrtis_major_enhanced">
               <h3>
                Syrtis Major Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 25 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Syrtis Major hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. This mosaic is composed of about 100 red and violet…
              </p>
             </div>
             <!-- end description -->
            </div>
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/valles_marineris_enhanced">
              <img alt="Valles Marineris Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/04085d99ec3713883a9a57f42be9c725_valles_marineris_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/valles_marineris_enhanced">
               <h3>
                Valles Marineris Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 27 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Valles Marineris hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. The distance is 2500 kilometers from the surface of…
              </p>
             </div>
             <!-- end description -->
            </div>
            <script>
             addBases=[];;if(typeof resetLayerSwitcher==="function"){resetLayerSwitcher(false)};var productTotal = 4;
            </script>
           </div>
           <!-- end this-section -->
          </div>
         </section>
        </div>
       </div>
       <div class="icons projects black scroll-wrapper">
        <div class="scroll">
         <a class="icon" href="http://isis.astrogeology.usgs.gov" title="Integrated Software for Imagers and Spectrometers">
          <img alt="ISIS Logo" height="112" src="/images/logos/isis_2x.jpg" width="112"/>
          <span class="label">
           ISIS
          </span>
         </a>
         <a class="icon" href="http://planetarynames.wr.usgs.gov" title="Gazetteer of Planetary Nomenclature">
          <img alt="Nomenclature Logo" height="112" src="/images/logos/nomenclature_2x.jpg" width="112"/>
          <span class="label">
           Planetary Nomenclature
          </span>
         </a>
         <a class="icon" href="http://astrogeology.usgs.gov/tools/map" title="Map a Planet 2">
          <img alt="Map-a-Planet Logo" height="112" src="/images/logos/map_a_planet_2x.jpg" width="112"/>
          <span class="label">
           Map a Planet 2
          </span>
         </a>
         <a class="icon" href="/facilities/imaging-node-of-nasa-planetary-data-system-pds" title="PDS Imaging Node">
          <img alt="PDS Logo" height="112" src="/images/pds_logo-black-web.png"/>
          <span class="label">
           PDS Imaging Node
          </span>
         </a>
         <!--
    						<a title="Astropedia Search" href="/search" class="icon">
    							<img alt="Astropedia Logo" height="112" width="112" src="/images/logos/astropedia_2x.jpg"/>
    							<span class="label">Astropedia</span>
    						</a>
    -->
         <a class="icon" href="/rpif" title="Regional Planetary Image Facility">
          <img alt="RPIF Logo" height="112" src="/images/logos/rpif_2x.jpg" width="112"/>
          <span class="label">
           RPIF
          </span>
         </a>
         <a class="icon" href="/facilities/photogrammetry-guest-facility" title="Photogrammetry Guest Facility">
          <img alt="Photogrammetry Guest Faciltiy Logo" height="112" src="/images/logos/photogrammetry_2x.jpg" width="112"/>
          <span class="label">
           Photogrammetry Guest Facility
          </span>
         </a>
         <a class="icon" href="http://pilot.wr.usgs.gov" title="Planetary Image Locator Tool">
          <img alt="Pilot Logo" height="112" src="/images/logos/pilot_2x.jpg" width="112"/>
          <span class="label">
           PILOT
          </span>
         </a>
         <a class="icon" href="/facilities/mrctr" title="Mapping, Remote-sensing, Cartography, Technology and Research GIS Lab">
          <img alt="MRCTR GIS Lab Logo" height="112" src="/images/logos/mrctr_2x.jpg" width="112"/>
          <span class="label">
           MRCTR GIS Lab
          </span>
         </a>
        </div>
       </div>
       <footer>
        <div class="left">
         <a href="http://astrogeology.usgs.gov">
          Home
         </a>
         |
         <a href="http://astrogeology.usgs.gov/contact">
          Contact
         </a>
         |
         <a href="http://astrogeology.usgs.gov/about/events">
          Events
         </a>
         |
         <a href="http://astrogeology.usgs.gov/news">
          News
         </a>
        </div>
        <div class="right">
         <a href="http://www.doi.gov">
          U.S. Department of Interior
         </a>
         |
         <a href="http://www.usgs.gov">
          U.S. Geological Survey
         </a>
         |
         <a href="http://www.usa.gov">
          USA.gov
         </a>
        </div>
       </footer>
      </div>
      <!--
    		<div class="credit">
    			<small>Background Credits: NASA/USGS</small>
    		</div>
    -->
      <div class="page-background" style="
    			background:url('/images/backgrounds/mars.jpg');
    			filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(
    				src='/images/backgrounds/mars.jpg', sizingMethod='scale');
    		">
      </div>
      <script type="text/javascript">
       var baseUrl = "";
    
    
    var _gaq = _gaq || [];_gaq.push(['_setAccount', 'UA-27613186-1']);_gaq.push(['_trackPageview']);(function() { var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js'; var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);})();
      </script>
      <script src="//ajax.googleapis.com/ajax/libs/jqueryui/1.11.3/jquery-ui.min.js" type="text/javascript">
      </script>
      <script src="/js/general.js" type="text/javascript">
      </script>
     </body>
    </html>
    


```python
#get the 4 hemispheres (class of 'item')
hemispheres = soup.select('div.item')

hemispheres
```




    [<div class="item"><a class="itemLink product-item" href="/search/map/Mars/Viking/cerberus_enhanced"><img alt="Cerberus Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/dfaf3849e74bf973b59eb50dab52b583_cerberus_enhanced.tif_thumb.png"/></a><div class="description"><a class="itemLink product-item" href="/search/map/Mars/Viking/cerberus_enhanced"><h3>Cerberus Hemisphere Enhanced</h3></a><span class="subtitle" style="float:left">image/tiff 21 MB</span><span class="pubDate" style="float:right"></span><br/><p>Mosaic of the Cerberus hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. This mosaic is composed of 104 Viking Orbiter images acquired…</p></div> <!-- end description --></div>,
     <div class="item"><a class="itemLink product-item" href="/search/map/Mars/Viking/schiaparelli_enhanced"><img alt="Schiaparelli Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/7677c0a006b83871b5a2f66985ab5857_schiaparelli_enhanced.tif_thumb.png"/></a><div class="description"><a class="itemLink product-item" href="/search/map/Mars/Viking/schiaparelli_enhanced"><h3>Schiaparelli Hemisphere Enhanced</h3></a><span class="subtitle" style="float:left">image/tiff 35 MB</span><span class="pubDate" style="float:right"></span><br/><p>Mosaic of the Schiaparelli hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. The images were acquired in 1980 during early northern…</p></div> <!-- end description --></div>,
     <div class="item"><a class="itemLink product-item" href="/search/map/Mars/Viking/syrtis_major_enhanced"><img alt="Syrtis Major Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/aae41197e40d6d4f3ea557f8cfe51d15_syrtis_major_enhanced.tif_thumb.png"/></a><div class="description"><a class="itemLink product-item" href="/search/map/Mars/Viking/syrtis_major_enhanced"><h3>Syrtis Major Hemisphere Enhanced</h3></a><span class="subtitle" style="float:left">image/tiff 25 MB</span><span class="pubDate" style="float:right"></span><br/><p>Mosaic of the Syrtis Major hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. This mosaic is composed of about 100 red and violet…</p></div> <!-- end description --></div>,
     <div class="item"><a class="itemLink product-item" href="/search/map/Mars/Viking/valles_marineris_enhanced"><img alt="Valles Marineris Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/04085d99ec3713883a9a57f42be9c725_valles_marineris_enhanced.tif_thumb.png"/></a><div class="description"><a class="itemLink product-item" href="/search/map/Mars/Viking/valles_marineris_enhanced"><h3>Valles Marineris Hemisphere Enhanced</h3></a><span class="subtitle" style="float:left">image/tiff 27 MB</span><span class="pubDate" style="float:right"></span><br/><p>Mosaic of the Valles Marineris hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. The distance is 2500 kilometers from the surface of…</p></div> <!-- end description --></div>]




```python
#Loop through each hemisphere

hemisphere_image_urls = []

for h in hemispheres:
    title = (h.find('h3').text).replace(' Enhanced', '')
        
    #click the hemisphere
    browser.click_link_by_partial_text(title)
    
    #make new soup of that page
    soup = BeautifulSoup(browser.html, 'html.parser')
    
    #find the full image
    full = soup.find('a', text='Sample')
    
    #get the img url
    img_url = full['href']
    
    #make a dict and append to the list
    hemisphere_image_urls.append({'title': title, 'img_url': img_url})
    
    #go back 
    browser.back()

#close browser
browser.quit()    

hemisphere_image_urls
```




    [{'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/cerberus_enhanced.tif/full.jpg',
      'title': 'Cerberus Hemisphere'},
     {'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/schiaparelli_enhanced.tif/full.jpg',
      'title': 'Schiaparelli Hemisphere'},
     {'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/syrtis_major_enhanced.tif/full.jpg',
      'title': 'Syrtis Major Hemisphere'},
     {'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/valles_marineris_enhanced.tif/full.jpg',
      'title': 'Valles Marineris Hemisphere'}]


