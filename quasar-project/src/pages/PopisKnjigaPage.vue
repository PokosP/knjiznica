<template>
  <q-page class="q-pa-md">
    <h5 class="q-mb-lg">Popis knjiga u knjižnici</h5>

    <q-table title="Knjige" :rows="rows" :columns="columns" row-key="id" />
  </q-page>
</template>

<script setup>
// 2. DIO ZA LOGIKU I PODATKE (JAVASCRIPT)

// --- A. DEFINICIJA STUPACA (COLUMNS) ---
// OVDJE UBACUJEM SVOJ NIZ OBJEKATA (ali prilagođen za knjige!)
const columns = [
  {
    name: "id",
    label: "ID",
    field: "id",
    style: { fontSize: "14px" },
    headerStyle: { fontSize: "16px", fontWeight: "bold" },
  },
  {
    name: "naslov",
    label: "Naslov knjige",
    field: "naslov",
    style: { fontSize: "14px" },
    headerStyle: { fontSize: "16px", fontWeight: "bold" },
  },
  {
    name: "autor",
    label: "Autor",
    field: "autor",
    style: { fontSize: "14px" },
    headerStyle: { fontSize: "16px", fontWeight: "bold" },
  },
  {
    name: "status",
    label: "Status",
    field: "status",
    style: { fontSize: "14px", fontWeight: "bold" },
    headerStyle: { fontSize: "16px", fontWeight: "bold" },
  },
  {
    name: "opis",
    label: "Opis knjige",
    field: "opis",
    style: { fontSize: "14px" },
    headerStyle: { fontSize: "16px", fontWeight: "bold" },
  },
  {
    name: "slika",
    label: "Slika knjige",
    field: "slika",
    style: { fontSize: "14px" },
    headerStyle: { fontSize: "16px", fontWeight: "bold" },
  },
  // Ovdje bi išle i definicije za opis i sliku...
];

// --- B. DEFINICIJA REDAKA (ROWS) ---
// OVDJE UBACUJEŠ TESTNE PODATKE ZA TABLICU
const rows = [
  {
    id: 1,
    naslov: "Gospodar prstenova",
    autor: "J.R.R. Tolkien",
    status: "slobodna",
    opis: "Znanstveno fantastična izuzetnog sadržaja",
  },
  {
    id: 2,
    naslov: "Zločin i kazna",
    autor: "Fjodor Dostojevski",
    status: "zauzeta",
    opis: "Bavi se temama kao što su dobro i zlo, moral, krivica, iskupljenje i huimanizam",
  },
  // ...dodaj još knjiga za testiranje
];
</script>
