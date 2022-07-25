<template>
  <div>
    <h3>Registrados</h3>
    <table style='width: 100%' >
        <thead>
            <th style='width: 25%'>Nombre y Apellido</th>
            <th style='width: 25%'>Fecha Nacimiento</th>
            <th style='width: 25%'>Nro</th>
            <th style='width: 25%'>Mail</th>
        </thead>
        <tbody>
            <tr v-for="item in UsuariosRegistrados" :key="item.id" style='text-align: center;'>
                <td style='width: 25%'>{{ item.nombre }}</td>
                <td style='width: 25%'>{{ item.nacimiento }}</td>
                <td style='width: 25%'>{{ item.rifa }}</td>
                <td style='width: 25%'>{{ item.mail }}</td>
            </tr>
        </tbody>
    </table>
    <hr />
  </div>
</template>

<script>
/* eslint-disabled */
export default {
  name: 'TablaRegistro',
  props: {
    UsuariosRegistrados: Array
  }
}
</script>
