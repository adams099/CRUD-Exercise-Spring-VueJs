<template>
  <div>
    <div>
      <router-link to="/add">
        <button class="btn btn-primary my-3 ml-3" v-show="!success">Add</button>
      </router-link>
    </div>

    <div v-if="studentData.length > 0" class="card-container d-flex flex-wrap">
      <div class="col-4 mt-4" v-for="(item) in studentData" :key="item.id" v-show="!success">
        <div class="card p-3 border">
          <h5>{{ item.nama }}, {{ item.umur }} years old.</h5>
          <p>{{ item.deskripsi_diri }}</p>
          <table>
            <tr>
              <td>Email</td>
              <td>: {{ item.email }}</td>
            </tr>
            <tr>
              <td>Soft Skill</td>
              <td>: {{ item.soft_skill }}</td>
            </tr>
            <tr>
              <td>Hard Skill</td>
              <td>: {{ item.hard_skill }}</td>
            </tr>
            <tr>
              <td>Interest</td>
              <td>: {{ item.interest }}</td>
            </tr>
          </table>
          <div class="d-flex justify-content-between mt-3">
            <div>
              <router-link :to="{ path: '/update/' + item.id }">
                <button id="btns" class="btn btn-primary mr-2">Update</button>
              </router-link>
              <router-link to="/">
                <button class="btn btn-danger" @click="deleteStudents(item.id)">
                  Delete
                </button>
              </router-link>
            </div>
            <img v-if="item.jenis_kelamin == 'Male'" :class="item.jenis_kelamin" src="@/assets/male.png" alt="" />
            <img v-else :class="item.jenis_kelamin" src="@/assets/female.png" alt="" />
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <h1 align="center">Tidak ada data yang ditampilkan!</h1>
    </div>
    <center>
      <Success v-show="success" class="text-left mt-5 mb-5" id="successC"></Success>
    </center>
  </div>
</template>

<script>
import StudentServices from "@/services/StudentServices.js";
import Success from "./Success.vue";

export default {
  name: "CardS",

  components: {
    Success
  },

  data() {
    return {
      studentData: null,
      success: false
    };
  },

  // METHOD
  methods: {
    getStudent() {
      StudentServices.getAll()
        .then((response) => {
          this.studentData = response.data;
          console.log(this.studentData);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    deleteStudents(id) {
      if (confirm(`Yakin Ingin menghapus data ini ?`)) {
        StudentServices.deleteStudents(id)
          .then((response) => {
            console.log(response.data);
            this.success = true;
          })
          .catch((e) => {
            console.log(e);
          });
      } else {
        alert("Hapus Dibatalkan");
      }
    },
  },

  mounted() {
    this.getStudent();
  },
};
</script>

<style scoped>
img {
  width: 50px;
  height: auto;
}

.Female {
  width: auto;
  height: 50px;
}

#successC {
  width: 50%;
}
</style>