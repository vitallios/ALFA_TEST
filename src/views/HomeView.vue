<script setup>
import router from '@/router';
import { reactive, ref } from 'vue';
//
import ParentName from '@/components/ParentName.vue';
import ParentAge from '@/components/ParentAge.vue';
import BtnAddChildren from '@/components/BtnAddChildren.vue';
import PageTitle from '@/components/PageTitle.vue';
import BtnSave from '@/components/BtnSave.vue';
//
const PageTitleText = ref('Дети (макс. 5)');
const textBtn = ref('Добавить ребенка');
const saveTextBtn = ref('Сохранить');
const iconBtn = ref("M5.13332 10.8556C4.50125 10.8555 3.98887 11.3679 3.98887 12C3.98887 12.6321 4.50126 13.1445 5.13332 13.1445L10.8554 13.1445L10.8554 18.8668C10.8554 19.4989 11.3678 20.0113 11.9999 20.0113C12.632 20.0113 13.1444 19.4989 13.1444 18.8668L13.1443 13.1445L18.8667 13.1445C19.4988 13.1445 20.0112 12.6321 20.0112 12C20.0112 11.3679 19.4988 10.8556 18.8667 10.8556L13.1443 10.8556L13.1443 5.13338C13.1443 4.50132 12.632 3.98893 11.9999 3.98893C11.3678 3.98893 10.8554 4.50131 10.8554 5.13338L10.8554 10.8556L5.13332 10.8556Z");
//
const Parent = reactive({
  name: '',
  age: '',
  childtern: []
});



const addChild = () => {
  const ChildrenList = document.getElementById('ChildrenList');
  const ChildElementLi = document.createElement('li');
  const ChildElementDivAge = document.createElement('div');
  const ChildElementDivName = document.createElement('div');
  const ChildElementLabelAge = document.createElement('label');
  const ChildElementInputAge = document.createElement('input');
  const ChildElementLabelName = document.createElement('label');
  const ChildElementInputName = document.createElement('input');
  const ChildElementButtonRemoveChild = document.createElement('button');


  ChildElementLi.classList.add('flex', 'flex-row', 'items-center', 'gap-[18px]');
  // children age wrapper
  ChildElementDivAge.classList.add('flex', 'flex-col', 'gap-[2px]', 'px-[16px]', 'py-[8px]', 'border-[1px]', 'border-[#DDE2E5]', 'rounded-[8px]', 'flex-1');
  // children name wrapper
  ChildElementDivName.classList.add('flex', 'flex-col', 'gap-[2px]', 'px-[16px]', 'py-[8px]', 'border-[1px]', 'border-[#DDE2E5]', 'rounded-[8px]', 'flex-1');

  // children age
  ChildElementLabelAge.classList.add('text-[13px]','text-[var(--lightBlack)]');  ChildElementInputAge.classList.add('w-full', 'border-none', 'outline-none', 'text-[14px]');
  // children name
  ChildElementLabelName.classList.add('text-[13px]','text-[var(--lightBlack)]');
  ChildElementInputName.classList.add('w-full', 'border-none', 'outline-none', 'text-[14px]');
  // children button remove
  ChildElementButtonRemoveChild.classList.add('text-[16px]', 'text-[#01A7FD]');

  // children name
  ChildElementLabelName.textContent = 'Имя';
  ChildElementInputName.type = 'text';
  ChildElementInputName.required = true;

  // children age
  ChildElementLabelAge.textContent = 'Возраст';
  ChildElementInputAge.type = 'text';
  ChildElementInputAge.required = true;

  // children button remove
  ChildElementButtonRemoveChild.textContent = 'Удалить';
  // children button remove function
  ChildElementButtonRemoveChild.addEventListener('click', () => {
    ChildrenList.removeChild(ChildElementLi);
  });

  // add children div name
  ChildElementDivName.appendChild(ChildElementLabelName);
  ChildElementDivName.appendChild(ChildElementInputName);
  // add children div age
  ChildElementDivAge.appendChild(ChildElementLabelAge);
  ChildElementDivAge.appendChild(ChildElementInputAge);

  // add children li
  ChildElementLi.appendChild(ChildElementDivName);
  ChildElementLi.appendChild(ChildElementDivAge);
  ChildElementLi.appendChild(ChildElementButtonRemoveChild);

  // children ul
  ChildrenList.appendChild(ChildElementLi);

}
const save = async () => {
  const ParentName = document.getElementById('parentNameLabel');
  const ParentAge = document.getElementById('parentAgeLabel');

  Parent.name = ParentName.value;
  Parent.age = ParentAge.value;

  const ChildrenList = document.getElementById('ChildrenList');
  const Children = ChildrenList.children;

  for (const element of Children) {
    const ChildElementInputAge = element.children[1].children[1];
    const ChildElementInputName = element.children[0].children[1];

    Parent.childtern.push({
      name: ChildElementInputName.value,
      age: ChildElementInputAge.value
    });
  }

  router.push('/about');
  localStorage.setItem('Parent', JSON.stringify(Parent));
  // delite localstorage


}
</script>


<template>
  <main class="pt-[30px] pb-[7em]">
    <div class="parentName flex flex-col gap-[10px]">
      <h3> Родитель </h3>
      <ParentName class="pt-[22px]" v-model="Parent.name" />
      <ParentAge v-model="Parent.age" />
    </div>

    <div>
      <div class="flex flex-row items-center mt-[44px]">
        <div class="flex justify-between items-center w-full relative">
          <PageTitle :title="PageTitleText" />
          <BtnAddChildren @addChild="addChild" :btnText="textBtn" :iconBtn="iconBtn" />
        </div>
      </div>

      <ul id="ChildrenList" class="pt-[22px] flex flex-col gap-[10px]"></ul>
      <BtnSave @save="save" :saveTextBtn="saveTextBtn" />
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

@media (max-width: 550px) {
  #addChildBtn {
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
