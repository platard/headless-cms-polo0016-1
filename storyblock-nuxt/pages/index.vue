<template>
    <div v-if="homeContent">
      <!-- Main Title -->
      <h1>{{ homeContent.title }}</h1>
  
      <!-- Introductions -->
         <div v-for="block in homeContent.introductions.content" :key="block._uid">
            <h2 v-if="block.type === 'heading'">{{ block.content[0].text }}</h2>
            <p v-if="block.type === 'paragraph'">{{ block.content[0].text }}</p>
        </div>
  
        <!-- Newborn Section -->
        <section v-if="homeContent.newborns" class="newborns">
        <div v-for="newborn in homeContent.newborns" :key="newborn._uid">
            <h2>{{ newborn.title }}</h2>
            <p v-html="newborn.summary.content[0].content[0].text"></p>
            
            <!-- Wake Windows -->
            <div v-if="newborn.wake_windows">
            <h3>Wake Windows</h3>
            <p>
                <span v-html="newborn.wake_windows.content[0].content[0].text"></span>
                <ul>
                <li v-for="(item, index) in newborn.wake_windows.content[1].content" :key="index" v-html="item.content[0].text"></li>
                </ul>
            </p>
            </div>

            <!-- Sleep Schedule -->
            <div v-if="newborn.sleep_schedule">
            <h3>Sleep Schedule</h3>
            <p>
                <span v-html="newborn.sleep_schedule.content[0].content[0].text"></span>
                <ul>
                <li v-for="(item, index) in newborn.sleep_schedule.content[1].content" :key="index" v-html="item.content[0].text"></li>
                </ul>
            </p>
        </div>

        <!-- Feeding Routine -->
        <div v-if="newborn.feeding_routine">
          <h3>Feeding Routine</h3>
          <p>
            <span v-html="newborn.feeding_routine.content[0].content[0].text"></span>
            <ul>
              <li v-for="(item, index) in newborn.feeding_routine.content[1].content" :key="index" v-html="item.content[0].text"></li>
            </ul>
          </p>
        </div>
        </div>
        </section>

        <!-- Infancy Section -->
        <section v-if="homeContent.infancy" class="infancy">
        <div v-for="infant in homeContent.infancy" :key="infant._uid">
            <h2>{{ infant.title }}</h2>
            <p v-html="infant.summary.content[0].content[0].text"></p>
            
                    <!-- Wake Windows -->
                    <div v-if="infant.wake_windows">
                    <h3>Wake Windows</h3>
                    <p>
                        <span v-html="infant.wake_windows.content[0].content[0].text"></span>
                        <ul>
                        <li v-for="(item, index) in infant.wake_windows.content[1].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    </p>
                    </div>

                    <!-- Sleep Schedule -->
                    <div v-if="infant.sleep_schedule">
                    <h3>Sleep Schedule</h3>
                    <p>
                        <span v-html="infant.sleep_schedule.content[0].content[0].text"></span>
                        <ul>
                        <li v-for="(item, index) in infant.sleep_schedule.content[1].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    </p>
                    </div>

                    <!-- Feeding Routine -->
                    <div v-if="infant.feeding_routine">
                    <h3>Feeding Routine</h3>
                    <p>
                        <span v-html="infant.feeding_routine.content[0].content[0].text"></span>
                        <ul>
                        <li v-for="(item, index) in infant.feeding_routine.content[1].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    </p>
                    </div>

                    <!-- Developmental Milestones -->
                    <div v-if="infant.developmental_milestones">
                    <h3>Developmental Milestones</h3>
                    <p>
                        <ul>
                        <li v-for="(item, index) in infant.developmental_milestones.content[0].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    <span v-html="infant.developmental_milestones.content[1].content[0].text"></span>
                    </p>
                    </div>
        </div>
        </section>

        <!-- Pre-toddler Section -->
        <section v-if="homeContent.pretoddler" class="pretoddler">
        <div v-for="pretoddler in homeContent.pretoddler" :key="pretoddler._uid">
            <h2>{{ pretoddler.title }}</h2>
            <p v-html="pretoddler.summary.content[0].content[0].text"></p>

            <!-- Wake Windows -->
            <div v-if="pretoddler.wake_windows">
                    <h3>Wake Windows</h3>
                    <p>
                        <span v-html="pretoddler.wake_windows.content[0].content[0].text"></span>
                    </p>
                    </div>

                    <!-- Sleep Schedule -->
                    <div v-if="pretoddler.sleep_schedule">
                    <h3>Sleep Schedule</h3>
                    <p>
                        <span v-html="pretoddler.sleep_schedule.content[0].content[0].text"></span>
                        <ul>
                        <li v-for="(item, index) in pretoddler.sleep_schedule.content[1].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    </p>
                    </div>

                    <!-- Feeding Routine -->
                    <div v-if="pretoddler.feeding_routine">
                    <h3>Feeding Routine</h3>
                    <p>
                        <span v-html="pretoddler.feeding_routine.content[0].content[0].text"></span>
                        <ul>
                        <li v-for="(item, index) in pretoddler.feeding_routine.content[1].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    </p>
                    </div>

                    <!-- Developmental Milestones -->
                    <div v-if="pretoddler.developmental_milestones">
                    <h3>Developmental Milestones</h3>
                    <p>
                        <ul>
                        <li v-for="(item, index) in pretoddler.developmental_milestones.content[0].content" :key="index" v-html="item.content[0].text"></li>
                        </ul>
                    <span v-html="pretoddler.developmental_milestones.content[1].content[0].text"></span>
                    </p>
                    </div>
        
        </div>
        </section>
    </div>
    </template>

    <script>
    export default {
    data() {
        return {
        homeContent: null,
        };
    },
    created() {
        fetch('https://api-us.storyblok.com/v2/cdn/stories/home?cv=1701814861&token=qpnUjnVIpRSryPMcwJJcAQtt&version=published')
        .then(resp => resp.json())
        .then(data => {
            this.homeContent = data.story.content;
        })
        .catch(error => {
            console.error('Error fetching home content:', error);
        });
    },

    base: '/headless-cms-polo0016/storyblock-nuxt/'
    }
    </script>
    
    <style scoped>
    /* General styling */
    body {
      font-family: 'Arial', sans-serif;
      line-height: 1.6;
      color: #444;
      background-color: #f4f4f4;
    }
    
    .container {
      max-width: 1100px;
      margin: 30px auto;
      padding: 20px;
      background: #fff;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    h1 {
      color: #5D647B;
      text-align: center;
      margin-bottom: 2rem;
    }
    
    h2 {
      color: #5D647B;
      margin-top: 1.5rem;
      border-bottom: 2px solid #E4E7EB;
      padding-bottom: 10px;
    }
    
    section {
      margin-bottom: 2rem;
    }
    
    ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    
    li {
      background: #E4E7EB;
      margin-bottom: 8px;
      padding: 10px 15px;
      border-radius: 5px;
      transition: background 0.3s ease;
    }
    
    li:hover {
      background: #CFD4DB;
    }
    
    /* Clearfix hack */
    .clearfix::after {
      content: "";
      display: table;
      clear: both;
    }
    
    /* Responsive styles */
    @media (max-width: 768px) {
      h1 {
        font-size: 24px;
      }
    
      h2 {
        font-size: 22px;
      }
    }
    
    @media (max-width: 480px) {
      .container {
        margin: 15px;
      }
    
      h1 {
        font-size: 20px;
      }
    
      h2 {
        font-size: 20px;
      }
    
      li {
        padding: 8px 10px;
      }
    }
    </style>
    
    
    