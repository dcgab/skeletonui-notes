<script lang="ts">
  import { goto } from '$app/navigation';
  import { noteStore } from '$lib/stores';
  import { InputChip, toastStore, type ToastSettings } from '@skeletonlabs/skeleton';

  let tags: string[] = [];
  let content: string;

  const t: ToastSettings = {
    message: 'Note created successfully!',
    background: 'variant-filled-success'
  };

  function createNote(): void {
    noteStore.update((notes) => [
      ...notes,
      {
        id: crypto.randomUUID(),
        content,
        tags
      }
    ]);
    content = '';
    tags = [];
    toastStore.trigger(t);
    goto('/');
  }
</script>

<div class="flex flex-col gap-8">
  <form class="card p-4 space-y-4 flex flex-col">
    <h2 class="h2">New Note</h2>
    <textarea bind:value={content} class="textarea" rows="5" placeholder="Note content..." />
    <InputChip bind:value={tags} name="tags" placeholder="Tags..." />
    <button on:click={createNote} type="button" class="btn variant-ghost-primary w-fit self-end"
      >Create Note</button
    >
  </form>
</div>
