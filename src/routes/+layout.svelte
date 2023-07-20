<script lang="ts">
  // The ordering of these imports is critical to your app working properly
  import '@skeletonlabs/skeleton/themes/theme-skeleton.css';
  // import '@skeletonlabs/skeleton/themes/theme-vintage.css';
  // If you have source.organizeImports set to true in VSCode, then it will auto change this ordering
  import '@skeletonlabs/skeleton/styles/skeleton.css';
  // Most of your app wide CSS should be put in this file
  import '../app.postcss';
  import {
    AppBar,
    AppShell,
    Avatar,
    Drawer,
    drawerStore,
    LightSwitch,
    Modal,
    Toast
  } from '@skeletonlabs/skeleton';
  import Navigation from '$lib/components/Navigation.svelte';

  function drawerOpen() {
    drawerStore.open();
  }
</script>

<Toast position="tr" />
<Modal />
<Drawer width="w-80">
  <h2 class="text-xl p-4">Navigation</h2>
  <hr />
  <Navigation />
</Drawer>

<AppShell slotSidebarLeft="w-0 md:w-52 bg-surface-500/10">
  <svelte:fragment slot="header">
    <AppBar>
      <svelte:fragment slot="lead">
        <div class="flex items-center">
          <button class="md:hidden btn btn-sm mr-4" on:click={drawerOpen}>
            <span>
              <svg viewBox="0 0 100 80" class="fill-token w-4 h-4">
                <rect width="100" height="20" />
                <rect y="30" width="100" height="20" />
                <rect y="60" width="100" height="20" />
              </svg>
            </span>
          </button>
          <strong class="text-xl uppercase">Noted</strong>
        </div>
      </svelte:fragment>
      <svelte:fragment slot="trail">
        <Avatar initials="DG" background="bg-primary-500" width="w-10" />
        <LightSwitch />
      </svelte:fragment>
    </AppBar>
  </svelte:fragment>
  <svelte:fragment slot="sidebarLeft">
    <Navigation />
  </svelte:fragment>
  <!-- <svelte:fragment slot="sidebarRight">Sidebar Right</svelte:fragment> -->
  <!-- <svelte:fragment slot="pageHeader">Page Header</svelte:fragment> -->
  <!-- Router Slot -->
  <div class="container mx-auto p-10">
    <slot />
  </div>

  <!-- ---- / ---- -->
  <!-- <svelte:fragment slot="pageFooter">Page Footer</svelte:fragment>
	<svelte:fragment slot="footer">Footer</svelte:fragment> -->
</AppShell>
