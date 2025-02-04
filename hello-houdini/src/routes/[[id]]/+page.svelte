<script>
    import { Container, Display, Sprite, Panel } from '~/components'
    
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
            src={$Info.data.species.sprites.front}
            speciesName={$Info.data.species.name}
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
    </Panel>
</Container>
{/if}
