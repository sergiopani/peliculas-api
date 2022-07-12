<script>
import Cargador from '../Componentes/Cargador.svelte'
import Grid from '../Componentes/Grid.svelte'
const url = 'https://api.themoviedb.org/3/movie/popular?api_key=<TU API KEY>&language=en-US&page=1'

let promesa = ajax()
let peliculas = []
async function ajax(){
    const res = await fetch(url)
    peliculas = await res.json()
    
    if(res.ok){
        return peliculas.results
    }else{
        throw new Error('No hya conexion con la api')
    }
}
</script>

<h1>Peliculas mas populares del momento</h1>

{#await promesa}
    <div align="center"><Cargador /></div>
{:then peliculas}
    <Grid {peliculas} />
{:catch error}
    <p style="color:red;" >{error}</p>
{/await}