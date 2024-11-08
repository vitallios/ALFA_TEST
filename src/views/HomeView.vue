<script setup>
import { ref } from 'vue';

const newChaild = ref([])

const Parent = ref({
  name: '',
  age: '',
  childtern: [],
});
let Child = ref({
  name: '',
  age: '',
});


// сохранить данные
const saveTiket = async () => {
  const childrenList = document.getElementById('ChildrenList');
  const children = childrenList.children;
  for (const element of children) {
    const inputName = element.children[0];
    const inputAge = element.children[1];
    Parent.value.childtern.push({
      name: inputName.value,
      age: inputAge.value
    });
  }
  newChaild.value.push(Parent.value)
  console.log(newChaild.value);
}

// создать и удалить плвое поле для добавления детей
const createNewChild = () => {
  console.dir(newChaild.value);

  const childrenItem = document.createElement('li');
  childrenItem.classList.add('childrenItem')

  const inputName = document.createElement('input');
  inputName.type = 'text';
  inputName.placeholder = 'Имя';
  inputName.classList.add('inputName')

  const inputAge = document.createElement('input');
  inputAge.type = 'text';
  inputAge.placeholder = 'Возраст';
  inputAge.classList.add('inputAge')

  const removeBtn = document.createElement('button');
  removeBtn.classList.add('removeBtn')
  removeBtn.textContent = 'Удалить'

  if (document.getElementById('ChildrenList').children.length <= 4) {
    childrenItem.appendChild(inputName);
    childrenItem.appendChild(inputAge);
    childrenItem.appendChild(removeBtn);
    document.getElementById('ChildrenList').appendChild(childrenItem);
  }

  removeBtn.addEventListener('click', () => {
    childrenItem.remove();
  })

};

</script>

<template>
  <main class="pt-[30px]">
    <!-- Родитель -->

    <div class="parentName flex flex-col ">
      <h2>Персональные данные</h2>
      <div class="pt-[22px]">
        <label for="parentNameLabel">Имя</label>
        <input v-model="Parent.name" class="w-full border-none outline-none" type="text">
      </div>
      <div>
        <label for="parentAgeLabel">Возраст</label>
        <input v-model="Parent.age" class="w-full border-none outline-none" type="text">
      </div>
    </div>
    <!-- Родитель -->

    <!-- Добавить поле с детьми -->
    <div>
      <div class="flex flex-row items-center ">
        <h2>Дети (макс. 5)</h2>
        <button @click="createNewChild()" class="btn flex justify-between items-center">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd"
              d="M5.13332 10.8556C4.50125 10.8555 3.98887 11.3679 3.98887 12C3.98887 12.6321 4.50126 13.1445 5.13332 13.1445L10.8554 13.1445L10.8554 18.8668C10.8554 19.4989 11.3678 20.0113 11.9999 20.0113C12.632 20.0113 13.1444 19.4989 13.1444 18.8668L13.1443 13.1445L18.8667 13.1445C19.4988 13.1445 20.0112 12.6321 20.0112 12C20.0112 11.3679 19.4988 10.8556 18.8667 10.8556L13.1443 10.8556L13.1443 5.13338C13.1443 4.50132 12.632 3.98893 11.9999 3.98893C11.3678 3.98893 10.8554 4.50131 10.8554 5.13338L10.8554 10.8556L5.13332 10.8556Z"
              fill="#01A7FD" />
          </svg>
          Добавить
        </button>
      </div>
      <ul id="ChildrenList" class="pt-[22px]">
        <li class="childrenItem">
          <div>
            <label for="childrenNameLabel">Имя</label>
            <input v-model="Child.name" type="text" placeholder="Иван" aria-label="Имя">
          </div>
          <div>
            <label for="childrenAgeLabel">Возраст</label>
            <input v-model="Child.age" type="text" placeholder="Возраст" aria-label="Возраст">

          </div>

          <button class="btn removeBtn">Удалить</button>
        </li>
      </ul>
      <!-- Добавить поле с детьми -->
      <!-- кнопка сохранить -->
      <button @click="saveTiket()">Сохранить</button>
    </div>
  </main>
</template>

<style scoped>
.parentName>div>input,
.childrenItem>div>input {
  padding: 7px 16px;
  border-radius: 8px;
  border: 1px solid #DDE2E5;
  margin-bottom: 10px;
  margin-right: 10px;
  position: relative;
  padding-top: 26px;
  line-height: 24px;
  font-size: 14px;
}

.parentName>div,
.childrenItem>div {
  position: relative;
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