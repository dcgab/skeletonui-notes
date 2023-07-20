<script lang="ts">
  import { noteStore } from '$lib/stores';
  import { toastStore, type ModalSettings, modalStore } from '@skeletonlabs/skeleton';

  function deleteNote(noteId: string): void {
    const confirmDelete: ModalSettings = {
      type: 'confirm',
      title: 'Delete Note',
      body: 'Are you sure you want to delete this note?',
      response: (r: boolean) => {
        if (r) {
          noteStore.update((notes) => notes.filter((n) => n.id !== noteId));
          toastStore.trigger({
            message: 'Note deleted successfully',
            background: 'variant-ghost-success'
          });
          return;
        }
        toastStore.trigger({
          message: 'Note not deleted',
          background: 'variant-ghost-error'
        });
      }
    };
    modalStore.trigger(confirmDelete);
  }
</script>

<div class="space-y-8">
  <div class="flex items-center justify-between">
    <h2 class="h2">Notes</h2>
    <a href="/new" class="btn variant-ghost-primary">New Note</a>
  </div>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
    {#each $noteStore as note (note.id)}
      <div class="card p-4 variant-ghost-warning flex flex-col gap-2 relative">
        <button
          on:click={() => deleteNote(note.id)}
          class="btn-icon btn-icon-sm variant-filled-error absolute -top-1.5 -right-1.5">X</button
        >
        <div>
          {note.content}
        </div>
        <div class="flex gap-1 flex-wrap">
          {#each note.tags as tag (tag)}
            <span class="chip variant-filled-secondary">{tag}</span>
          {/each}
        </div>
      </div>
    {/each}
  </div>
</div>

<!-- <div class="space-y-5">
  <h3 class="h3">Page title</h3>
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Officia consequuntur nulla veritatis
    cum commodi dicta, incidunt architecto sed nostrum doloribus praesentium quis officiis
    cupiditate fugit mollitia quos earum et. Explicabo.
  </p>
  <button type="button" class="btn variant-filled-primary">Hello world</button>
</div>

<hr class="my-8" /> -->
