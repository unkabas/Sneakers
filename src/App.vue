<script setup lang="ts">
import axios from 'axios'
import { onMounted, ref } from 'vue'
import CardList from './components/CardList.vue'
// import Drawer from './components/Drawer.vue'
import Header from './components/Header.vue'

const items = ref([])

onMounted(async () => {
	try {
		const { data } = await axios.get('https://0f285d6667c87a29.mokky.dev/items')
		items.value = data
	} catch (err) {
		console.log(err)
	}
})
</script>

<template>
	<!-- <Drawer /> -->
	<div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-10">
		<Header />
		<div class="p-10">
			<div class="flex justify-between items-center">
				<h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

				<div class="flex gap-4">
					<select class="py-2 px-3 border rounded-md outline-none">
						<option>По названию</option>
						<option>Дешевые</option>
						<option>Дорогие</option>
					</select>

					<div class="relative">
						<img src="/search.svg" alt="Search" class="absolute left-4 top-3" />
						<input
							type="text"
							placeholder="Поиск..."
							class="border border-gray-200 rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400 transition"
						/>
					</div>
				</div>
			</div>
			<CardList :items="items" />
		</div>
	</div>
</template>
