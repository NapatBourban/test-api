<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
const UserData = ref([]);
const url = ref("https://api.opensea.io/api/v1/assets?format=json");
function buttonclik() {
  axios
    .get(url.value)
    .then((response) => {
      UserData.value = response.data.assets;
    })
    .catch((err) => {
      console.log(err);
    });
}

onMounted(() => {
  buttonclik();
});
</script>
<template>
  <div class="container">
    <div class="row">
      <div class="col-5 m-5" v-for="usedata in UserData">
        <div class="card mb-3" style="max-width: 540px; display: grid">
          <div class="row g-0">
            <div class="col-md-4">
              <img
                :src="usedata.image_thumbnail_url"
                class="img-fluid rounded-start"
                alt="..."
                style="width: 350px; height: 250px"
              />
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h3>ID: {{ usedata.id }}</h3>
                <h5 class="card-title">Name : {{ usedata.name }}</h5>
                <p class="card-text">
                  Type : {{ usedata.asset_contract.asset_contract_type }} <br />Date :
                  {{ usedata.asset_contract.created_date }}

                  <br /><a
                    :href="usedata.permalink"
                    class="d-flex justify-content-center mt-5"
                    ><svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="25"
                      height="25"
                      fill="currentColor"
                      class="bi bi-basket2-fill"
                      viewBox="0 0 16 16"
                    >
                      <path
                        d="M5.929 1.757a.5.5 0 1 0-.858-.514L2.217 6H.5a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h.623l1.844 6.456A.75.75 0 0 0 3.69 15h8.622a.75.75 0 0 0 .722-.544L14.877 8h.623a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-1.717L10.93 1.243a.5.5 0 1 0-.858.514L12.617 6H3.383L5.93 1.757zM4 10a1 1 0 0 1 2 0v2a1 1 0 1 1-2 0v-2zm3 0a1 1 0 0 1 2 0v2a1 1 0 1 1-2 0v-2zm4-1a1 1 0 0 1 1 1v2a1 1 0 1 1-2 0v-2a1 1 0 0 1 1-1z"
                      /></svg
                  ></a>
                </p>
                <p class="card-text">
                  <small class="text-muted">{{ UserData.permalink }}</small>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
