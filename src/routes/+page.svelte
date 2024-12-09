<script lang="ts">
	import { TableShowCase } from '$lib/website/components/base/table-showcase';
	import { Page, Main, MainContent } from '$lib/website/templates/base';
	import { BaseDataTableView, type Settings } from '$lib/data-table/views';

	import { MarkdownContent } from '$lib/website/components/base/markdown-content';
	import Giris, { metadata } from '$lib/website/contents/Giris.md';

	import common from '$lib/website/utils/common';

	type DataType = {
		order: number;
		producer: string;
		province: string;
		district: string;
		village: string;
		grape: string;
		grapeColor: string;
		quantity: number;
		price: number;
		amount: number;
	};

	let data: DataType[] = $state(common.generateExampleData(10));

	let settings: Settings<DataType> = $state({
		columns: [
			{ field: 'order', label: 'Order', width: '75px' },
			{ field: 'producer', label: 'Producer', width: '150px' },
			{ field: 'province', label: 'Province', width: '90px' },
			{ field: 'district', label: 'District', width: '100px' },
			{ field: 'village', label: 'Village', width: '120px' },
			{ field: 'grape', label: 'Grape', width: '160px' },
			{ field: 'grapeColor', label: 'Grape Color', width: '110px', hidden: false },
			{ field: 'quantity', label: 'Quantity', align: 'right', width: '100px' },
			{ field: 'price', label: 'Price', align: 'right', width: '100px' },
			{ field: 'amount', label: 'Amount', align: 'right', width: '100px' }
		],
		footers: [{ order: 'f1' }, { quantity: 'f2' }]
	});

	const setPageData = (count: number) => {
		data = common.generateExampleData(count);
	};
	const setFirstRow = () => {
		data[0] = {
			order: 0,
			producer: 'Mustahsil',
			province: 'Tip',
			district: 'Bölge',
			village: 'İl',
			grape: 'İlçe',
			grapeColor: '0',
			quantity: 0,
			price: 0,
			amount: 0
		};
	};
	const hiddenSecondColumn = () => {
		if (typeof settings.columns === 'undefined') return;
		settings.columns[1].hidden = !settings.columns[1].hidden;
	};
</script>

<Page>
	<Main>
		<div class="flex select-none items-center justify-center gap-4 rounded-full p-2">
			<div class="flex items-center gap-1">
				<img
					src="/images/svelte-logo.png"
					alt="Svelte Logo"
					class="h-8 w-8 slc-image-select-none"
				/>
				<p class=" text-lg font-semibold">Svelte</p>
			</div>
			<div class="flex items-center gap-1">
				<img
					src="/images/ts-logo-512.png"
					alt="TypeScript Logo"
					class="h-8 w-8 slc-image-select-none"
				/>
				<p class=" text-lg font-semibold">TypeScript</p>
			</div>
		</div>
		<MainContent>
			<TableShowCase>
				<BaseDataTableView {data} {settings} />
			</TableShowCase>
		</MainContent>
		<MainContent>
			<div>
				<button onclick={() => setPageData(0)} class="bg-surface-200 p-1">0</button>
				<button onclick={() => setPageData(3)} class="bg-surface-200 p-1">3</button>
				<button onclick={() => setPageData(5)} class="bg-surface-200 p-1">5</button>
				<button onclick={() => setPageData(10)} class="bg-surface-200 p-1">10</button>
				<button onclick={() => setPageData(100)} class="bg-surface-200 p-1">100</button>
				<button onclick={() => setPageData(1000)} class="bg-surface-200 p-1">1000</button>
				<button onclick={() => setPageData(10000)} class="bg-surface-200 p-1">10000</button>
				<button onclick={() => setPageData(100000)} class="bg-surface-200 p-1">100000</button>
				<button onclick={() => setFirstRow()} class="bg-surface-200 p-1">setFirstRow</button>
				<button onclick={() => hiddenSecondColumn()} class="bg-surface-200 p-1"
					>hiddenSecondColumn</button
				>
				<p>Current Count:{data.length}</p>
			</div>
		</MainContent>
		<MainContent>
			<TableShowCase>
				<BaseDataTableView {data} {settings} />
			</TableShowCase>
		</MainContent>
		<MainContent>
			<MarkdownContent {metadata}>
				<Giris />
			</MarkdownContent>
		</MainContent>
	</Main>
</Page>
