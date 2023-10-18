<template>
  <div class="services">
    <div style="width: 100%">
      <h1>Development</h1>
      <v-carousel cycle hide-delimiters show-arrows-on-hover>
        <v-carousel-item
          style="height: 100%"
          v-for="(service, index) in developmentServices"
          :key="index"
        >
          <!-- <h2>{{ service.title }}</h2> -->
          <div class="service-cards">
            <div class="mobile-card">
              <h3>{{ service.title }}</h3>
              <p>{{ service.description }}</p>
              <!-- <p>Going Rate: {{ service.goingRate }}</p>
              <p>ifTech Rate: {{ service.iftechRate }}</p> -->
              <router-link :to="`${service.linkTo}`" class="book-button"
                >Learn More</router-link
              >
            </div>
          </div>
        </v-carousel-item>
      </v-carousel>
      <h1>Data</h1>
      <v-carousel cycle hide-delimiters show-arrows-on-hover>
        <v-carousel-item
          style="height: 100%"
          v-for="(service, index) in dataServices"
          :key="index"
        >
          <!-- <h2>{{ service.title }}</h2> -->
          <div class="service-cards">
            <div class="mobile-card">
              <h3>{{ service.title }}</h3>
              <p>{{ service.description }}</p>
              <!-- <p>Going Rate: {{ service.goingRate }}</p>
              <p>ifTech Rate: {{ service.iftechRate }}</p> -->
              <router-link :to="`${service.linkTo}`" class="book-button"
                >Learn More</router-link
              >
            </div>
          </div>
        </v-carousel-item>
      </v-carousel>

      <h1>Design</h1>
      <v-carousel cycle hide-delimiters show-arrows-on-hover>
        <v-carousel-item
          style="height: 100%"
          v-for="(service, index) in designServices"
          :key="index"
        >
          <!-- <h2>{{ service.title }}</h2> -->
          <div class="service-cards">
            <div class="mobile-card">
              <h3>{{ service.title }}</h3>
              <p>{{ service.description }}</p>
              <!-- <p>Going Rate: {{ service.goingRate }}</p>
              <p>ifTech Rate: {{ service.iftechRate }}</p> -->
              <router-link :to="`${service.linkTo}`" class="book-button"
                >Learn More</router-link
              >
            </div>
          </div>
        </v-carousel-item>
      </v-carousel>
    </div>
    <div></div>
  </div>
</template>
<script>
export default {
  data: () => ({
    dataServices: [
      {
        title: 'Data Mining',
        description: 'Extracting valuable insights from large datasets.',
        goingRate: '$60 - $80/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Database Management',
        description: 'Maintaining and securing your databases reliably.',
        goingRate: '$50 - $70/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Data Cleaning',
        description: 'Ensuring accuracy and integrity of your data.',
        goingRate: '$50 - $60/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Predictive Analytics',
        description: 'Using advanced tech to predict future outcomes.',
        goingRate: '$70 - $90/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Data Visualization',
        description: 'Representing your data in clear and creative ways.',
        goingRate: '$60 - $80/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Machine Learning',
        description: 'Improving your systems with data-driven algorithms.',
        goingRate: '$80 - $100/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Data Integration',
        description: 'Combining data and applications into one unified system.',
        goingRate: '$60 - $80/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Big Data Solutions',
        description:
          'Handling massive volumes of both structured and unstructured data.',
        goingRate: '$80 - $100/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Real-time Analytics',
        description: 'Providing analysis as soon as data enters the system.',
        goingRate: '$65 - $85/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
      {
        title: 'Cloud Database Solutions',
        description: 'Securely manage and analyze your data on cloud.',
        goingRate: '$70 - $90/hour',
        iftechRate: '~$39/hour',
        linkTo: '/Services/Data',
      },
    ],

    developmentServices: [
      {
        title: 'App Development',
        description: 'Building user-friendly mobile apps.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'Web Development',
        description: 'Creating cutting-edge and responsive websites.',
        goingRate: '$70 - $90/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'Software Development',
        description: 'Designing and developing high-quality software.',
        goingRate: '$70 - $100/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'Game Development',
        description: 'Creating engaging and interactive video games.',
        goingRate: '$80 - $110/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'API Development',
        description: 'Developing secure APIs for flexible solutions.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'Backend Development',
        description: 'Strengthening your apps with a powerful backend.',
        goingRate: '$70 - $100/hour',
        iftechRate: '$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'Frontend Development',
        description: 'Designing accessible and intuitive UIs.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'E-commerce Development',
        description: 'Developing robust E-commerce platforms.',
        goingRate: '$75 - $105/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'CMS Development',
        description: 'Customizing CMS as per your business needs.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
      {
        title: 'Cross-Platform App Development',
        description: 'Creating apps that work seamlessly across devices.',
        goingRate: '~$70 - $100/hour',
        iftechRate: '~$49/hour',
        linkTo: '/Services/Dev',
      },
    ],

    designServices: [
      {
        title: 'Branding',
        description: 'Building strong and unique brand identities.',
        goingRate: '$70 - $100/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Logo Design',
        description: 'Designing logos that represent your brand.',
        goingRate: '$50 - $80/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Graphic Design',
        description: 'Creating visually appealing graphics.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'UX/UI Design',
        description: 'Improving user experience and interface.',
        goingRate: '$70 - $100/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: '2D/3D Asset Creation',
        description: 'Crafting beautiful and detailed 2D/3D assets.',
        goingRate: '$80 - $110/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Website Layout Design',
        description: 'Designing coherent and impactful website layouts.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Print Design',
        description: 'Creating designs for printed media.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Illustration',
        description: 'Turning ideas into unique and expressive illustrations.',
        goingRate: '$70 - $100/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Motion Graphics',
        description: 'Enhance your stories with captivating motion graphics.',
        goingRate: '$80 - $110/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
      {
        title: 'Infographics',
        description:
          'Presenting complex information through engaging infographics.',
        goingRate: '$60 - $90/hour',
        iftechRate: '~$29/hour',
        linkTo: '/Services/Design',
      },
    ],
    serviceTitles: ['Data Services', 'Development Services', 'Design Services'],
  }),
  computed: {
    allServices() {
      return [this.dataServices, this.developmentServices, this.designServices]
    },
    currentView() {
      if (this.$vuetify.breakpoint.xsOnly) {
        // for mobile devices
        return 'vertical-view'
      } else if (this.carousel) {
        // carousel view
        return 'carousel-view'
      } else {
        // expanded view i.e., Full list
        return 'expanded-view'
      }
    },
  },
}
</script>

<style scoped>
::-webkit-scrollbar {
  display: none;
}
.expanded-view {
  /* Styles for expanded/full-list view here */
}

.carousel-view {
  /* Styles for carousel view here */
}

.vertical-view {
  /* Styles for vertical view on mobile devices here */
}
.services {
  display: flex;
  flex-wrap: wrap;
  height: 100%;
}

.service-section {
  width: 100%;
  height: 100%;
}

.service-cards {
  display: flex;
  flex-wrap: wrap;
  height: 100%;
}

.card {
  width: 20%;
  margin: 1%;
  border: 1px solid #ddd;
  padding: 20px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

.mobile-card {
  width: 100%;
  margin: 1%;
  border: 1px solid #ddd;
  padding: 20px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

.book-button {
  display: inline-block;
  background-color: #44c767;
  border-radius: 28px;
  color: white;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.book-button:hover {
  background-color: #5cbf2a;
}
</style>
