<!-- Please remove this file from your project -->
<template>
  <div
    class="
      relative
      flex
      items-top
      justify-center
      min-h-screen
      bg-gray-100
      sm:items-center sm:pt-0
    "
  >
    <link
      href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css"
      rel="stylesheet"
    />
    <div class="container col-offset-3 col-6">
      <h2 class="text-2xl leading-7 font-semibold mb-4">Welcome to Apace</h2>
      <div
        class="alert alert-danger d-flex align-items-center"
        role="alert"
        v-if="error"
      >
        <svg
          class="bi flex-shrink-0 me-2"
          width="24"
          height="24"
          role="img"
          aria-label="Danger:"
        >
          <use xlink:href="#exclamation-triangle-fill" />
        </svg>
        <div>{{ error }}</div>
      </div>
      <form class="mt-8">
        <div class="mb-3">
          <label class="form-label"> Name </label>
          <input type="text" class="form-control" v-model="form.name" />
        </div>
        <div class="mb-3">
          <label class="form-label">Email</label>
          <input type="email" class="form-control" v-model="form.email" />
        </div>
        <div class="mb-3">
          <label class="form-label">Country</label>
          <select class="form-control" v-model="form.country">
            <option selected>--select--</option>
            <option value="NG">Nigeria</option>
            <option value="GH">Ghana</option>
          </select>
        </div>
        <div class="mb-3">
          <label class="form-label">Password</label>
          <input type="password" class="form-control" v-model="form.password" />
        </div>
        <button
          type="button"
          class="btn btn-primary"
          v-on:click="onSubmit"
          :disabled="disabled"
        >
          Submit
        </button>
        <hr class="mt-4 mb-4" />
        <NuxtLink to="/" class="pt-8"> Login </NuxtLink>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Register",
  data: function () {
    return {
      form: {
        name: "",
        email: "",
        country: "",
        password: "",
      },
      disabled: false,
      error: null,
    };
  },

  methods: {
    async onSubmit() {
      try {
        this.disabled = true;
        let response = await this.$axios.$post("/register", this.form);
        if (response.status == "error") {
          this.error = response.message;
        } else {
          this.$router.push("/login");
        }
        this.disabled = false;
      } catch (err) {
        console.log(err);
        this.disabled = false;
        this.error = err;
      }
    },
  },
};
</script>
