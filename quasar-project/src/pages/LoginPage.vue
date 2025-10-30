<template>
  <q-page class="flex flex-center bg-grey-3">
    <q-card class="q-pa-lg shadow-10" style="width: 450px">
      <q-card-section class="text-center">
        <q-icon name="account_circle" size="6em" color="primary" />
        <div class="text-h5 text-primary q-mt-md">Prijava</div>
        <div class="text-subtitle2 text-grey">Unesite svoje vjerodajnice</div>
      </q-card-section>

      <q-card-section>
        <q-form @submit="onSubmit" class="q-gutter-md">
          <q-input
            v-model="username"
            label="Korisničko ime"
            lazy-rules
            :rules="[
              (val) =>
                (val && val.length > 0) || 'Molimo unesite korisničko ime',
            ]"
            outlined
            dense
            color="primary"
          >
            <template v-slot:prepend>
              <q-icon name="person" />
            </template>
          </q-input>

          <q-input
            v-model="password"
            label="Lozinka"
            lazy-rules
            :rules="[
              (val) => (val && val.length > 0) || 'Molimo unesite lozinku',
            ]"
            outlined
            dense
            type="password"
            color="primary"
          >
            <template v-slot:prepend>
              <q-icon name="lock" />
            </template>
          </q-input>

          <div class="q-mt-xl">
            <q-btn
              label="Potvrdi"
              type="submit"
              color="primary"
              class="full-width q-py-sm"
              icon="login"
              :loading="loading"
            />
          </div>

          <div v-if="error" class="text-negative text-center q-mt-md">
            {{ error }}
          </div>
        </q-form>
      </q-card-section>

      <q-card-actions align="center">
        <q-btn
          flat
          dense
          label="Zaboravili ste lozinku?"
          color="grey"
          size="sm"
        />
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: "LoginPage",
  data() {
    return {
      username: "",
      password: "",
      loading: false,
      error: null,
    };
  },
  methods: {
    onSubmit() {
      this.error = null;
      this.loading = true;

      // Simulacija API poziva
      setTimeout(() => {
        if (this.username === "korisnik" && this.password === "tajna") {
          this.$q.notify({ type: "positive", message: "Uspješna prijava!" });
          // Ovdje ide this.$router.push('/');
        } else {
          this.error = "Neispravno korisničko ime ili lozinka.";
          this.$q.notify({ type: "negative", message: "Prijava neuspješna." });
        }
        this.loading = false;
      }, 1500);
    },
  },
};
</script>

<style scoped>
/* Opcionalni stilovi */
</style>
