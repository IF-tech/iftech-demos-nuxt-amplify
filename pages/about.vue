<template>
    <v-container>
   <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-card><div class="page-container">


    </div></v-card>
         <v-card class="logo py-4 d-flex justify-center">
          <v-img
            height="180px"
            max-width="180"
            src="https://iftechpublicassets.s3.us-west-2.amazonaws.com/static-public-images/ian-floyd-profile-picture.png"
            alt=""
          ></v-img>
        </v-card>
         <v-card>
          <v-card-title class="headline">
            ifTech Digital Foundry and Boutique
          </v-card-title>
          <v-card-text>
            <p>
              Ian Floyd is a passionate technologist that seeks to merge the
              realms of DATA, DEVELOPMENT, and DESIGN to create digital products
              that fit into a world where humans feel good about using the
              technology they rely on.
            </p>
            <p>Preferred development stack:</p>
            <p>Frontend: Vue || Nuxt || Vuetify || Vuex || D3 || ThreeJS</p>
            <p>
              Backend: Node || Express || AWS Amplify || AWS Appsync || AWS API
              Gateway || Rocket
            </p>
            <p>Query: REST || GraphQL</p>
            <p>Cloud: AWS</p>
            <p>
              Database/Data Analytics/ETL: Python, Pandas, Jupyter, SSIS, MongoDB,
              NoSQL, DynamoDB, PostgreSQL
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
