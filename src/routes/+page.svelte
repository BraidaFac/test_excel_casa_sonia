<script lang="ts">
    import { onMount } from 'svelte';
    import { Table, tableMapperValues } from '@skeletonlabs/skeleton';
    import type { Tab, TableSource } from '@skeletonlabs/skeleton';

    async function getRows() {
        const response = await fetch('Listado.csv');
        const data = await response.text();
        const rows = data.split('\n').slice(2);
        const array = rows.map((row,i) => {
            const columns = row.split(';');
            return {
                id: i,
                codigo: columns[0],
                descripcion: columns[1],
                marca: columns[2],
                tipo_articulo: columns[3],
                clase: columns[4],
                detalle : columns[5],
                activo : columns[6],
                stock_negativo: columns[7],
                fecha_vencimiento: columns[8],
                certificado_calidad: columns[9],
                codigo_barra: columns[10],
                fecha_alta: columns[11], 
                publicado_web: columns[12],
                destacado_web : columns[13],   
            }
        });
       const tableSource = {
        	head: ['Id','Codigo', 'Descripcion', 'Marca', 'Tipo Articulo', 'Clase', 'Detalle', 'Activo', 'Stock Negativo', 'Fecha Vencimiento', 'Certificado Calidad', 'Codigo Barra', 'Fecha Alta', 'Publicado Web', 'Destacado Web'],
	        body: tableMapperValues(array.slice(0, 10), ['id','codigo', 'descripcion', 'marca', 'tipo_articulo', 'clase', 'detalle', 'activo', 'stock_negativo', 'fecha_vencimiento', 'certificado_calidad', 'codigo_barra', 'fecha_alta', 'publicado_web', 'destacado_web']),
     }
     return tableSource;
    }
    const tableSource =  getRows();
    
    
 
     
    
    
  
</script>
<div>
{#await tableSource}
        <p>Loading...</p>
{:then list}
         <Table source={list} /> 
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

</div>