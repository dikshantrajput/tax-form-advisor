<script lang="ts">
  import ItrDecisionTree from "$lib/components/ITRDecisionTree.svelte";
    import { GITHUB_ICON } from "$lib/icons";
  import Icon from "@iconify/svelte";
</script>

<div class="flex justify-center items-center absolute right-0 sm:p-4 p-2 gap-3">
  <a href="https://www.producthunt.com/posts/itr-form-advisor?embed=true&utm_source=badge-featured&utm_medium=badge&utm_souce=badge-itr&#0045;form&#0045;advisor" target="_blank"><img src="https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=469253&theme=light" alt="ITR&#0032;Form&#0032;Advisor - Find&#0032;your&#0032;appropriate&#0032;ITR&#0032;forms&#0032;effortlessly&#0046; | Product Hunt" style="width: 250px; height: 54px;" width="250" height="54" /></a>
  <a
    href="https://github.com/dikshantrajput/tax-form-advisor"
    target="_blank"
    class=" text-4xl"
  >
    <Icon icon={GITHUB_ICON} />
  </a>
</div>
<ItrDecisionTree />
