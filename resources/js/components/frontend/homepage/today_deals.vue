<template>
	<section class="products-section item-space-rmv" v-if="lengthCounter(products) > 0">
		<div class="container">
			<div class="title justify-content-between" :class="{ 'title-bg title-btm-space': addons.includes('ishopet') }">
				<div class="deal_wrapper" style="display: flex; align-items: center;">
					<div>
						<h1>{{ lang.today_deals }}</h1>
					</div>
					<div class="product-stock-delivery">
						<div class="sg-countdown">
							<ul class="countdown">
								<li><span class="days">31</span>
									<p>Days</p>
								</li>
								<li><span class="hours">12</span>
									<p>Hrs</p>
								</li>
								<li><span class="minutes">50</span>
									<p>Mins</p>
								</li>
								<li><span class="seconds">30</span>
									<p>Secs</p>
								</li>
							</ul>
						</div>
					</div>
				</div>

				<a :href="getUrl('daily-deals')" @click.prevent="routerNavigator('daily.deals')">{{ lang.more_products
				}}<span class="icon mdi mdi-name mdi-arrow-right"></span></a>
			</div>
			<productCarousel :products="today_deals" :grid_class="'grid-6'"></productCarousel>
		</div>
	</section>
	<section class="products-section bg-white" v-else-if="show_shimmer">
		<div class="container">
			<ul class="products grid-6">
				<li v-for="(product, index) in 6" :key="index">
					<div class="sg-product">
						<a href="javascript:void(0)">
							<shimmer :height="290"></shimmer>
						</a>
					</div>
				</li>
			</ul>
		</div>
	</section>
</template>

<script>
import productCarousel from "../pages/product-carousel";
import shimmer from "../partials/shimmer";

export default {
	name: "today_deals",
	components: {
		productCarousel,
		shimmer,
	},
	data() {
		return {
			show_shimmer: true,
		};
	},
	props: ["today_deals"],

	mounted() {
		this.checkHomeComponent("todays_deal");
	},
	watch: {
		homeResponse() {
			this.checkHomeComponent("todays_deal");
		},
	},
	computed: {
		products() {
			if (this.today_deals && this.today_deals.length > 0) {
				return this.today_deals;
			} else {
				return [];
			}
		},
	},
	methods: {
		checkHomeComponent(component_name) {
			let component = this.homeResponse.find((data) => data == component_name);

			if (component) {
				return (this.show_shimmer = false);
			}
		},
	},
};
</script>

