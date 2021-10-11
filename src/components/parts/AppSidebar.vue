<template>
  <div class="w-full flex flex-col my-4 sticky top-5">
    <p class="text-xl font-semibold pb-5">Ads</p>
    <p class="pb-2" v-if="$static.metadata.siteShowAds">
      <Adsense
        data-ad-client="ca-pub-6367184538164263"
        data-ad-slot="1042574308"
        data-ad-format="auto"
        data-full-width-responsive="yes"
      >
      </Adsense>
    </p>
  </div>
</template>

<static-query>
query {
  metadata {
    siteShowAds
  }
}
</static-query>
