<script lang="ts">
  import { metadata } from "$lib/app/stores";
  import Image from "$lib/components/Image.svelte";
  import { authModel, watch } from "$lib/pocketbase";
  import type { ConsultationsResponse } from "$lib/pocketbase/generated-types";
  $metadata.title = "Recent Consultations";
  const consultations = watch<ConsultationsResponse>("consultations", {
    sort: "-updated",
  });
</script>

{#if $authModel}
  <a href="new/edit">Create New</a>
{:else}
  <p>Please login to create new consultations.</p>
{/if}
<hr />
<table>
  <tbody>
    {#each $consultations.items as consultation}
      {#if $authModel?.id == consultation.user}
        <tr>
          <td><a href={consultation.id}>{consultation.quand}</a></td>
          <td><a href={`${consultation.id}/edit`}>Edit</a></td>
          <td><a href={`${consultation.id}#delete`}>Delete</a></td>
        </tr>
      {:else}
        <tr>

          <td><a href={consultation.id}>{consultation.quand}</a></td>
          <td>{consultation.quand}</td>
        </tr>
      {/if}
    {:else}
      <tr>
        <td>No consultations found.</td>
      </tr>
    {/each}
  </tbody>
</table>
