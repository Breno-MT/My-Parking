<template>
    <div class="text-center" v-if="reservas.length === 0">
      Não há reservas cadastradas
    </div>
    <table class="table" v-else>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Data Reserva</th>
          <th>Hora de Entrada</th>
          <th>Qtd Horas</th>
          <th>Placa</th>
          <th>Modelo</th>
          <th>Ano</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="reserva in reservas" :key="reserva.id">
          <td>{{ reserva.nome }}</td>
          <td>{{ reserva.dataReserva }}</td>
          <td>{{ reserva.horaEntrada }}</td>
          <td>{{ reserva.qtdHoras }}</td>
          <td>{{ reserva.placa }}</td>
          <td>{{ reserva.modelo }}</td>
          <td>{{ reserva.ano }}</td>
        </tr>
      </tbody>
    </table>

    <div class="text-center">
      <router-link to="/">Home</router-link>
    </div>

</template>

<script>
export default {
    data() {
        return {
            reservas: []
        }
    }
}
</script>