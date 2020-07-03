<template>
  <Layout>
    <v-container>
      <v-row class="justify-center align-center mb-8">
        <v-col class="mb-12">
          <h1
            class="display-3 mont secondary--text text-center mt-md-5 mb-5 mb-md-12"
            style="line-height: 1em;"
          >
            Mortality Defines
          </h1>
          <p class="text-center">(insert book cover)</p>
          <p class="body-1 secondary--text mt-6" style="line-height: 2em;">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero
            autem facilis vitae sint enim repudiandae repellendus ea quia at in
            sed adipisci dolore modi, aspernatur voluptatem obcaecati neque
            asperiores harum cum culpa ducimus, error ad exercitationem!
            Consequatur, quasi quaerat? Iusto itaque temporibus aliquid
            recusandae architecto molestias similique nam rerum consectetur!
          </p>
          <p class="body-1 secondary--text mt-6" style="line-height: 2em;">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero
            autem facilis vitae sint enim repudiandae repellendus ea quia at in
            sed adipisci dolore modi, aspernatur voluptatem obcaecati neque
            asperiores harum cum culpa ducimus, error ad exercitationem!
            Consequatur, quasi quaerat? Iusto itaque temporibus aliquid
            recusandae architecto molestias similique nam rerum consectetur!
          </p>
        </v-col>
      </v-row>
      <v-row class="justify-center align-centermb-12">
        <v-col class="mb-12">
          <p class="text-center">(insert photo)</p>
          <h1
            class="display-3 mont secondary--text text-center mt-md-5"
            style="line-height: 1em;"
          >
            Josh Shuh
          </h1>
          <h2
            class="mont primary--text text-center mt-md-5 mb-5 mb-md-12"
            style="line-height: 1em;"
          >
            Author
          </h2>
          <p class="body-1 secondary--text mt-6" style="line-height: 2em;">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero
            autem facilis vitae sint enim repudiandae repellendus ea quia at in
            sed adipisci dolore modi, aspernatur voluptatem obcaecati neque
            asperiores harum cum culpa ducimus, error ad exercitationem!
            Consequatur, quasi quaerat? Iusto itaque temporibus aliquid
            recusandae architecto molestias similique nam rerum consectetur!
          </p>
          <p class="body-1 secondary--text mt-6" style="line-height: 2em;">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero
            autem facilis vitae sint enim repudiandae repellendus ea quia at in
            sed adipisci dolore modi, aspernatur voluptatem obcaecati neque
            asperiores harum cum culpa ducimus, error ad exercitationem!
            Consequatur, quasi quaerat? Iusto itaque temporibus aliquid
            recusandae architecto molestias similique nam rerum consectetur!
          </p>
        </v-col>
      </v-row>
      <v-row class="justify-center my-12 pb-12">
        <v-col
          cols="12"
          sm="6"
          md="4"
          lg="3"
          v-for="post in posts.slice(0, 4)"
          :key="post.node.id"
          @click="onClick(post)"
          style="cursor: pointer;"
        >
          <v-card flat>
            <v-img
              :src="post.node.featuredImage"
              :alt="post.node.alt"
              class="mx-auto mb-6"
              lazy-src
            ></v-img>
            <h3
              class="title secondary--text text-center mb-6"
              style="line-height: 1em;"
            >
              {{ post.node.title }}
            </h3>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<page-query>
query {
  allPost {
    totalCount
    edges {
      node {
        id
        title
        path
        date
        content
        preview
        featuredImage
        alt
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: 'Home',
  },
  computed: {
    posts() {
      const x = this.$page.allPost.edges.sort((a, b) =>
        Date.parse(a.node.date) > Date.parse(b.node.date) ? -1 : 1
      );
      return x;
    },
  },
  methods: {
    onClick(post) {
      this.$router.push({ path: post.node.path });
    },
  },
};
</script>
