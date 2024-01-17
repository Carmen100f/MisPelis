

<!-- // accedemos a la api VITE_TMDB -->
<script>
    export const API_KEY = import.meta.env.VITE_TMDB_API_KEY;

    let searchTerm = "";
    let movies = [];

    const searchMovis = async () => {
        const response = await fetch(
            `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&query=${searchTerm}&language=es-ES`,
        );
        const data = await response.json();
        movies = data.results;
    };
</script>

<section>
    <div class="movtitel">
        <input bind:value={searchTerm} placeholder="Pelicula a buscar" />

        <button on:click={searchMovis}>Buscar</button>
    </div>

    {#if movies.length > 0}
        <ul>
            <div class="contenedor">
                <div class="contenedor-cards">
                    <!-- buscamos el registro de los datos con movi.id -->
                    {#each movies as movie (movie.id)}
                    <div class="contenedor-card-item">
                        <div class="contenedor-card-item-wrapper">
                            
                            <!--obtenemnos los campos que nos interese indicando el nombre del campo en la API
                            despues de movie. -->

                            <img
                                src={`https://image.tmdb.org/t/p/w200${movie.poster_path}`}
                                alt={movie.title}
                            />
                            <div class="contenedor-info">
                                <div class="info">
                                    <p class="titulo">{movie.title}</p>
                                    <span class="categoria"
                                        >{movie.overview}</span
                                    >
                                </div>
                            </div>
                        </div>
                        <div class="fondo"></div>
                    </div>
                    {/each}
                </div>
            </div>
        </ul>
    {:else if searchTerm.length === 0 }
        <div></div>
    {:else}
        <div class="nopeli">
            <p>no hay pelis</p>
        </div>
    {/if}
</section>

<style>
    input{
        padding: 15px;
        width: 300px;
        border-radius: 10px;
     
        
    }
    button{ 
        color: #fff;
        padding: 15px;
        width: 150px;
        padding-inline: 0px;
        border-radius: 10px;
        margin-left: 10px;
        background-color: rgb(66, 60, 60);
        border-color: #fff;
     
    }
 .movtitel{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    align-items: center;
    height: 350px;
    border-radius: 10px;
   background-image:url(/img/pelisClasicas1.jpg) ;

 }
 .nopeli{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    align-items: center;
    height: 50px;
    border-radius: 10px;
    background-color: black;
    color: #fff;
      

 }
    * {
        font-family: arial;
        
    }

    .contenedor {
        position: relative;
        width: 100%;
        margin: 5 auto;
        transition: all 0.3s ease-out;
        margin-top: 50px;
        margin-bottom: 20px;
        display: -moz-box;
    }

    .contenedor-cards {
        display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
 
    }

    .contenedor-cards .contenedor-card-item {
        /* -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        -o-box-sizing: border-box; */
        box-sizing: border-box;
        width: 25%;
        margin: 1%;
        -webkit-transition: all 0.3s ease-out;
        -o-transition: all 0.3s ease-out;
        transition: all 0.3s ease-out;
        border-radius: 5px;
        cursor: help;
    }

    .contenedor-cards .contenedor-card-item:hover {
        box-shadow: 0 15px 30px rgba(85, 93, 55, 0.906);
        -webkit-transform: translateY(-10px);
        -ms-transform: translateY(-10px);
        -o-transform: translateY(-10px);
        transform: translateY(-10px);
    }

    .contenedor-card-item-wrapper {
        overflow: hidden;
        position: relative !important;
        background: #b0d19e;
        border-radius: 5px;
        height: 100%;
    }

    .contenedor-card-item img {
        max-width: 100%;
        position: relative;
        top: 0;
        -webkit-transition: all 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
        transition: all 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
        border-radius: 5px;
    }

    .contenedor-card-item .contenedor-info {
        position: relative;
        width: 100%;
        /* left: 30%; */
        margin-right: 15%;
        -webkit-transition: all 0.5s cubic-bezier(0.645, 0.045, 0.355, 1);
        transition: all 0.5s cubic-bezier(0.645, 0.045, 0.355, 1);
        background: #00000040;
        height: 100%;
    }

    .contenedor-card-item .contenedor-info .fondo {
        background: -moz-linear-gradient(
            top,
            rgba(0, 0, 0, 0) 0%,
            rgba(0, 0, 0, 0.73) 53%,
            rgba(0, 0, 0, 0.88) 100%
        );
        background: -webkit-linear-gradient(
            top,
            rgba(0, 0, 0, 0) 0%,
            rgba(0, 0, 0, 0.73) 53%,
            rgba(0, 0, 0, 0.88) 100%
        );
        background: linear-gradient(
            to bottom,
            rgba(0, 0, 0, 0) 0%,
            rgba(0, 0, 0, 0.73) 53%,
            rgba(0, 0, 0, 0.88) 100%
        );
        /* filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#00000000', endColorstr='#e0000000',GradientType=0 );
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0; */
    }

    .contenedor-card-item .contenedor-info .info {
        color: #fff;
        position: relative;
        z-index: 500;
        padding: 20px 15px;
        margin: 0px 20px;
    }

    .contenedor-card-item .contenedor-info .info .titulo {
        margin: 0;
        font-size: 20px;
    }

    .contenedor-card-item .contenedor-info .info .categoria {
        display: block;
        font-size: 15px;
    }

    .contenedor-card-item:hover .contenedor-info {
        bottom: 0;
    }

    .contenedor-card-item:hover img {
        top: -30px;
        -webkit-transform: rotate(-5deg) scale(2);
        -ms-transform: rotate(-5deg) scale(2);
        -o-transform: rotate(-5deg) scale(2);
        transform: rotate(-5deg) scale(2);
    }

    @media screen and (max-width: 900px) {
        .contenedor-card-item:hover img {
            top: -30px;
            -webkit-transform: rotate(-5deg) scale(1.3);
            -ms-transform: rotate(-5deg) scale(1.3);
            -o-transform: rotate(-5deg) scale(1.3);
            transform: rotate(-5deg) scale(1.3);
        }

        .contenedor-card-item .contenedor-info {
            bottom: 0;
        }
    }

    @media screen and (max-width: 767px) {
        .contenedor {
            width: 95%;
        }

        .contenedor-cards .contenedor-card-item {
            width: 48%;
            margin: 1%;
        }
    }

    @media screen and (max-width: 550px) {
        .contenedor-cards .contenedor-card-item {
            width: 60%;
            margin: 10px auto;
        }
    }

    @media screen and (max-width: 480px) {
        .contenedor {
            width: 90%;
        }

        .contenedor-cards .contenedor-card-item {
            width: 90%;
        }
    }

    @media screen and (max-width: 400px) {
        .contenedor {
            width: 100%;
        }
    }
</style>
