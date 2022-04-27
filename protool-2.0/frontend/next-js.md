# Next js

In Current FE environment, `next-js` is the best solution for ssr (server side rendering). And in ecg, more and more site is turning the tech to `next-js` .

In this document, I would not try to explain how to use next-js, but give some Tips in our developing and consideration.



### Redux vs Reducer

I know lots of people really love the data flow redux does, but in our project, we use reducer.

The reason only use reducer hook is that:

1. redux is too heavy for the business
2. the trends for functional component is to use native reducer and it works well



### SSR and SSG

For SEO, Server side rendering is one of the key technology for generating the content to the google bot.&#x20;

SSR in next-js is based on the function:

```javascript
export async function getServerSideProps(context) {
  return {
    props: {}, // will be passed to the page component as props
  }
}
```

On server side, this function will generate the initial props for static render all the page content.



The difference from SSR and SSG is that SSG is generate the page before the server start.

```javascript
export async function getStaticPaths() {
  return {
    paths: [
      { params: { ... } }
    ],
    fallback: true // false or 'blocking'
  };
}

export async function getStaticProps(context) {
  return {
    props: {}, // will be passed to the page component as props
  }
}

```

These 2 apis would help to generate the static page and the dynamic part could be handle by client js code.



see also : [https://nextjs.org/docs/basic-features/data-fetching/overview](https://nextjs.org/docs/basic-features/data-fetching/overview)



### Other features

1. jest integration, the next js native support jest ([https://nextjs.org/blog/next-12-1#zero-configuration-jest-plugin](https://nextjs.org/blog/next-12-1#zero-configuration-jest-plugin))
2. [SWC](https://nextjs.org/docs/advanced-features/compiler) , the complier written in rust, very fast.







