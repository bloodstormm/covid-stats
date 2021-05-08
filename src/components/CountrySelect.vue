<template>
    <select 
    @change="onChange()"
    v-model='selected' 
    class="mt-10 block dark:bg-gray-700 dark:border-gray-800 w-1/2 mx-auto border rounded-lg p-3 focus:outline-none shadow-lg"
    >
        <option value="0">Selecionar País</option>
        <option v-for="country in countries" :value="country.ID">
            <!-- Nome de todos os paises na API por meio do country.ID -->
            {{ country.Country }}
        </option>
    </select>
</template>

<script>    
export default {
    name: 'CountrySelect',
    props: ['countries'],
    data() {
        return {
            selected: 0
        }
    },
    methods: {
        onChange() {
            const country = this.countries.find((item) => item.ID === this.selected)

            console.log(country);

            this.$emit('get-country', country)
        }
    }
}
</script>