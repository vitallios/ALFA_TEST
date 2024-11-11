<script setup>
import router from '@/router';
import { ref, reactive } from 'vue';
defineProps(['titlePages', 'childrenCol', 'AGE', 'NAME', 'addChildrenItem', 'textSAVE']);
const emit = defineEmits(['CREATE_NEW_CHILD', '']);


const newChaild = ref([]);
const Parent = reactive({
  name: '',
  age: '',
  childtern: [],
});
const saveTiket = () => {
  const childrenList = document.getElementById('ChildrenList');
  const children = childrenList.children;
  for (const element of children) {
    const inputName = element.querySelector('input[name="childName"]');
    const inputAge = element.querySelector('input[name="childAge"]');
    Parent.childtern.push({
      name: inputName.value,
      age: inputAge.value
    });
  }
  newChaild.value.push({ ...Parent });
  localStorage.setItem('newChaild', JSON.stringify(newChaild.value));
  router.push('/about');
};

</script>


<template>
  <main class="pt-[30px] pb-[7em]">
    <div class="parentName flex flex-col gap-[10px]">

      <h3>{{ titlePages }}</h3>
      <div class="pt-[22px]">
        <label for="parentNameLabel">{{NAME}}</label>
        <input v-model="Parent.name" required class="w-full border-none outline-none" type="text" id="parentNameLabel">
      </div>
      <div>
        <label for="parentAgeLabel">{{AGE}}</label>
        <input v-model="Parent.age" required class="w-full border-none outline-none" type="text" id="parentAgeLabel">
      </div>
    </div>

    <div>
      <div class="flex flex-row items-center mt-[44px]">
        <div class="flex justify-between items-center w-full relative">
          <h3>{{ childrenCol }}</h3>
          <button @click="emit('CREATE_NEW_CHILD')" id="addChildBtn"
            class="btn absolute right-0 flex justify-between items-center px-[20px] py-[10px] border-[#01A7FD] border-[1px] rounded-[100px] outline-none">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M5.13332 10.8556C4.50125 10.8555 3.98887 11.3679 3.98887 12C3.98887 12.6321 4.50126 13.1445 5.13332 13.1445L10.8554 13.1445L10.8554 18.8668C10.8554 19.4989 11.3678 20.0113 11.9999 20.0113C12.632 20.0113 13.1444 19.4989 13.1444 18.8668L13.1443 13.1445L18.8667 13.1445C19.4988 13.1445 20.0112 12.6321 20.0112 12C20.0112 11.3679 19.4988 10.8556 18.8667 10.8556L13.1443 10.8556L13.1443 5.13338C13.1443 4.50132 12.632 3.98893 11.9999 3.98893C11.3678 3.98893 10.8554 4.50131 10.8554 5.13338L10.8554 10.8556L5.13332 10.8556Z"
                fill="#01A7FD" />
            </svg>
            <span class="ml-[10px] text-[#01A7FD]">
              {{ addChildrenItem }}
            </span>
          </button>
        </div>
      </div>
      <ul id="ChildrenList" class="pt-[22px] flex flex-col gap-[10px]"></ul>
      <button @click="saveTiket"
        class="mt-[30px] py-[10px] px-[20px] border-[#01A7FD] border-[1px] rounded-[100px] bg-[#01A7FD] text-white text-[14px]">
        {{ textSAVE }}
      </button>
    </div>
  </main>
</template>


<style>
.parentName>div,
.childrenItem>div {
  position: relative;
  flex: 1;
}

.parentName>div>input,
.childrenItem>div>input {
  padding: 7px 16px;
  border-radius: 8px;
  border: 1px solid #DDE2E5;
  position: relative;
  padding-top: 26px;
  line-height: 24px;
  font-size: 14px;
  width: 100%;
}

.parentName>div>label,
.childrenItem>div>label {
  position: absolute;
  padding: 8px 0 2px 16px;
  font-size: 13px;
  color: var(--lightBlack);
  z-index: 10;
}

@media (max-width: 550px){
  #addChildBtn{
    padding: 0.5em 0.7em;
  }
  .childrenItem {
    flex-direction: column;
    align-items: flex-start;
  }
  .childrenItem>div {
    width: 100%;
  }

}
</style>
