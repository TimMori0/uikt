<template>
<div class="container">
    <h4 class="text-end m-3">Pozdravljeni, <b>Uporabnik</b>!</h4>
    <div class="row justify-content-center align-items-center text-start">
        <div class="col-md-12">
            <h1 class="mt-4 mb-4">Oddaja Vloge</h1>
            <form @submit="AddVloga()">
              <div class="row">
                  <div class="col-md-4">
                      <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Ime</label>
                        <input v-model="vloga.name" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Spol</label>
                        <input v-model="vloga.gender" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Ulica</label>
                        <input v-model="vloga.street" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Poštna številka</label>
                        <input v-model="vloga.postal" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                  </div>
                  <div class="col-md-4">
                      <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Priimek</label>
                        <input v-model="vloga.surname" type="text" class="form-control" id="exampleInputEmail1" required>
                      </div>
                      <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Datum rojstva</label>
                        <input v-model="vloga.birth" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                        <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Hišna Št.</label>
                        <input v-model="vloga.houseNum" type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" required>
                      </div>
                      <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Kraj</label>
                        <input v-model="vloga.place" type="text" class="form-control" id="exampleInputPassword1" required>
                      </div>
                  </div>
                  <div class="col-md-4">
                      <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">EMŠO</label>
                        <input v-model="vloga.emso" type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                      </div>
                      <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Izobrazba</label>
                        <input v-model="vloga.education" type="text" class="form-control" id="exampleInputPassword1">
                      </div>
                        <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Država</label>
                        <input v-model="vloga.country" type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                      </div>
                      <div class="mb-3">
                        <label for="tt"></label>
                        <div class="m-3"><input type="checkbox" id="tt" required><span> Strinjam se s splošnimi <a href="/terms">pogoji</a> registracije.</span></div>
                      </div>
                  </div>
              </div>
              <div class="row text-end">
                  <div class="col-md-4">
                    <button type="submit" class="btn btn-secondary m-2" @click="Check()">Pregled vlog</button>
                  </div>
                   <div class="col-md-2">
                       <h5 v-if="isSigned" class="m-3 text-success">Vloga podpisana</h5>
                  </div>
                   <div class="col-md-6">
                       <button type="button" class="btn btn-primary m-2" @click="Add()">Dodaj priloge</button>
                       <button type="button" class="btn btn-primary m-2" @click="Sign()">Podpis vloge</button>
                       <button type="submit" class="btn btn-primary m-2">Oddaja vloge</button>
                  </div>
              </div>
            </form>
        </div>
        <div class="col-md-12">
            <h3>Priloge: </h3>
            <ul>
                <li v-for="priloga in priloge" :key="priloga">{{ priloga.filename }}</li>
            </ul>
        </div>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            vloga: {
                name: '',
                gender: '',
                street: '',
                postal: '',
                surname: '',
                birth: '',
                houseNum: '',
                place: '',
                emso: '',
                education: '',
                country: '',
                rod: '',
                date: '',
                mentor: '',
                isAccepted: null
            },
            isSigned: false,
            priloge: [ ],
        }
    },
    methods: {
        Sign() {
            this.isSigned = true;
        },
        Add () {
            this.priloge.push({ filename: 'vlogaDokazilo.pdf' }, { filename: 'dodatno.docx' }, { filename: 'podpis.jpg' });
        },
        AddVloga() {
            let tempVloge = localStorage.getItem("vloge")
            let parsedVloge = JSON.parse(tempVloge);
            parsedVloge.push(this.vloga);
            localStorage.setItem("vloge", JSON.stringify(parsedVloge));
            this.$router.push( { name: 'Success' } )
        },
        Check() {
          this.$router.push( { name: 'Checker' } )
        }
    }
}
</script>

<style scoped>
input[type='file'] {
  color: rgba(0, 0, 0, 0)
}
</style>