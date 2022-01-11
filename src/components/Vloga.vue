<template>
  <div class="accordion-item">
    <h2 class="accordion-header" :id="'headingOne' + id">
      <button class="accordion-button" type="button" data-bs-toggle="collapse" :data-bs-target="'#collapseOne' + id" aria-expanded="false" :aria-controls="'collapseOne' + id">
        <span>{{ vloga.name + " " + vloga.surname }}</span>
      </button>
    </h2>
    <div :id="'collapseOne' + id" class="accordion-collapse collapse" :aria-labelledby="'headingOne' + id" data-bs-parent="#accordionExample">
      <div class="accordion-body">
        <ul>
          <li>Rojstvo: {{ vloga.birth }}</li>
          <li>Država: {{ vloga.country }}</li>
          <li>Izobrazba: {{ vloga.education }}</li>
          <li>EMSO: {{ vloga.emso }}</li>
          <li>Spol: {{ vloga.gender }}</li>
          <li>Hišna št.: {{ vloga.houseNum }}</li>
          <li>Kraj: {{ vloga.place }}</li>
          <li>Pošta: {{ vloga.postal }}</li>
          <li>Ulica: {{ vloga.street }}</li>
        </ul>
        <button class="btn btn-danger m-3" @click="Rejected" v-if="vloga.rod.length == 0">Zavrni</button><div class="fw-bold" v-else>Vloga je bila že obravnavana</div>
        <button class="btn btn-success" @click="SubmitVloga" v-if="vloga.rod == '' ">Sprejmi</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Vloga',
    data() {
        return {
            idVloge: null,
            itemVloga: this.vloga
        }
    },
    mounted() {
        
    },
    methods: {
      SubmitVloga() {
        let tempVloge = localStorage.getItem("vloge")
                let parsedVloge = JSON.parse(tempVloge);
                let arr = [];

                for (let i = 0; i < parsedVloge.length; i++) {
                    const x = parsedVloge[i];
                    if(this.vloga.name == x.name) {
                        arr.push({ name: this.vloga.name, surname: this.vloga.surname, birth: this.vloga.birth, country: this.vloga.country, date: this.date, education: this.vloga.education, emso: this.vloga.emso, gender: this.vloga.gender, houseNum: this.vloga.houseNum, mentor: this.mentor, place: this.vloga.place, postal: this.vloga.postal, rod: this.rod, street: this.vloga.street, isAccepted: true })
                    }
                    else {
                        arr.push({ name: x.name, surname: x.surname, birth: x.birth, country: x.country, date: this.date, education: x.education, emso: x.emso, gender: x.gender, houseNum: x.houseNum, mentor: this.mentor, place: x.place, postal: x.postal, rod: this.rod, street: x.street })
                    }
                }

                localStorage.setItem("vloge", JSON.stringify(arr));
        this.$router.push( { name: 'Additional', params: { id: this.vloga.name } } );
      },
      Rejected() {
        let tempVloge = localStorage.getItem("vloge")
                let parsedVloge = JSON.parse(tempVloge);
                let arr = [];

                for (let i = 0; i < parsedVloge.length; i++) {
                    const x = parsedVloge[i];
                    if(this.vloga.name == x.name) {
                        arr.push({ name: this.vloga.name, surname: this.vloga.surname, birth: this.vloga.birth, country: this.vloga.country, date: this.date, education: this.vloga.education, emso: this.vloga.emso, gender: this.vloga.gender, houseNum: this.vloga.houseNum, mentor: this.mentor, place: this.vloga.place, postal: this.vloga.postal, rod: this.rod, street: this.vloga.street, isAccepted: false })
                    }
                    else {
                        arr.push({ name: x.name, surname: x.surname, birth: x.birth, country: x.country, date: this.date, education: x.education, emso: x.emso, gender: x.gender, houseNum: x.houseNum, mentor: this.mentor, place: x.place, postal: x.postal, rod: this.rod, street: x.street })
                    }
                }

                localStorage.setItem("vloge", JSON.stringify(arr));

        this.$router.push( { name: 'Edit', params: { id: this.vloga.name } } );
      }
    },
    props: {
        id: Number,
        vloga: Object
    }
}
</script>