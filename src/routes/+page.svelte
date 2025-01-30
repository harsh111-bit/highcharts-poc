<script>
	import { onMount } from 'svelte';

	let Highcharts, drilldown, Chart;

	onMount(async () => {
		Highcharts = await import('highcharts');
		drilldown = await import('highcharts/modules/drilldown');

		const { Chart: ChartComponent } = await import('@highcharts/svelte');
		Chart = ChartComponent;

		drilldown(Highcharts);
	});

	let options = {
		chart: {
			type: 'line',
			reflow: true,
			responsive: {
				rules: [
					{
						condition: {
							maxWidth: 500
						},
						chartOptions: {
							legend: {
								enabled: false
							},
							yAxis: {
								title: {
									text: null // Remove axis title on small screens
								}
							}
						}
					}
				]
			},
			marginLeft: 24
		},
		title: {
			text: 'Donations'
		},
		subtitle: {
			text: null
		},
		xAxis: {
			type: 'category'
		},
		yAxis: {
			title: {
				text: 'Total Amount'
			}
		},
		legend: {
			enabled: false
		},
		plotOptions: {
			series: {
				dataLabels: {
					enabled: true,
					format: '{point.y:.1f}'
				}
			}
		},
		series: [
			{
				name: 'Main Categories',
				data: [
					{
						name: 'Category A',
						y: 50000,
						drilldown: 'category_a'
					},
					{
						name: 'Category B',
						y: 30000,
						drilldown: 'category_b'
					},
					{
						name: 'Category C',
						y: 20000,
						drilldown: 'category_c'
					}
				]
			}
		],
		drilldown: {
			series: [
				{
					id: 'category_a',
					name: 'Category A Subcategories',
					type: 'column', // Bar chart for subcategories
					data: [
						{
							name: 'Subcategory A1',
							y: 30000,
							drilldown: 'subcategory_a1'
						},
						{
							name: 'Subcategory A2',
							y: 20000,
							drilldown: 'subcategory_a2'
						}
					]
				},
				{
					id: 'subcategory_a1',
					name: 'Subcategory A1 Items',
					type: 'column', // Bar chart for items
					data: [
						['Item A1.1', 15000],
						['Item A1.2', 10000],
						['Item A1.3', 5000]
					]
				},
				{
					id: 'subcategory_a2',
					name: 'Subcategory A2 Items',
					type: 'column', // Bar chart for items
					data: [
						['Item A2.1', 12000],
						['Item A2.2', 8000]
					]
				},
				{
					id: 'category_b',
					name: 'Category B Subcategories',
					type: 'column', // Bar chart for subcategories
					data: [
						{
							name: 'Subcategory B1',
							y: 15000,
							drilldown: 'subcategory_b1'
						},
						{
							name: 'Subcategory B2',
							y: 15000,
							drilldown: 'subcategory_b2'
						}
					]
				},
				{
					id: 'subcategory_b1',
					name: 'Subcategory B1 Items',
					type: 'column', // Bar chart for items
					data: [
						['Item B1.1', 7000],
						['Item B1.2', 8000]
					]
				},
				{
					id: 'subcategory_b2',
					name: 'Subcategory B2 Items',
					type: 'column', // Bar chart for items
					data: [
						['Item B2.1', 6000],
						['Item B2.2', 9000]
					]
				},
				{
					id: 'category_c',
					name: 'Category C Subcategories',
					type: 'column', // Bar chart for subcategories
					data: [
						{
							name: 'Subcategory C1',
							y: 10000,
							drilldown: 'subcategory_c1'
						},
						{
							name: 'Subcategory C2',
							y: 10000,
							drilldown: 'subcategory_c2'
						}
					]
				},
				{
					id: 'subcategory_c1',
					name: 'Subcategory C1 Items',
					type: 'column', // Bar chart for items
					data: [
						['Item C1.1', 5000],
						['Item C1.2', 5000]
					]
				},
				{
					id: 'subcategory_c2',
					name: 'Subcategory C2 Items',
					type: 'column', // Bar chart for items
					data: [
						['Item C2.1', 7000],
						['Item C2.2', 3000]
					]
				}
			]
		},
		credits: {
			style: {
				display: 'none'
			},
			position: {
				align: 'right',
				x: -10, // Distance from right edge
				y: 8 // Vertical position
			}
		}
	};
</script>

{#if Chart}
	<div class="chart-container">
		<Chart {options} highcharts={Highcharts} />
	</div>
{/if}

<style>
	.chart-container {
		width: 100%;
		min-height: 400px;
		max-width: 1200px;
		margin: 0 auto;
	}

	:global(.highcharts-drilldown-data-label text),
	:global(.highcharts-drilldown-axis-label),
	:global(.highcharts-label a),
	:global(.highcharts-breadcrumbs-button text) {
		color: #ea580c !important; /* Orange color */
		fill: #ea580c !important;
	}

	:global(.highcharts-label a:hover),
	:global(.highcharts-breadcrumbs-button:hover) {
		color: #fb923c !important; /* Slightly lighter orange for hover state */
		fill: #fb923c !important;
	}

	:global(.highcharts-breadcrumbs-button .highcharts-button-box) {
		/* Added this */
		fill: transparent;
	}
</style>
