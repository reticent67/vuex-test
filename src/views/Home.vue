<template>
	<div class="home">
		<img alt="Vue logo" src="../assets/logo.png">
		<person1></person1>
		<person2></person2>
		<button @click="newPerson">Add Person</button>
	</div>
</template>

<script>
	// @ is an alias to /src
	import person1 from "@/components/person1";
	import person2 from "@/components/person2";
	import { createHelpers } from "vuex-map-fields";
	import { createNamespacedHelpers } from "vuex";
	import state from "../../store/store";

	const { mapFields } = createHelpers({
		getterType: "person/getField",
		mutationType: "person/updateField"
	});
	export default {
		name: "home",
		data() {
			return {};
		},

		components: { person1, person2 },
		methods: {
			newPerson() {
				this.counter += 1;
				this.$store.registerModule(`person${this.counter}`, person);
			}
		},
		computed: {
			...mapFields(["counter"])
		},
		created() {
			this.$store.registerModule("person1", state);
		}
	};
</script>
