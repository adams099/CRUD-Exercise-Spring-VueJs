<template>
    <div>
        <router-link to="/" v-show="!success">
            <button class="btn btn-primary my-3 ml-3">Back</button>
        </router-link>
        <div class="d-flex justify-content-around">
            <form @submit.prevent="inputStudents" v-show="!success"
                class="border border-primary mt-5 col-8 p-5 rounded">
                <h4>Add Student</h4>
                <div class="form-row">
                    <div class="form-group col-md-6">
                        <label for="name">Student Name</label>
                        <input v-model="studentsData.nama" type="text" class="form-control" id="name" required />
                    </div>
                    <div class="form-group col-md-6">
                        <label for="softskill">Soft Skill</label>
                        <input v-model="studentsData.soft_skill" type="text" class="form-control" id="softskill"
                            required />
                    </div>
                </div>
                <div class="form-group">
                    <div class="form-row">
                        <div class="form-group col-md-3">
                            <label for="age">Student Age</label>
                            <input v-model="studentsData.umur" type="number" class="form-control" id="age" required />
                        </div>
                        <div class="form-group col-md-3">
                            <label for="gender">Gender</label>
                            <select v-model="studentsData.jenis_kelamin" id="gender" class="form-control">
                                <option selected disabled value="">Choose...</option>
                                <option id="male">Male</option>
                                <option id="female">Female</option>
                            </select>
                        </div>
                        <div class="form-group col-md-6">
                            <label for="hardskill">Hard Skill</label>
                            <input v-model="studentsData.hard_skill" type="text" class="form-control" id="hardskill"
                                required />
                        </div>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group col-md-6">
                        <label for="email">Student Email</label>
                        <input v-model="studentsData.email" type="email" class="form-control" id="email" required />
                    </div>
                    <div class="form-group col-md-6">
                        <label for="interest">Interest</label>
                        <select id="interest" class="form-control" v-model="studentsData.interest">
                            <option selected disabled value="">Choose...</option>
                            <option id="datascience">Data Science</option>
                            <option id="network">Network</option>
                            <option id="webfrontend">Web Frondend</option>
                            <option id="webbackend">Web Backend</option>
                            <option id="mobileapp">Mobile App</option>
                        </select>
                    </div>
                </div>

                <div class="form-group">
                    <label for="selfdescriptions">Self Descriptions</label>
                    <textarea v-model="studentsData.deskripsi_diri" class="form-control" id="selfdescriptions"
                        rows="3"></textarea>
                </div>
                <button type="submit" class="btn btn-primary">{{ buttonValue }}</button>
            </form>

            <Success v-show="success"></Success>
        </div>
    </div>
</template>

<script>
import Success from "@/components/Success.vue";
import StudentsServices from "@/services/StudentServices";

export default {
    name: "FormCom",

    components: {
        Success,
    },

    data() {
        return {
            studentsData: {
                deskripsi_diri: null,
                email: null,
                hard_skill: null,
                interest: "",
                jenis_kelamin: "",
                nama: null,
                soft_skill: null,
                umur: null,
            },
            success: false,
            buttonValue: "Submit"
        };
    },

    methods: {
        inputStudents() {
            let data = this.studentsData;
            let id = this.$route.params.id;
            let route = this.$route.fullPath;
            if (route === "/add") {
                StudentsServices.create(data)
                    .then((response) => {
                        console.log(response.data);
                        this.success = true;
                    })
                    .catch((e) => {
                        console.log(e);
                    });
            } else {
                StudentsServices.updateStudents(id, data)
                    .then((response) => {
                        console.log(response.data);
                        this.success = true;
                    })
                    .catch((e) => {
                        console.log(e);
                    });
            }

        },

        getStudentsById() {
            let id = this.$route.params.id;
            if (id > 0) {
                this.buttonValue = "Update";
            }

            StudentsServices.getStudentsById(id)
                .then((response) => {
                    this.studentsData = response.data;
                    console.log(this.studentsData);
                })
                .catch((e) => {
                    console.log(e);
                });
        },
    },

    mounted() {
        if ((this.$route.params.id > 0)) {
            this.getStudentsById();
        }
    },
};
</script>

<style>

</style>