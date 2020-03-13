<template>
    <div>
        <table class="table table-condensed">
            <tbody>
                <tr>
                    <td>
                    <div>
                        <label>Species:</label>
                        {{pokemon.dados.species.name.toUpperCase()}}
                    </div>
                    <hr>
                    <div>
                        <label>Types:</label>
                        <span class="label label-info" style="margin-right: 5px" v-for="(it, idx) in pokemon.dados.types" :key="idx">
                        {{it.type.name.toUpperCase()}}
                        </span>
                    </div>
                    <hr>
                    <div>
                        <label>Abilities:</label>
                        <span class="label label-primary" style="margin-right: 5px" v-for="(ability, idxAbility) in pokemon.dados.abilities" :key="idxAbility">
                        {{ability.ability.name}}
                        </span>
                    </div>
                    <hr>
                    <div>
                        <label>Base Experience:</label>
                        {{pokemon.dados.base_experience}}
                    </div>
                    <hr>
                        <div>
                        <label>Height:</label>
                        {{pokemon.dados.height}}
                    </div>
                    <hr>
                    <div>
                        <label>Weight:</label>
                        {{pokemon.dados.weight}}kg
                    </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    props: ['pokemon'],
}
</script>
<style scoped>
hr{
  margin: 5px 0;
}
</style>
