<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <h3 class="mb-3">User List</h3>
        <UserListView @editUser="editUser" />
      </div>
      <div class="col-md-6">
        <h3 class="mt-4 mb-3 mt-md-0">User sign</h3>
        <UserSignView :editData="editData" @editdone="editdone" />
      </div>
    </div>

    <div class="row">
      <div class="col-md-6">
        <h3 class="mt-4 mb-3">지도</h3>
        <MapView />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useStore } from "vuex";
import MapView from "../components/user/MapView.vue";
import UserListView from "../components/user/UserListView.vue";
import UserSignView from "../components/user/UserSignView.vue";

const store = useStore();

const editData = ref(-1);

const editUser = (i) => {
  editData.value = i;
};
const editdone = () => {
  editData.value = -1;
};
</script>

<style lang="scss" scoped></style>
