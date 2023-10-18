<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-card><div class="page-container"></div></v-card>
        <v-card class="logo py-4 d-flex justify-center">
          <v-img
            height="180px"
            max-width="180"
            src="https://iftechpublicassets.s3.us-west-2.amazonaws.com/static-public-images/ian-floyd-profile-picture.png"
            alt=""
          ></v-img>
        </v-card>
        <v-card>
          <v-card-text>
            <h1>Development Philosophy and Approach</h1>
            <br />
            <p>
              At ifTech Digital Foundry and Boutique, we believe that the best
              digital products are those that are:
            </p>
            <p>
              User-centered: We start by understanding our clients' users and
              their needs. This allows us to design and develop products that
              are easy to use and enjoyable to interact with.
            </p>

            <p>
              Data-driven: We use data to inform our design and development
              decisions. This helps us to create products that are effective and
              meet the needs of our clients' users.
            </p>
            <p>
              Technically sound: We use the latest technologies and best
              practices to develop high-quality, scalable, and secure products.
            </p>
            <h2>Approach</h2>
            <br />

            Our approach to web development is iterative and collaborative. We
            work closely with our clients throughout the development process to
            ensure that we are meeting their needs and expectations. Our typical
            development process includes the following steps:
            <br />
            Discovery: We begin by understanding our client's business goals,
            target audience, and requirements.
            <br />
            Design: We create wireframes and mockups to visualize the product
            and get feedback from our client. Development: We develop the
            product using our preferred development stack and best practices.
            <br />
            <p>
              Testing: We thoroughly test the product to ensure that it is
              bug-free and meets our client's requirements. Deployment: We
              deploy the product to a production environment and provide support
              to our client after launch. Contact iftech at
              ianfloydtechnology.com today to learn more about how we can help
              you build your next digital product.
            </p>
            <br />
            <p>Preferred development stack:</p>
            <p>Frontend: Vue || Nuxt || Vuetify || Vuex || D3 || ThreeJS</p>
            <p>
              Backend: Node || Express || AWS Amplify || AWS Appsync || AWS API
              Gateway || Rocket
            </p>
            <p>Query: REST || GraphQL</p>
            <p>Cloud: AWS</p>
            <p>
              Database/Data Analytics/ETL: Python, Pandas, Jupyter, SSIS,
              MongoDB, NoSQL, DynamoDB, PostgreSQL
            </p>
            <p>Other: Godot, Adobe Products, FL Studio</p>
            <p>
              For a complete description of familiar technologies, see
              <v-btn color="primary" nuxt to="/inspire"> My Toolset </v-btn>
            </p>
            <p>Thank you for checking out my website.</p>
            <div class="text-xs-right">
              <em><small>&mdash; Ian Floyd</small></em>
            </div>
            <hr class="my-3" />
          </v-card-text>
          <!-- <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/inspire"> Continue </v-btn>
        </v-card-actions> -->
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
