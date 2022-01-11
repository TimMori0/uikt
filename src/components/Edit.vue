<template>
    <div>
        <h3 class="mt-4">Popravki</h3>
        <div class="container mt-3">
          <h4 class="text-end m-3">Pozdravljeni, <b>Admin</b>!</h4>
            <div class="row justify-content-center align-items-center text-start">
                <div class="col-md-6">
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
                </div>
            </div>
            <div class="row justify-content-center align-items-center text-start mt-3">
                <div class="col-md-6">
                      <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Ime</label>
                        <input v-model="vloga.name" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputPassword1" class="form-label">Priimek</label>
                        <input v-model="vloga.surname" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Rojstni dan</label>
                        <input v-model="vloga.birth" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputPassword1" class="form-label">Država</label>
                        <input v-model="vloga.country" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Izobrazba</label>
                        <input v-model="vloga.education" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                     <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">EMSO</label>
                        <input v-model="vloga.emso" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputPassword1" class="form-label">Spol</label>
                        <input v-model="vloga.gender" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Hišna Št.</label>
                        <input v-model="vloga.houseNum" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Place</label>
                        <input v-model="vloga.place" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputPassword1" class="form-label">Poštna št.</label>
                        <input v-model="vloga.postal" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Street</label>
                        <input v-model="vloga.street" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Rod</label>
                        <input v-model="vloga.rod" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3 d-none">
                        <label for="exampleInputPassword1" class="form-label">Datum Začetka Opravljanja</label>
                        <input v-model="vloga.date" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3 d-none">
                        <label for="exampleInputEmail1" class="form-label">Mentor</label>
                        <input v-model="vloga.mentor" type="text" class="form-control" id="exampleInputEmail1" required>
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
    name: 'Edit',
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
                let tempVloge = localStorage.getItem("vloge")
                let parsedVloge = JSON.parse(tempVloge);
                let arr = [];

                for (let i = 0; i < parsedVloge.length; i++) {
                    const x = parsedVloge[i];
                    if(this.$router.currentRoute._value.params.id == x.name) {
                        arr.push({ name: this.vloga.name, surname: this.vloga.surname, birth: this.vloga.birth, country: this.vloga.country, date: this.date, education: this.vloga.education, emso: this.vloga.emso, gender: this.vloga.gender, houseNum: this.vloga.houseNum, mentor: this.mentor, place: this.vloga.place, postal: this.vloga.postal, rod: this.rod, street: this.vloga.street, isAccepted: false })
                    }
                    else {
                        arr.push({ name: x.name, surname: x.surname, birth: x.birth, country: x.country, date: this.date, education: x.education, emso: x.emso, gender: x.gender, houseNum: x.houseNum, mentor: this.mentor, place: x.place, postal: x.postal, rod: this.rod, street: x.street })
                    }
                }

                localStorage.setItem("vloge", JSON.stringify(arr));
                this.$router.push( { name: 'Finish' } )
        }
    }
}
</script>