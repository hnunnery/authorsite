<template>
  <Layout>
    <v-container class="pt-0 pt-md-6">
      <v-row class="justify-center mb-12 pb-12">
        <v-col cols="12" md="10" lg="8" xl="6" class="pa-0">
          <v-img
            :src="$page.post.featuredImage"
            :alt="$page.post.alt"
            lazy-src
          ></v-img>
          <h1
            class="display-1 mont mt-5 mt-sm-12 mb-4 mb-sm-8 mx-3 text-center"
            style="line-height: 1em;"
          >
            {{ $page.post.title }}
          </h1>
          <p class="subheading text-xs-left mx-3 mb-6 mb-sm-12">
            {{ $page.post.date }}
          </p>
          <div
            v-html="$page.post.content"
            class="markdown-body text-xs-left mx-3"
          />
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<page-query>
query Post ($path: String!) {
  post: post (path: $path) {
    title
    content
    featuredImage
    alt
    date
    preview
    path
  }
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.post.title,
      meta: [
        {
          key: 'description',
          name: 'description',
          content: this.$page.post.preview,
        },
        {
          key: 'og:title',
          property: 'og:title',
          content: this.$page.post.title,
        },
        {
          key: 'og:description',
          property: 'og:description',
          content: this.$page.post.preview,
        },
        {
          key: 'og:image',
          property: 'og:image',
          content: this.$page.post.featuredImage,
        },
        {
          key: 'og:url',
          property: 'og:url',
          content: `https://authorsite.netlify.app${this.$page.post.path}`,
        },
        {
          key: 'og:type',
          property: 'og:type',
          content: 'article',
        },
        {
          key: 'twitter:card',
          name: 'twitter:card',
          content: 'summary_large_image',
        },
      ],
    };
  },
};
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/4.0.0/github-markdown.min.css');
</style>
