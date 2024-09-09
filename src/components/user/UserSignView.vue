<template>
  <div>
    <div class="mb-3">
      <input
        type="text"
        id="userid"
        class="form-control"
        placeholder="userid"
        v-model="userData.userid"
      />
    </div>
    <div class="mb-3">
      <input
        type="text"
        id="userpassword"
        class="form-control"
        placeholder="userpassword"
        v-model="userData.password"
      />
    </div>
    <div class="mb-3">
      <input
        type="text"
        id="username"
        class="form-control"
        placeholder="username"
        v-model="userData.username"
      />
    </div>
    <div class="mb-3">
      <input
        type="text"
        id="addr"
        class="form-control"
        placeholder="addr"
        v-model="userData.addr"
      />
    </div>
    <div class="d-flex gap-3 mb-3">      
      <input
        type="text"
        id="latitude"
        class="form-control"
        placeholder="latitude"
        v-model="userData.latitude"
      />     
      <input
        type="text"
        id="longitude"
        class="form-control"
        placeholder="longitude"
        v-model="userData.longitude"
      />
    </div>
    <div class="input-group mb-3">
      <input
        type="file"
        class="form-control"
        id="fileform"
        @change="handleImage"
        accept="image/*"
      />
      <label class="input-group-text" for="fileform">Upload</label>
    </div>

    <div v-if="editData >= 0" class="mb-3">
      <div class="btn btn-primary me-2" @click="[
          editUser(),
          $emit('editdone')]
        ">수정완료</div>
      <div
        class="btn btn-primary"
        @click="[
          editEnd(),
          $emit('editdone')]
        "
      >
        수정취소
      </div>
    </div>
    <div v-else class="btn btn-primary me-2 mb-3" @click="addUser">회원가입</div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import { useStore } from "vuex";

const store = useStore();
const props = defineProps({
  editData: Boolean,
});

watch(
  () => {
    return props.editData;
  },
  () => {
    if(props.editData >= 0){

      fillForm();
    }
  }
);

const userData = ref({
  userid: null,
  password: null,
  username: null,
  addr: null,
  latitude: null,
  longitude: null,
  image: null,
});

const fillForm = () => {
  userData.value.userid = store.state.editData.userid;
  userData.value.password = store.state.editData.password;
  userData.value.username = store.state.editData.username;
  userData.value.addr = store.state.editData.addr;
  userData.value.latitude = store.state.editData.latitude;
  userData.value.longitude = store.state.editData.longitude;
};

const clearform = () => {
  userData.value.userid = null;
  userData.value.password = null;
  userData.value.username = null;
  userData.value.addr = null;
  userData.value.latitude = null;
  userData.value.longitude = null;
  userData.value.image = null;
};

const addUser = () => {
  let uData = {
    userid: userData.value.userid,
    password: userData.value.password,
    username: userData.value.username,
    addr: userData.value.addr,
    latitude: userData.value.latitude,
    longitude: userData.value.longitude,
    image: userData.value.image,
  };
  store.commit("addUser", uData);
  clearform();
};

const editUser = () => {
  let uData = {
    userid: userData.value.userid,
    password: userData.value.password,
    username: userData.value.username,
    addr: userData.value.addr,
    latitude: userData.value.latitude,
    longitude: userData.value.longitude,
    image: userData.value.image,
    index: props.editData,
  };
  store.commit("editUser", uData);
  clearform();
}

const handleImage = (e) => {
  const file = e.target.files[0];
  console.log(file);
  if (file) {
    userData.value.image = URL.createObjectURL(file);
  }
};

const editEnd = () => {
  clearform();
  alert("수정이 취소 됐습니다.");
};
</script>

<style lang="scss" scoped></style>
