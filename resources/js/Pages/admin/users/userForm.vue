<script setup>


import { Head, Link, useForm } from '@inertiajs/vue3';
import adminLayeout from '@/Layouts/admin/adminLayeout.vue'
import GuestLayout from '@/Layouts/GuestLayout.vue'
const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
    is_admin:'',
    is_seller:''
});

const submit = () => {
    form.post(route('user.store'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
      <adminLayeout>
        <h1 class="mt-4 mb-4 font-sans font-extrabold uppercase text-md">Create a user</h1>
        <form @submit.prevent="submit()" class="grid grid-cols-1 mb-5 in-product-form" action="">
                <label class="text-sm font-extrabold" for="Product Name">Name</label>
                <input v-model="form.name" class="p-1 text-xs text-gray-500" type="text" placeholder="name" />
                <label class="text-sm font-extrabold" for="Serial Number">Email</label>
                <input v-model="form.email" class="p-1 text-xs text-gray-500" type="email"
                    placeholder="email" />
                    <label class="text-sm font-extrabold" for="Product Name">Make admin</label>
                <select  v-model="form.is_admin" name="category_id" id="countries"   class="p-1 text-xs text-gray-500 bg-blue-100 rounded-lg">
                <option :value="1" >True</option>
                <option :value="0" >False</option>
                </select>
                <label class="text-sm font-extrabold" for="Product Name">Make seller</label>
                <select  v-model="form.is_seller" name="category_id" id="countries"   class="p-1 text-xs text-gray-500 bg-blue-100 rounded-lg">
                <option :value="1" >True</option>
                <option :value="0" >False</option>
                </select>
                <label class="text-sm font-extrabold" for="Quantity">Password</label>
                <input v-model="form.password" class="p-1 text-xs text-gray-500" type="password" placeholder="password" />
                <label class="text-sm font-extrabold" for="Quantity">confirm password</label>
                <input v-model="form.password_confirmation" class="p-1 text-xs text-gray-500" type="password" placeholder="confirm password" />


                <button type="submit" class="text-sm btn-component text-bold">
                    submit
                </button>
            </form>

      </adminLayeout>

</template>
