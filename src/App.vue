<template>
  <v-app>
      <v-container>
        <v-row>
          <v-col class="text-center text-h3" cols="12">
            <span>Тех. поддержка</span>
          </v-col>
          <v-col cols="12">
            <v-form ref="form">
              <v-text-field v-model="data_massage.fio" label="ФИО"></v-text-field>
              <v-text-field
                  label="Телефон"
                  v-model="data_massage.phone"
                  v-mask="'+7 (###) ### ## ##'"
              ></v-text-field>
              <v-text-field
                  label="Email"
                  v-model="data_massage.email"
              ></v-text-field>
              <v-combobox
                  v-model="data_massage.program_project"
                  :items="items_name_program"
                  label="Названия программного продукта"
              ></v-combobox>
              <v-textarea
                  label="Опишите проблему"
                  v-model="data_massage.problem_massage"
              ></v-textarea>
              <v-btn
                  depressed
                  color="success"
                  @click="send_data"
              >
                Отправить запрос
              </v-btn>
            </v-form>
          </v-col>
        </v-row>
      </v-container>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {},

  data: () => ({
    data_massage: {
      fio: '',
      phone:'',
      email:'',
      program_project: '',
      problem_massage: ''
    },
    items_name_program: [
        'Открытый университет',
        'BigBlueButton',
        'Контингент студентов',
        'Штатное расписание',
        'Расчет часов',
        'Создания дипломов',
        'Тесты'
    ],

  }),
  methods: {
    send_data(){
      const requestOptions = {
        method : "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.data_massage)
      }

      fetch("http://gdd.kbsu.ru/send_email_massage.php", requestOptions)
      .then(response => (console.log(response.data)))
      .catch(error => (console.log(error.response)))
    }
  }
};
</script>
