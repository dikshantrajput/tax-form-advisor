<script lang="ts">
  import ItrDecisionTree from "$lib/components/ITRDecisionTree.svelte";
    import { GITHUB_ICON } from "$lib/icons";
  import Icon from "@iconify/svelte";
</script>

<div class="flex justify-center items-center absolute right-0 sm:p-4 p-2">
  <a
    href="https://github.com/dikshantrajput/tax-form-advisor"
    target="_blank"
    class=" text-4xl"
  >
    <Icon icon={GITHUB_ICON} />
  </a>
</div>
<ItrDecisionTree />
