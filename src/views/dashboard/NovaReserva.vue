<template>
    <vee-form @submit="save" :validation-schema="schema" v-slot="{ errors }">
      <div class="row g-2">
        <div class="col-md-4">
          <label for="nome">Nome</label>
          <vee-field name="nome" class="form-control" v-model="reserva.nome" />
          <span class="text-danger" v-text="errors.nome" v-show="errors.nome"></span>
        </div>

        <div class="col-3">
          <label for="">Data Reserva</label>          
          <vee-field type="date" name="dataReserva" class="form-control" v-model="reserva.dataReserva" />
          <span class="text-danger" v-text="errors.dataReserva" v-show="errors.dataReserva"></span>          
        </div>

        <div class="col-3">
          <label for="">Hora de Entrada</label>
          <vee-field type="time" name="horaEntrada" class="form-control" v-model="reserva.horaEntrada" />
          <span class="text-danger" v-text="errors.horaEntrada" v-show="errors.horaEntrada"></span>          
        </div>

        <div class="col-2">
          <label for="">Qtd. Horas</label>
          <vee-field type="number" name="qtdHoras" class="form-control" v-model="reserva.qtdHoras" />
          <span class="text-danger" v-text="errors.horaEntrada" v-show="errors.qtdHoras"></span>
        </div>      

        <div class="col-4">
          <label for="">Placa</label>
          <vee-field name="placa" class="form-control" v-model="reserva.placa" />
          <span class="text-danger" v-text="errors.placa" v-show="errors.placa"></span>
        </div>

        <div class="col-4">
          <label for="">Modelo</label>
          <vee-field name="modelo" class="form-control" v-model="reserva.modelo" />
          <span class="text-danger" v-text="errors.modelo" v-show="errors.modelo"></span>
        </div>

        <div class="col-4">
          <label for="">Ano</label>
          <vee-field type="number" name="ano" class="form-control" v-model="reserva.ano" />
          <span class="text-danger" v-text="errors.ano" v-show="errors.ano"></span>
        </div>
  
        <div class="col-12">
          <button type="submit" class="btn btn-primary" style="margin-right: 5px">Save</button>
          <button type="button" class="btn btn-danger" @click="clear">Limpar</button>
        </div>
      </div>
    </vee-form>

    <div class="text-center">
      <router-link to="/reserva/lista">Lista Reserva</router-link>
    </div>
</template>

<script>
    import { Form, Field, defineRule } from 'vee-validate';
    export default {
        components: {
            'vee-form': Form,
            'vee-field': Field
        },
        data() {
            defineRule("dataSuperior", value => {
                if (new Date(value + ` ${this.reserva.horaEntrada}:00`) < new Date()) {
                    return "Data deve ser posterior a data atual"
                }
                return true;  
            });

            defineRule("required", value => {
                if (!value || value.length === 0) {
                    return "Campo obrigatório"
                }

                return true;
            });

            defineRule("placaValida", value => {
                let regexp = /^[a-zA-Z]{3}-[0-9]{1}[a-zA-Z0-9]{1}[0-9]{2}$/
                
                if (!regexp.test(value)) {
                    return "Placa inválida!"
                }
                return true;
            });

            const schema = {
                nome: "required",
                dataReserva: "required|dataSuperior",
                horaEntrada: "required",
                qtdHoras: "required",
                placa: "required|placaValida",
                modelo: "required",
                ano: "required"
            }

            return {
                schema,
                reserva: {}
            }
        },
        methods: {
            save() {       
                this.reserva = {};
            },
            clear() {
                this.reserva = {};  
            }
        }
    }
</script>