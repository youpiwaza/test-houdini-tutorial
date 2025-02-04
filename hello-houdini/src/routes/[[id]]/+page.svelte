<script>
    import { Container, Display, Sprite, Panel } from '~/components'
    import { SpeciesPreview, SpeciesPreviewPlaceholder } from '~/components'
    
    /* @type { import('./$houdini').PageData } */
    export let data
    
    $: ({ Info } = data)
</script>

{#if $Info.fetching}
    <Container/>
{:else}
<Container>
    <Panel slot="left">
        <Display id="species-name">
            {$Info.data.species.name}
            <span>no.{$Info.data.species.id}</span>
        </Display>
        <Sprite
            id="species-sprite"
            species={$Info.data.species}
        />
        <Display id="species-flavor_text">
            {$Info.data.species.flavor_text}
        </Display>
    </Panel>
    <Panel slot="right">
        <nav>
            <a href={$Info.data.species.id - 1} disabled={$Info.data.species.id <= 1}>
                previous
            </a>
            <a href={$Info.data.species.id + 1} disabled={$Info.data.species.id >= 151}>
                next
            </a>
        </nav>
        <div id="species-evolution-chain">
            {#each $Info.data.species.evolution_chain as form, i}
                <SpeciesPreview species={form} number={i + 1} />
            {/each}
            <!-- if there are less than three species in the chain, leave a placeholder behind -->
            {#each Array.from({ length: 3 - $Info.data.species.evolution_chain?.length }) as _, i}
                <SpeciesPreviewPlaceholder number={$Info.data.species.evolution_chain.length + i + 1} />
            {/each}
        </div>
    </Panel>
</Container>
{/if}
