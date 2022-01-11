<template>
<div>
  <div class="d-flex flex-column min-vh-100 justify-content-center align-items-center">
          <div class="card">
              <div class="card-body ms-5 me-5 mt-3 mb-4">
                  <h4 class="card-title fw-bold customFontColor mb-4">PRIJAVA</h4>
                  <p class="mb-4 text-muted ms-5 me-5 mb-5">Vpišite vaše uporabniško ime in geslo</p>
                  <form @submit="isAdmin()">
                      <div class="input-group mb-3">
                          <input v-model="username" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default" placeholder="Uporabniško ime" id="priimek" required>
                      </div>
                      <div class="input-group mb-3">
                          <input v-model="password" type="password" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default" placeholder="Geslo" id="geslo" required>
                      </div>
                      <button type="submit" class="mt-4 mb-4 mt-5 btn w-100 fw-bold customBackgroundColor">PRIJAVI SE</button>
                  </form>
              </div>
          </div>
    </div>
    <div :class="cookies">
      <div class="row">
        <div class="col-10">
          <div class="bg-secondary">To spletno mesto uporablja piškotke. S piškotki zagotavljamo boljšo uporabniško izkušnjo, enostavnejši pregled vsebin, analizo uporabe, oglasne sisteme in funkcionalnosti. S klikom na »Strinjam se« dovoljuješ vse namene obdelave. Več o piškotkih lahko prebereš <a href="/cookies" class="text-white">TUKAJ</a></div>
        </div>
        <div class="col-2 text-end p-3">
          <button class="btn btn-primary" @click="Close()">SPREJMEM</button>
          <button class="btn btn-danger" @click="Close()">ZAVRNEM</button>
        </div>
      </div>
    </div>
    <div :class="cookies">
      <div class="row">
        <div class="col-10">
          <div class="bg-secondary">Uporabljamo splošne pogoje uporabe tega spletnega mesta, zato prosim, da ga skrbno preberete.<a href="/terms" class="text-white">TUKAJ</a></div>
        </div>
        <div class="col-2 text-end p-3">
          <button class="btn btn-primary" @click="Close()">SPREJMEM</button>
          <button class="btn btn-danger" @click="Close()">ZAVRNEM</button>
        </div>
      </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      username: '',
      password: '',
      vloge: [],
      cookies: 'container-fluid bg-secondary text-white mb-1'
    };
  },
  methods: {
    isAdmin() {
      if (this.username == localStorage.getItem("up_ime_admin") && this.password == localStorage.getItem("pass_admin")) {
        this.$router.push( { path: 'Preview' })
      }
      else if (this.username == localStorage.getItem("up_ime_user") && this.password == localStorage.getItem("pass_user")) {
        this.$router.push( { path: 'UserVloga' })
      }
    },
    Close() {
      this.cookies = 'd-none';
    }
  },
  mounted() {
    let tempVloge = localStorage.getItem("vloge")
    let parsedVloge = JSON.parse(tempVloge);
    
      if(parsedVloge.length == 0) {
        localStorage.setItem("vloge", JSON.stringify(this.vloge));
      }

    localStorage.setItem("up_ime_admin", "admin");
    localStorage.setItem("pass_admin", "admin");

    localStorage.setItem("up_ime_user", "user");
    localStorage.setItem("pass_user", "user");
  },
}
</script>