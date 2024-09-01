<template>
    <div class="container mt-5">
      <h2 class="text-center mb-4">Liste des Recettes</h2>
      <table class="table table-hover">
        <thead class="table-success">
          <tr>
            <th>Titre</th>
            <th>Type</th>
            <th class="text-center">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(recette, index) in recettes" :key="index">
            <td>{{ recette.titre }}</td>
            <td>{{ recette.type }}</td>
            <td class="text-center">
              <button
                class="btn btn-info btn-sm me-2"
                @click="store.getRecette(recette)"
                data-bs-toggle="modal"
                data-bs-target="#voirRecetteModal"
              >
                <i class="fas fa-eye"></i>
              </button>
              <button
                class="btn btn-warning btn-sm me-2"
                @click="store.getRecette(recette)"
              >
                <RouterLink to="/modifier">
                  <i class="fas fa-edit"></i>
                </RouterLink>
              </button>
              <button
                class="btn btn-danger btn-sm"
                @click="store.removeRecette(index)"
              >
                <i class="fas fa-trash"></i>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <RouterLink class="btn btn-primary mt-4" to="/ajouter">
        Ajouter une Recette
      </RouterLink>
  
      <div
        class="modal fade"
        id="voirRecetteModal"
        tabindex="-1"
        aria-labelledby="voirRecetteModalTitle"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="voirRecetteModalTitle">Détails de la Recette</h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              <p><strong>Id:</strong> {{ store.recette.id }}</p>
              <p><strong>Titre:</strong> {{ store.recette.titre }}</p>
              <p><strong>Ingrédients:</strong> {{ store.recette.ingredient }}</p>
              <p><strong>Type:</strong> {{ store.recette.type }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { useRecetteStore } from "@/stores/recette";
  import { RouterLink } from "vue-router";
  
  const store = useRecetteStore();
  const recettes = store.recettes;
  </script>
  
  <style scoped>
  i {
    font-size: 12px;
  }
  </style>
  