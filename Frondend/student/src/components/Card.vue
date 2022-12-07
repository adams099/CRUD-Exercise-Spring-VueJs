<template>
  <div>
    <div>
      <router-link to="/add">
        <button class="btn btn-primary my-3 ml-3">Add</button>
      </router-link>
    </div>

    <div>
      <div class="container d-flex flex-wrap justify-content-center">
        <div class="card m-3 col-md-3 col-sm-3" v-for="item in studentData" :key="item.id">
          <div class="card-body">
            <h5 class="card-title mb-3">{{ item.nama }}, {{ item.umur }} years old</h5>

            <p>Email : {{ item.nama }}</p>
            <p>Soft Skill : {{ item.soft_skill }}</p>
            <p>Hard Skill : {{ item.hard_skill }}</p>
            <p>Interest : {{ item.interest }}</p>

            <div class="row">
              <div class="d-flex row mt-3">
                <router-link :to="{ path: '/update/' + item.id }">
                  <button class="btn btn-primary mr-2">Update</button>
                </router-link>
                <router-link to="/">
                  <button class="btn btn-danger" @click="deleteStudents(item.id)">
                    Delete
                  </button>
                </router-link>
                <div>
                  <img class="male" v-if="item.jenis_kelamin == 'Male'" src="../assets/male.png" alt="" />
                  <img class="female" v-else-if="item.jenis_kelamin == 'Female'" src="../assets/female.png" alt="" />
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StudentServices from "@/services/StudentServices.js";

export default {
  name: "CardS",

  data() {
    return {
      studentData: null,
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
            location.reload();
          })
          .catch((e) => {
            console.log(e);
          });
        // this.success = true;
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
.male {
  width: 40px;
  margin-left: 50px;
}

.female {
  width: 30px;
  margin-left: 50px;
}

.btn {
  margin: 5px;
}
</style>>