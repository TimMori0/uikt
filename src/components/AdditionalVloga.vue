<template>
    <div>
        <h3 class="mt-4">Zadnji korak</h3>
        <div class="container mt-3">
          <h4 class="text-end m-3">Pozdravljeni, <b>Admin</b>!</h4>
            <div class="row justify-content-center align-items-center text-start">
                <div class="col-md-6">
                    <ul>
                        <li>Ime: {{ vloga.name }}</li>
                        <li>Priimek: {{ vloga.surname }}</li>
                        <li>Rojstni dan: {{ vloga.birth }}</li>
                        <li>Država: {{ vloga.country }}</li>
                        <li>Izobrazba: {{ vloga.education }}</li>
                        <li>EMSO: {{ vloga.emso }}</li>
                        <li>Spol: {{ vloga.gender }}</li>
                        <li>Hišna Št.{{ vloga.houseNum }}</li>
                        <li>Kraj: {{ vloga.place }}</li>
                        <li>Poštna Št.: {{ vloga.postal }}</li>
                        <li>Ulica: {{ vloga.street }}</li>
                    </ul>
                </div>
            </div>
            <div class="row justify-content-center align-items-center text-start mt-3">
                <div class="col-md-6">
                      <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Rod</label>
                        <input v-model="rod" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Datum Začetka Opravljanja</label>
                        <input v-model="date" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Mentor</label>
                        <input v-model="mentor" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div v-if="isEmpty">
                          <p class="text-danger">Podatki niso napolnjeni!</p>
                      </div>
                      <div class="text-end"><button class="btn btn-secondary" @click="SubmitData">Obdelaj in pošlji!</button></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AdditionalVloga',
    data() {
        return {
            vloga: {},
            rod: '',
            date: '',
            mentor: '',
            isEmpty: false
        };
    },
    mounted() {
        let tempVloge = localStorage.getItem("vloge")
        this.parsedVloge = JSON.parse(tempVloge);
        this.parsedVloge.forEach(x => {
            if(this.$router.currentRoute._value.params.id == x.name) {
                console.log(x);
                this.vloga = x;
            }
        })
    },
    methods: {
        SubmitData() {
            if (this.rod != '' && this.date != '' && this.mentor != '') {
                let tempVloge = localStorage.getItem("vloge")
                let parsedVloge = JSON.parse(tempVloge);
                let arr = [];

                for (let i = 0; i < parsedVloge.length; i++) {
                    const x = parsedVloge[i];
                    if(this.$router.currentRoute._value.params.id == x.name) {
                        arr.push({ name: x.name, surname: x.surname, birth: x.birth, country: x.country, date: this.date, education: x.education, emso: x.emso, gender: x.gender, houseNum: x.houseNum, mentor: this.mentor, place: x.place, postal: x.postal, rod: this.rod, street: x.street, isAccepted: true })
                    }
                    else {
                        arr.push({ name: x.name, surname: x.surname, birth: x.birth, country: x.country, date: this.date, education: x.education, emso: x.emso, gender: x.gender, houseNum: x.houseNum, mentor: this.mentor, place: x.place, postal: x.postal, rod: this.rod, street: x.street })
                    }
                }

                localStorage.setItem("vloge", JSON.stringify(arr));
                this.$router.push( { name: 'Preview' } )
            }
            else {
                this.isEmpty = true;
            }
        }
    }
}
</script>