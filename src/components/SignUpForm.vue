<template>
  <form
    class="bg-white my-[30px] max-w-[500px] mx-auto rounded-[10px] pt-[60px] pb-[30px] px-[40px]" @submit.prevent="handleSubmit"
  >
    <div class="flex flex-col gap-6">
      <label class="text-[#aaa] text-[15px] font-bold tracking-[1px] uppercase"
        >Email:</label
      >
      <input
        type="email"
        class="border-b border-gray-300 text-[#555] focus:outline-none"
        v-model="email"
      />

      <label class="text-[#aaa] text-[15px] font-bold tracking-[1px] uppercase"
        >Password:</label
      >
      <div class="flex relative">
        <input
          :type="isPassword ? 'password' : 'text'"
          class="border-b border-gray-300 text-[#555] focus:outline-none w-full"
          v-model="password"
        />
        <p
          class="absolute right-0 cursor-pointer w-8 text-right"
          @click="showPassword"
        >
          @
        </p>
      </div>

      <div class="text-red-500 font-bold">{{ passwordError }}</div>

      <label class="text-[#aaa] text-[15px] font-bold tracking-[1px] uppercase"
        >Role:</label
      >
      <select
        class="border-b border-gray-300 text-[#555] bg-white focus:outline-none"
        v-model="role"
      >
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <label class="text-[#aaa] text-[15px] font-bold tracking-[1px] uppercase"
        >Skills:</label
      >
      <div v-if="tempSkill && showPopup" class="text-bold text-[15px] text-[#1bd478]">! Press space to add skill</div>
      <input
        type="text"
        class="border-b border-gray-300 text-[#555] focus:outline-none"
        v-model="tempSkill"
        @keyup="addSkill"
      />
      <div class="flex flex-wrap gap-[10px]">
        <span
          v-for="skill in skills"
          :key="skill"
          class="border-[2px] rounded-[20px] px-[15px] py-[3px] bg-[#e0dfdf] text-[#727171] font-bold uppercase tracking-[1px] flex relative">
            {{ skill }}
            <p class="absolute right-0 top-0 text-[0.5em] bg-[#646363] text-[rgb(255,255,255)] rounded-full w-[10px] text-center aspect-square cursor-auto" @click="deleteSkill(skill)">x</p>
        </span>
      </div>
      <div>
        <input type="checkbox" class="mr-[10px]" v-model="terms" required />
        <label
          class="text-[#aaa] text-[15px] font-bold tracking-[1px] uppercase"
          >Accept terms and conditions</label
        >
      </div>

      <div class="text-center mt-[10px]">
        <button class="bg-blue-600 rounded-[20px] px-[10px] py-[5px] text-white">Creat an Account</button>
      </div>

    </div>
  </form>
</template> 

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      tempSkill: "",
      skills: [],
      isPassword: true,
      passwordError: "",
      showPopup: false,
    };
  },
  methods: {
    addSkill(e) {
      if(this.skills.length === 0) this.showPopup = true
      if (e.key == " " && this.tempSkill) {
        this.showPopup = false
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    showPassword() {
      this.isPassword = !this.isPassword;
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => item !== skill);
    },
    handleSubmit(){
      this.passwordError = this.password.length < 8 ? "! Passwoed must be at least 8 characters" : ""
    }
  },
};
</script>

<style>
</style>