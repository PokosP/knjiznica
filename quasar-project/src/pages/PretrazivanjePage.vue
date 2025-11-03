<template>
  <q-page padding>
    <div class="q-pa-md q-gutter-md">
      <q-input
        v-model="searchTerm"
        label="Upišite pojam za pretraživanje"
        clearable
        outlined
        @keyup.enter="searchBooks"
      >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>

      <div class="row q-gutter-x-md">
        <q-checkbox
          v-model="searchByTitle"
          label="Pretraživanje po Naslovu"
          color="primary"
        />
        <q-checkbox
          v-model="searchByAuthor"
          label="Pretraživanje po Autoru"
          color="secondary"
        />
      </div>

      <q-btn
        label="Traži"
        color="positive"
        icon="send"
        @click="searchBooks"
        :disable="!searchTerm || (!searchByTitle && !searchByAuthor)"
      />
    </div>

    <q-separator spaced />

    <h5 v-if="loading" class="text-center text-primary">
      Pretraživanje u tijeku...
    </h5>

    <q-table
      v-else-if="books.length"
      title="Rezultati pretrage"
      :rows="books"
      :columns="columns"
      row-key="id"
      :pagination="{ rowsPerPage: 10 }"
      separator="horizontal"
      flat
      bordered
    />

    <p v-else-if="searched" class="text-center text-negative">
      Nema rezultata za zadani pojam.
    </p>
    <p v-else class="text-center text-grey">
      Unesite pojam i kliknite 'Traži'.
    </p>
  </q-page>
</template>

<script>
// Pretpostavljena lista knjiga za simulaciju
const mockBooks = [
  { id: 1, title: "Zločin i kazna", author: "Fjodor Dostojevski", year: 1866 },
  { id: 2, title: "Ana Karenjina", author: "Lav Tolstoj", year: 1877 },
  {
    id: 3,
    title: "Sto godina samoće",
    author: "Gabriel García Márquez",
    year: 1967,
  },
  {
    id: 4,
    title: "Mali Princ",
    author: "Antoine de Saint-Exupéry",
    year: 1943,
  },
  {
    id: 5,
    title: "Dostojevski u Japanu",
    author: "Haruki Murakami",
    year: 2021,
  },
];

export default {
  name: "PretrazivanjePage",
  data() {
    return {
      searchTerm: "", // Vrijednost iz input polja
      searchByTitle: true, // Stanje checkboxa za naslov
      searchByAuthor: true, // Stanje checkboxa za autora
      books: [], // Popis pronađenih knjiga (rezultati)
      loading: false, // Indikator učitavanja
      searched: false, // Indikator da je pretraga pokrenuta

      // Definicija kolona za q-table
      columns: [
        {
          name: "title",
          required: true,
          label: "Naslov",
          align: "left",
          field: (row) => row.title,
          sortable: true,
        },
        {
          name: "author",
          label: "Autor",
          align: "left",
          field: "author",
          sortable: true,
        },
        {
          name: "year",
          label: "Godina izdavanja",
          align: "center",
          field: "year",
          sortable: true,
        },
      ],
    };
  },
  methods: {
    searchBooks() {
      // Izbjegavanje pretrage ako nema pojma ili nije odabran način pretrage
      if (!this.searchTerm || (!this.searchByTitle && !this.searchByAuthor)) {
        return;
      }

      this.loading = true; // Pokreni loading indikator
      this.searched = true; // Označi da je pretraga pokrenuta
      this.books = []; // Resetiraj prethodne rezultate

      // Simulacija asinkronog poziva (npr. API poziv)
      setTimeout(() => {
        const term = this.searchTerm.toLowerCase();

        // Logika filtriranja
        const results = mockBooks.filter((book) => {
          let match = false;

          if (this.searchByTitle) {
            match = match || book.title.toLowerCase().includes(term);
          }

          if (this.searchByAuthor) {
            match = match || book.author.toLowerCase().includes(term);
          }

          return match;
        });

        this.books = results;
        this.loading = false; // Zaustavi loading indikator
      }, 1000); // Odgoda od 1 sekunde za simulaciju učitavanja
    },
  },
};
</script>

<style scoped>
/* Opcionalno dodajte stilove ako je potrebno */
.q-page {
  max-width: 900px;
  margin: 0 auto;
}
</style>
