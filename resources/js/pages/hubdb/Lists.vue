<template>
	<div class="bg-grey-lighter min-h-screen flex flex-col">
		<div class="container my-12 mx-auto px-4 md:px-12">
			<div class="py-5 flex justify-start">
				<div>
					<h1 class="mb-8 text-3xl text-center">My HubSpot Contact Lists</h1>
				</div>
			</div>
		</div>
		<div class="container my-12 mx-auto px-4 md:px-12" v-if="loaded">
			<div class="flex flex-wrap -mx-1 lg:-mx-4" v-if="lists.length">
				<div class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3" v-for="(list, key) in lists" :key="key">

					<div class="p-6 max-w-sm bg-white rounded-lg border border-gray-200 shadow-md bg-gray-800 border-gray-700">
						<div class="flex mb-4">
							<svg height="35" viewBox="6.20856283 .64498824 244.26943717 251.24701176" width="35" xmlns="http://www.w3.org/2000/svg"><path d="m191.385 85.694v-29.506a22.722 22.722 0 0 0 13.101-20.48v-.677c0-12.549-10.173-22.722-22.721-22.722h-.678c-12.549 0-22.722 10.173-22.722 22.722v.677a22.722 22.722 0 0 0 13.101 20.48v29.506a64.342 64.342 0 0 0 -30.594 13.47l-80.922-63.03c.577-2.083.878-4.225.912-6.375a25.6 25.6 0 1 0 -25.633 25.55 25.323 25.323 0 0 0 12.607-3.43l79.685 62.007c-14.65 22.131-14.258 50.974.987 72.7l-24.236 24.243c-1.96-.626-4-.959-6.057-.987-11.607.01-21.01 9.423-21.007 21.03.003 11.606 9.412 21.014 21.018 21.017 11.607.003 21.02-9.4 21.03-21.007a20.747 20.747 0 0 0 -.988-6.056l23.976-23.985c21.423 16.492 50.846 17.913 73.759 3.562 22.912-14.352 34.475-41.446 28.985-67.918-5.49-26.473-26.873-46.734-53.603-50.792m-9.938 97.044a33.17 33.17 0 1 1 0-66.316c17.85.625 32 15.272 32.01 33.134.008 17.86-14.127 32.522-31.977 33.165" fill="#ff7a59"/></svg>
							<div class="px-4 flex whitespace-nowrap text-ellipsis overflow-hidden"><h3 class="text-white text-xl">Contact List</h3></div>
						</div>
						<div class="border-b border-blue-400 mb-5"></div>
						<h5 class="mb-2 text-2xl font-semibold tracking-tight text-white">{{list.name}}</h5>
						<p class="mb-3 font-normal text-gray-500  text-gray-100">List Type: <br><strong>{{list.listType}}</strong></p>
						<p class="mb-3 font-normal text-gray-500  text-gray-100">Size: <br><strong>{{list.metaData?.size}}</strong></p>
					</div>


				</div>
			</div>
			<div class="flex justify-center" v-if="!lists.length">
				<div>
					<h1 class="mb-8 text-3xl text-center">No Lists found.</h1>
					<p class="text-center">You don't have any Contact Lists in this portal. <router-link class="no-underline border-b border-blue text-blue-500" :to="{name: 'portals'}">Choose another portal</router-link>.</p>
				</div>
			</div>
		</div>

	</div>
</template>

<script>

    import { useAuthStore } from '@/store/auth'

	export default {
		name: 'Lists',
		props: { },
        data: () => ({
			auth: useAuthStore(),
            lists: [],
			loaded: false
        }),
        mounted () {
			this.fetchLists()
        },
		methods: {
            
            async fetchLists(){
                const res = await axios.get(route('hs-lists.get'))
                this.lists = res.data.lists
				this.loaded = true
            }
            
        }
	}
</script>