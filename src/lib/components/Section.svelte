<script>
  import { slide, fade } from "svelte/transition";
  import Carousel from "svelte-carousel";
  import { link } from "svelte-spa-router";
  export let overview = false;
  export let section = {
    image,
    title,
    title_shadow,
    text,
    resume,
    icons,
    tint,
    filter,
    url,
  };

  const textToShow =
    (overview ? section.resume : section.text) || section.text[0];
  let iconsUrl = section.icons.map((iconName) => {
    const iconMapper = {
      image: "icons/003-image-gallery.png",
      video: "icons/002-video.png",
      text: "icons/001-text-format.png",
      map: "icons/001-maps.png",
      pdf: "icons/006-pdf.png",
    };
    return iconMapper[iconName];
  });

  let showText = true;
  function disableText() {
    showText = !showText;
  }
</script>

<!-- data-aos="zoom-out" -->
<!-- data-aos-anchor-placement="center"  -->
<div
  class="relative w-full flex align-middle justify-center md:h-screen-80 lg:h-screen-90 : {section.tint} 
  "
>
  <div
    class="transition delay-100 parallax {section.tint}
      w-full h-full absolute bg-cover"
    style="{section.image
      ? `background-image: url(./images/${section.image});`
      : ''} filter: {section.filter};"
  ></div>

  <div class="text-white relative h-full w-2/3 bg-purple">
    <div class="md:pt-20 lg:pt-20 h-1/3 overflow-hidden">
      <h2
        data-aos="zoom-out"
        class="text-shadow-sm {section.title_shadow} transition delay-300 text-center bg-purple
        md:text-4xl xl:text-6xl : tracking-wider font-mont font-medium py-5 whitespace-pre-line"
      >
        {section.title.toUpperCase()}
      </h2>
      <div data-aos="zoom-out" class="flex justify-center">
        {#each iconsUrl as icon}
          <a
            class="hover:scale-125 mr-8 transition ease-in-out delay-75 w-12 mr-2"
            href={`/${section.url}`}
            use:link
          >
            <i class="w-16">
              <img class="invert" src="./images/{icon}" alt="video" />
            </i>
          </a>
        {/each}
      </div>

      <p
        data-aos="zoom-out"
        class="transition delay-50 text-justify bg-[]
          md:text-base lg:text-base font-mont h-2/3
             py-10 whitespace-pre-line truncate
            "
      >
        {textToShow}
      </p>
      <!-- </Carousel> -->
    </div>
  </div>
</div>

<style>
  .h-screen-50 {
    height: 50vh;
  }
  .h-screen-80 {
    height: 80vh;
  }

  .h-screen-90 {
    height: 90vh;
  }

  .parallax {
    /* filter: grayscale(100%); */
    /* background-color: rgb(83, 13, 56); */
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-blend-mode: multiply;
  }
</style>
