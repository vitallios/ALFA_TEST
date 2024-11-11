<script setup>
import { RouterView } from 'vue-router'
import TheHeader from './components/TheHeader.vue'
import TheFooter from './components/TheFooter.vue'
const text ={
  titlePages:'Персональные данные',
  childrenCol:'Дети (макс. 5)',
  AGE:'Возраст',
  NAME:'Имя',
  addChildrenItem:'Добавить ребёнка',
  textSAVE:'Сохранить'
}




const CREATE_NEW_CHILD = () => {
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
  inputName.attributes.required = true;
  inputName.name = 'childName';
  inputName.classList.add('w-full', 'border-none', 'outline-none');

  const childrenDivInputLabelAge = document.createElement('div');
  childrenDivInputLabelAge.classList.add('childrenInput');

  const childrenLabelAge = document.createElement('label');
  childrenLabelAge.textContent = 'Возраст';

  const inputAge = document.createElement('input');
  inputAge.type = 'text';
  inputAge.attributes.required = true;
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
}
</script>

<template>
  <TheHeader />
  <div class="container">
    <RouterView
    :titlePages = text.titlePages
    :childrenCol = text.childrenCol
    :AGE = text.AGE
    :NAME = text.NAME
    :addChildrenItem = text.addChildrenItem
    :textSAVE = text.textSAVE
    @CREATE_NEW_CHILD = CREATE_NEW_CHILD
     />
  </div>
  <TheFooter />
</template>


<style scoped>
@media  (max-width: 550px)  {
  .container{
    padding: 0 10px;
  }
}
</style>
