<template lang="jade">
	div.wrapper
		span.tag-wrapper(v-for="item in AddedItems"){{ getItemName(item) }}
			i.del(@click="delAddedItem($index)")x
		input.form-control(type="text", :placeholder="schema.placeholder")
			  span.btn(@click="addItem(item)")+	
</template>
<script>
    import isFunction from 'lodash/isFunction';
	import abstractField from "./abstractField";
	
	export default {
		mixins: [ abstractField ],
	    computed:{
	    	AddedItems(){
	    		let values = this.schema.values;
	    		return values;
	    	}
	    },
		methods: {
			addItem(item) {
				   let item = this.value
       				this.AddedItems.push(item);
       				this.value = "";
      	},
			delAddedItem(index) {
        			this.AddedItems.splice(index, 1);
      	},
      		getItemName(item) {
				if (isObject(item) && item.name)
					return item.name;

				return item;
			},
      		getItemIsAdded(item) {
				return (this.AddedItems && this.AddedItems.indexOf(item) != -1)	
		}
	}
};
</script>

<style lang="sass">
	.vue-form-generator .field-tips{
		.wrapper {
			width: 100%;
			position: relative;
			overflow: hidden;
		}
		span.tag-wrapper{
			display:inline-block !important;
			position:relative;

		}
	}
</style>
