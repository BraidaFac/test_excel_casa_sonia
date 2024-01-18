<script lang="ts">
    import { onMount } from 'svelte';
    import { Table, tableMapperValues } from '@skeletonlabs/skeleton';
    import type { Tab, TableSource } from '@skeletonlabs/skeleton';
    let rows : any[] = [];
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
       return array.slice(0, 2500);
    }

    onMount(async ()=>{
        rows = await getRows();
    })
    
 
     
    
    
  
</script>
<div>
{#if rows.length === 0}
        <p>Loading...</p>
{:else }
<table class="table">
			<thead>
				<tr>
					<th>ID</th>
                    <th>Codigo</th>
                    <th>Descripcion</th>
                    <th>Marca</th>
                    <th>Tipo Articulo</th>
                    <th>Clase</th>
                  <!--   <th>Detalle</th>
                    <th>Activo</th>
                    <th>Stock Negativo</th>
                    <th>Fecha Vencimiento</th>
                    <th>Certificado Calidad</th>
                    <th>Codigo Barra</th>
                    <th>Fecha Alta</th>
                    <th>Publicado Web</th>
                    <th>Destacado Web</th> -->
				</tr>
			</thead>
			<tbody>
				{#each rows as item (item.id)}
					<tr>
						<td>{item.id}</td>
                        <td>{item.codigo}</td>
                        <td>{item.descripcion}</td>
                        <td>{item.marca}</td>
                        <td>{item.tipo_articulo}</td>
                        <td>{item.clase}</td>
                        <!-- <td>{item.detalle}</td>
                        <td>{item.activo}</td>
                        <td>{item.stock_negativo}</td>
                        <td>{item.fecha_vencimiento}</td>
                        <td>{item.certificado_calidad}</td>
                        <td>{item.codigo_barra}</td>
                        <td>{item.fecha_alta}</td>
                        <td>{item.publicado_web}</td>
                        <td>{item.destacado_web}</td> -->
					</tr>
				{/each}
			</tbody>
		</table>
{/if }


</div>