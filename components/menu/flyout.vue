<template>
  <header class="bg-gray-900">
    <nav
      v-if="load"
      class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8"
      aria-label="Global"
    >
      <div class="flex lg:flex-1">
        <a href="/perfil" class="-m-1.5 p-1.5">
          <span class="sr-only">Your Company</span>
          <svg
            class="text-white"
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
          >
            <g
              fill="none"
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="1.5"
            >
              <path
                d="m17.123 9.03l-4.816-4.816L4.121 12.4a1.362 1.362 0 0 0 0 1.926L6.689 16.9a1.5 1.5 0 0 0 2.124 0v0"
              />
              <path
                d="m4.602 14.808l-2.408 2.408l1.926 1.926l2.408-2.408l-1.926-1.926ZM.75 20.587l2.408-2.408M10.863 2.77l1.444 1.444m1.445 1.445l3.371-3.371m1.926 1.926l-3.371 3.371m0-6.742l4.816 4.816m2.756 9.998a7.67 7.67 0 0 1-6 7.5a7.67 7.67 0 0 1-6-7.5v-2.25a1.5 1.5 0 0 1 1.5-1.5h9a1.5 1.5 0 0 1 1.5 1.5v2.25Zm-6-.75v4.5M15 17.157h4.5"
              />
            </g>
          </svg>
        </a>
      </div>
      <div class="flex lg:hidden">
        <button
          type="button"
          class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-white"
          @click="mobileMenuOpen = true"
        >
          <span class="sr-only">Open main menu</span>
          <Bars3Icon class="h-6 w-6" aria-hidden="true" />
        </button>
      </div>
      <PopoverGroup class="hidden lg:flex lg:gap-x-12">
        <Popover v-if="admin" class="relative">
          <PopoverButton
            class="flex items-center gap-x-1 text-sm font-semibold leading-6 text-white"
          >
            Listar
            <ChevronDownIcon class="h-5 w-5 flex-none text-gray-400" aria-hidden="true" />
          </PopoverButton>

          <transition
            enter-active-class="transition ease-out duration-200"
            enter-from-class="opacity-0 translate-y-1"
            enter-to-class="opacity-100 translate-y-0"
            leave-active-class="transition ease-in duration-150"
            leave-from-class="opacity-100 translate-y-0"
            leave-to-class="opacity-0 translate-y-1"
          >
            <PopoverPanel
              class="absolute -left-8 top-full z-10 mt-3 w-screen max-w-md overflow-hidden rounded-3xl bg-white shadow-lg ring-1 ring-gray-900/5"
            >
              <div class="p-4">
                <div
                  v-for="item in products"
                  :key="item.name"
                  class="group relative flex items-center gap-x-6 rounded-lg p-4 text-sm leading-6 hover:bg-gray-50"
                >
                  <div
                    class="flex h-11 w-11 flex-none items-center justify-center rounded-lg bg-gray-50 group-hover:bg-white"
                  >
                    <component
                      :is="item.icon"
                      class="h-6 w-6 text-gray-600 group-hover:text-indigo-600"
                      aria-hidden="true"
                    />
                  </div>
                  <div class="flex-auto">
                    <a :href="item.href" class="block font-semibold text-gray-900">
                      {{ item.name }}
                      <span class="absolute inset-0" />
                    </a>
                    <p class="mt-1 text-gray-600">{{ item.description }}</p>
                  </div>
                </div>
              </div>
            </PopoverPanel>
          </transition>
        </Popover>

        <a
          v-if="!admin"
          href="/meus-agendamentos"
          class="text-sm font-semibold leading-6 text-white"
          >Meus agendamentos</a
        >

        <a href="/agenda/cadastro" class="text-sm font-semibold leading-6 text-white"
          >Cadastrar Agenda</a
        >
        <a
          v-if="admin"
          href="/paciente/cadastro"
          class="text-sm font-semibold leading-6 text-white"
          >Cadastrar Paciente</a
        >
        <a
          v-if="admin"
          href="/vacina/cadastro"
          class="text-sm font-semibold leading-6 text-white"
          >Cadastrar Vacinas</a
        >
        <a
          v-if="admin"
          href="/alergia/cadastro"
          class="text-sm font-semibold leading-6 text-white"
          >Cadastrar Alergias</a
        >
      </PopoverGroup>

      <div class="hidden lg:flex lg:flex-1 lg:justify-end">
        <a href="/logout" class="text-sm font-semibold leading-6 text-white"
          >Sair <span aria-hidden="true">&rarr;</span></a
        >
      </div>
    </nav>
    <Dialog
      v-if="load"
      as="div"
      class="lg:hidden"
      @close="mobileMenuOpen = false"
      :open="mobileMenuOpen"
    >
      <div class="fixed inset-0 z-10" />
      <DialogPanel
        class="fixed inset-y-0 right-0 z-10 w-full overflow-y-auto bg-gray-900 px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10"
      >
        <div class="flex items-center justify-between">
          <a href="/perfil" class="-m-1.5 p-1.5">
            <span class="sr-only">Your Company</span>
            <svg
              class="text-white"
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
            >
              <g
                fill="none"
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1.5"
              >
                <path
                  d="m17.123 9.03l-4.816-4.816L4.121 12.4a1.362 1.362 0 0 0 0 1.926L6.689 16.9a1.5 1.5 0 0 0 2.124 0v0"
                />
                <path
                  d="m4.602 14.808l-2.408 2.408l1.926 1.926l2.408-2.408l-1.926-1.926ZM.75 20.587l2.408-2.408M10.863 2.77l1.444 1.444m1.445 1.445l3.371-3.371m1.926 1.926l-3.371 3.371m0-6.742l4.816 4.816m2.756 9.998a7.67 7.67 0 0 1-6 7.5a7.67 7.67 0 0 1-6-7.5v-2.25a1.5 1.5 0 0 1 1.5-1.5h9a1.5 1.5 0 0 1 1.5 1.5v2.25Zm-6-.75v4.5M15 17.157h4.5"
                />
              </g>
            </svg>
          </a>
          <button
            type="button"
            class="-m-2.5 rounded-md p-2.5 text-white"
            @click="mobileMenuOpen = false"
          >
            <span class="sr-only">Close menu</span>
            <XMarkIcon class="h-6 w-6" aria-hidden="true" />
          </button>
        </div>
        <div class="mt-6 flow-root">
          <div class="-my-6 divide-y divide-gray-500/10">
            <div class="space-y-2 py-6">
              <Disclosure as="div" class="-mx-3" v-slot="{ open }" v-if="admin">
                <DisclosureButton
                  class="flex w-full items-center justify-between rounded-lg py-2 pl-3 pr-3.5 text-white font-semibold leading-7 text-white hover:bg-gray-700"
                >
                  Listar
                  <ChevronDownIcon
                    :class="[open ? 'rotate-180' : '', 'h-5 w-5 flex-none']"
                    aria-hidden="true"
                  />
                </DisclosureButton>
                <DisclosurePanel class="space-y-1">
                  <DisclosureButton
                    v-for="subItem in products"
                    :key="subItem.name"
                    as="a"
                    :href="subItem.href"
                    class="group flex w-full items-center rounded-md py-2 pl-10 pr-2 text-sm font-medium text-white hover:bg-gray-50 hover:text-gray-900"
                    >{{ subItem.name }}</DisclosureButton
                  >
                </DisclosurePanel>
              </Disclosure>
              <a
                v-if="!admin"
                href="/meus-agendamentos"
                class="-mx-3 block rounded-lg px-3 py-2 text-white font-semibold leading-7 text-white hover:bg-gray-50"
                >Meus agendamentos</a
              >
              <a
                href="/agenda/cadastro"
                class="-mx-3 block rounded-lg px-3 py-2 text-white font-semibold leading-7 text-white hover:bg-gray-50"
                >Cadastrar Agenda</a
              >
              <a
                v-if="admin"
                href="/paciente/cadastro"
                class="-mx-3 block rounded-lg px-3 py-2 text-white font-semibold leading-7 text-white hover:bg-gray-50"
                >Cadastrar Paciente</a
              >
              <a
                v-if="admin"
                href="/vacina/cadastro"
                class="-mx-3 block rounded-lg px-3 py-2 text-white font-semibold leading-7 text-white hover:bg-gray-50"
                >Cadastrar Vacinas</a
              >
              <a
                v-if="admin"
                href="/alergia/cadastro"
                class="-mx-3 block rounded-lg px-3 py-2 text-white font-semibold leading-7 text-white hover:bg-gray-50"
                >Cadastrar Alergias</a
              >
            </div>
            <div class="py-6">
              <a
                href="/logout"
                class="-mx-3 block rounded-lg px-3 py-2.5 text-white font-semibold leading-7 text-white hover:bg-gray-50"
                >Sair</a
              >
            </div>
          </div>
        </div>
      </DialogPanel>
    </Dialog>
  </header>
</template>

<script setup>
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  Disclosure,
  DisclosureButton,
  DisclosurePanel,
  Popover,
  PopoverButton,
  PopoverGroup,
  PopoverPanel,
} from "@headlessui/vue";
import {
  ArrowPathIcon,
  Bars3Icon,
  ChartPieIcon,
  CursorArrowRaysIcon,
  FingerPrintIcon,
  SquaresPlusIcon,
  XMarkIcon,
} from "@heroicons/vue/24/outline";
import { ChevronDownIcon, PhoneIcon, PlayCircleIcon } from "@heroicons/vue/20/solid";

const admin = ref(false);
const load = ref(false);

onMounted(() => {
  if (localStorage.getItem("admin") == "true") {
    admin.value = true;
  } else {
    admin.value = false;
  }
  load.value = true;
});

const products = [
  {
    name: "Agendas",
    description: "Listar as agendas cadastradas",
    href: "/agenda/listar",
    icon: ChartPieIcon,
  },
  {
    name: "Alergia",
    description: "Listar as alergias cadastradas",
    href: "/alergia/listar",
    icon: CursorArrowRaysIcon,
  },
  {
    name: "Vacina",
    description: "Listar as vacinas cadastradas",
    href: "/vacina/listar",
    icon: FingerPrintIcon,
  },
  {
    name: "Pacientes",
    description: "Listar os pacientes cadastrados",
    href: "/paciente/listar",
    icon: SquaresPlusIcon,
  },
];

const mobileMenuOpen = ref(false);
</script>
