<template>
    <div>
        <div style="position: fixed; z-index: 99999; top: 0px; left: 45%;"><a
                class="sr-only sr-only-focusable aurora-skip" href="#main-content">Skip to main content</a>
        </div>
        <header class="shadow-sm">
            <div class="" style="background-color: #FAF2CC; text-align: left; vertical-align: middle;">
                <div class="container py-3">
                    <div style="width: 2em ;display: inline-block; padding-right: .5em; vertical-align: middle;">
                      <a @click="toggleBannerInfo()" href="#">
                          <i id="chevron" class="fa fa-chevron-right" style="color: #000; font-size: 1.3em"></i>
                      </a>
                    </div>

                    <button
                        style="background: #FEC04F; border: 1px solid #000000; border-radius: 20px; margin-right: 10px;"><strong>ARCHIVED</strong></button>
                    <span>This prototype is no longer under development.</span>

                    <div v-show="showBannerContent">
                        <br>
                        <p style="margin-bottom: .2em;">This prototype is no longer being maintained as of
                            March 27, 2020. The information provided may no longer be accurate. Please
                            consult the <a target="_blank"
                                href="https://rehelv-acrd.tpsgc-pwgsc.gc.ca/acrds/index-eng.aspx">Accommodation
                                and Car Rental Directory</a> and the
                            <a target="_blank" href="https://www.njc-cnm.gc.ca/directive/d10/en">National Joint Council Travel
                                Directive</a> for the most up-to-date information.</p>
                            <p style="margin-bottom: .2em;">For more information on the NextGen Travel program, please visit
                            <a target="_blank"
                                href="http://gcintranet.tpsgc-pwgsc.gc.ca/gc/svp-sts/postes-roles-eng.html">http://gcintranet.tpsgc-pwgsc.gc.ca/gc/svp-sts/postes-roles-eng.html</a>.</p>
                            <p style="margin-bottom: .2em;">If you are interested in contributing to this project, the source code is
                            available on Github: <a target="_blank"
                                href="https://github.com/nextgentravel/travel-estimator">https://github.com/nextgentravel/travel-estimator</a></p>
                    </div>
                </div>
            </div>
        </header>
    </div>
</template>

<script>
    export default {
        name: 'Header',
        mounted: function () {
          this.setInitialBannerState();
        },
        data: function () {
          return {
            showBannerContent: true,
          }
        },
        methods: {
            toggleBannerInfo: function () {
              localStorage.setItem("banner-content", !this.showBannerContent);
              this.showBannerContent = !this.showBannerContent;
            },
            setInitialBannerState: function () {
              let bannerContent = localStorage.getItem("banner-content");
              this.showBannerContent = JSON.parse(bannerContent.toLowerCase());
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

header {
  margin-bottom: 20px;
}

</style>