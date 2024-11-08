<script setup>
import { ref, reactive } from 'vue';

const newChaild = ref([]);
const Parent = reactive({
  name: '',
  age: '',
  childtern: [],
});
const Child = reactive({
  name: '',
  age: '',
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
  console.log(newChaild.value);
};

const createNewChild = () => {
  const childrenList = document.getElementById('ChildrenList');
  if (childrenList.children.length >= 5) {
    alert('Максимальное количество детей - 5');
    return;
  }
  
  const childrenItem = document.createElement('li');
  childrenItem.classList.add('childrenItem', 'flex', 'gap-[18px]');
  
  const childrenDivInputLabelName = document.createElement('div');
  childrenDivInputLabelName.classList.add('childrenInput');
  
  const childrenLabelName = document.createElement('label');
  childrenLabelName.textContent = 'Имя';
  
  const inputName = document.createElement('input');
  inputName.type = 'text';
  inputName.name = 'childName';
  inputName.classList.add('w-full', 'border-none', 'outline-none');
  
  const childrenDivInputLabelAge = document.createElement('div');
  childrenDivInputLabelAge.classList.add('childrenInput');
  
  const childrenLabelAge = document.createElement('label');
  childrenLabelAge.textContent = 'Возраст';
  
  const inputAge = document.createElement('input');
  inputAge.type = 'text';
  inputAge.name = 'childAge';
  inputAge.classList.add('w-full', 'border-none', 'outline-none');
  
  const removeBtn = document.createElement('button');
  removeBtn.classList.add('btn', 'removeBtn', 'text-[#01A7FD]');
  removeBtn.textContent = 'Удалить';

  childrenDivInputLabelName.append(childrenLabelName, inputName);
  childrenDivInputLabelAge.append(childrenLabelAge, inputAge);
  childrenItem.append(childrenDivInputLabelName, childrenDivInputLabelAge, removeBtn);
  childrenList.appendChild(childrenItem);

  removeBtn.addEventListener('click', () => childrenItem.remove());
};

</script>

<template>
  <main class="pt-[30px]">
    <div class="parentName flex flex-col gap-[10px]">
      <h1>Персональные данные</h1>
      <div class="pt-[22px]">
        <label for="parentNameLabel">Имя</label>
        <input v-model="Parent.name" class="w-full border-none outline-none" type="text" id="parentNameLabel">
      </div>
      <div>
        <label for="parentAgeLabel">Возраст</label>
        <input v-model="Parent.age" class="w-full border-none outline-none" type="text" id="parentAgeLabel">
      </div>
    </div>

    <div>
      <div class="flex flex-row items-center mt-[44px]">
        <div class="flex justify-between items-center w-full relative">
          <h4>Дети (макс. 5)</h4>
          <button @click="createNewChild" class="btn absolute right-0 flex justify-between items-center px-[20px] py-[10px] border-[#01A7FD] border-[1px] rounded-[100px] outline-none">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M5.13332 10.8556C4.50125 10.8555 3.98887 11.3679 3.98887 12C3.98887 12.6321 4.50126 13.1445 5.13332 13.1445L10.8554 13.1445L10.8554 18.8668C10.8554 19.4989 11.3678 20.0113 11.9999 20.0113C12.632 20.0113 13.1444 19.4989 13.1444 18.8668L13.1443 13.1445L18.8667 13.1445C19.4988 13.1445 20.0112 12.6321 20.0112 12C20.0112 11.3679 19.4988 10.8556 18.8667 10.8556L13.1443 10.8556L13.1443 5.13338C13.1443 4.50132 12.632 3.98893 11.9999 3.98893C11.3678 3.98893 10.8554 4.50131 10.8554 5.13338L10.8554 10.8556L5.13332 10.8556Z"
                fill="#01A7FD" />
            </svg>
            <span class="ml-[10px] text-[#01A7FD]">
              Добавить ребенка
            </span>
          </button>
        </div>
      </div>
      <ul id="ChildrenList" class="pt-[22px] flex flex-col gap-[10px]"></ul>
      <button @click="saveTiket" class="mt-[30px] py-[10px] px-[20px] border-[#01A7FD] border-[1px] rounded-[100px] bg-[#01A7FD] text-white text-[14px]">Сохранить</button>
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
</style>
