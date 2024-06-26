<script lang="ts">
	import Intro from '$lib/Intro.svelte';
	import { Button, GradientButton, Dropdown, DropdownItem, ChevronRight, DropdownDivider, } from 'flowbite-svelte';
	import * as XLSX from 'xlsx';
	import { onMount } from 'svelte';

	export let data;

	let showUploadSection = false;
	let showCreateSection = false;
	let fileInput;
	let rowData = [];
	let numRows = 8;
	let numCols = 13;
	let selectedCell = null;
	let fileName = "";
	
	
	// download logic:
	function downloadSheet(fileExt) {
		const tableData = document.querySelector("tbody");

		// creating workbook object
		const tableWbObj = XLSX.utils.table_to_book(tableData, { sheet: "Sheet 1" });

		// pushing our table content inside the workbook along with file metadata
		XLSX.write(tableWbObj, { bookType: fileExt, bookSST: true, type: "base64" });

		// for giving unique name to files
		var uniqueNum = Math.floor(100 + Math.random() * 900);
		var uniqueStr = Math.random().toString(36).substr(2, 4);
		
		if (showUploadSection) {
			// creating file on user's machine i.e. triggering download from Upload Section
			XLSX.writeFile(tableWbObj, `${fileName}_${uniqueNum + uniqueStr}.` + fileExt);
		} else {
			// creating file on user's machine i.e. triggering download from Create Section
			XLSX.writeFile(tableWbObj, `Spreadsheet_${uniqueNum + uniqueStr}.` + fileExt);
		}
	};


	// create logic:
	function createAddRow() {
		numRows++;
	};

	function createAddColumn() {
		numCols++;
	};


	// upload logic:
	function handleFileChange(event) {
		const file = event.target.files[0];

		// Saving filename without extension for future use in global variable
		let fileNameWithExt = file.name;
		fileName = fileNameWithExt.replace(/\.[^/.]+$/, "");

		if (file) {
			// get file extension
			var inputFileExt = fileNameWithExt.split(".").pop().toLowerCase();

			// list of allowed file extensions
			var allowedExts = ["csv", "xlsx", "xls"];

			if (allowedExts.includes(inputFileExt)) {
                parseSheet(file);
            } else {
                alert('Invalid File Extension: ' + inputFileExt);
                // Reset the input field
				fileInput.value = '';
            }
		} else {
            alert('No File Selected');
        }
  	};

  	function parseSheet(file) {
		const sheetReader = new FileReader();

		sheetReader.onloadend = (e) => {
			const data = new Uint8Array(e.target.result);
			const workbook = XLSX.read(data, { type: 'array' });
			const firstSheet = workbook.Sheets[workbook.SheetNames[0]];
			const jsonData = XLSX.utils.sheet_to_json(firstSheet, { header: 1 });

			// Set numRows and numCols based on parsed data
			numRows = jsonData.length;
			numCols = Math.max(...jsonData.map(row => row.length));

			// Initialize rowData with parsed data
			rowData = jsonData.map(dataRow => {
				const emptyCells = Array(numCols - dataRow.length).fill('');
				return dataRow.concat(emptyCells);
			});

			if (numRows !== 0 && numCols !== 0) {
				showUploadSection = !showUploadSection;
			} else {
				alert("Empty File Selected");
			}
			
		};

		sheetReader.readAsArrayBuffer(file);
	};

	function uploadAddRow() {
		rowData.push(Array(numCols).fill(''));
		numRows++;
	};

	function uploadAddColumn() {
		rowData.forEach(row => row.push(''));
		numCols++;
	};

	// Common Functions for Upload and Create Sections

	function getColumnName(index) {
		if (index < 26) {
			// A to Z
			return String.fromCharCode(65 + index);
		} else {
			// After Z, AA, AB, AC...
			let firstChar = String.fromCharCode(65 + Math.floor(index / 26) - 1);
			let secondChar = String.fromCharCode(65 + (index % 26));
			return `${firstChar}${secondChar}`;
		};
	};

	function deleteRow() {
		if (numRows > 1) 
			numRows--;
	};

	function deleteColumn() {
		if (numCols > 1) 
			numCols--;
	};

	onMount(() => {
		// Initialize rowData with empty strings
		rowData = Array.from({ length: numRows }, () => Array(numCols).fill(''));
	});
</script>

<Intro heading={data.meta.title} description={data.meta.description} />

<section class="bg-white dark:bg-gray-900">
	{#if !showCreateSection && !showUploadSection}
		<div class="flex justify-center items-center section-button mt-2 mb-4 mr-4 ml-4"> <!--Two buttons added from flowbite-svelte-->
			<!-- Upload Button -->
			<Button size="xl" outline color="blue" class="mr-2 p-6" on:click={()=>{ fileInput.click() }}><b>Upload Your Spreadsheet</b></Button>
			<input id="sheetuploader" type="file" class="hidden" accept=".csv, .xlsx, .xls" bind:this={fileInput} on:change={handleFileChange} />

			<!-- Create Button -->
			<GradientButton size="xl" color="blue" class="ml-2 p-6" on:click={()=>{showCreateSection = !showCreateSection}}><b>Create New Spreadsheet</b></GradientButton>
		</div>

	{:else if showUploadSection}
		<div class="flex justify-start mt-4 ml-6 mr-4 mb-4">
			<GradientButton size="md" outline color="blue">Menu<ChevronRight /></GradientButton>
			<Dropdown placement="right-start">
				<DropdownItem on:click={() => {downloadSheet("csv")}}>Download <b>CSV</b></DropdownItem>
				<DropdownItem on:click={() => {downloadSheet("xlsx")}}>Download <b>XLSX</b></DropdownItem>
				<DropdownItem on:click={() => {downloadSheet("xls")}}>Download <b>XLS</b></DropdownItem>
				<DropdownDivider />
				<DropdownItem on:click={uploadAddRow}>Add Row</DropdownItem>
				<DropdownItem on:click={deleteRow}>Delete Row</DropdownItem>
				<DropdownDivider />
				<DropdownItem on:click={uploadAddColumn}>Add Column</DropdownItem>
				<DropdownItem on:click={deleteColumn}>Delete Column</DropdownItem>
				<DropdownDivider />
				<DropdownItem on:click={() => {showUploadSection = false; selectedCell = null; rowData = []; numRows=8; numCols=13;}}>Exit Editor</DropdownItem>
			</Dropdown>
		</div>

		<div class="w-100 h-100 ml-4 mr-4 mb-4 scrollable-container">
			<table>
				<thead>
					<tr>
						<th class="describers" />
						{#each Array(numCols) as _, i}
							<th class="content describers">{getColumnName(i)}</th>
						{/each}
					</tr>
				</thead>
				<tbody>
					{#each Array(numRows) as _, rowIndex}
						<tr>
							<td class="row-numbering describers"><b>{rowIndex + 1}</b></td>
							{#each Array(numCols) as _, colIndex}
								{#if typeof rowData[rowIndex][colIndex] !== "undefined"}
									<td contenteditable="true" class="content">{rowData[rowIndex][colIndex]}</td>
								{:else}
									<td contenteditable="true" class="content" />
								{/if}
							{/each}
						</tr>
					{/each}
				</tbody>
			</table>
		</div>

	{:else if showCreateSection}
		
		<div class="flex justify-start mt-4 ml-6 mr-4 mb-4">
			<GradientButton size="md" outline color="blue">Menu<ChevronRight /></GradientButton>
			<Dropdown placement="right-start">
				<DropdownItem on:click={() => {downloadSheet("csv")}}>Download <b>CSV</b></DropdownItem>
				<DropdownItem on:click={() => {downloadSheet("xlsx")}}>Download <b>XLSX</b></DropdownItem>
				<DropdownItem on:click={() => {downloadSheet("xls")}}>Download <b>XLS</b></DropdownItem>
				<DropdownDivider />
				<DropdownItem on:click={createAddRow}>Add Row</DropdownItem>
				<DropdownItem on:click={deleteRow}>Delete Row</DropdownItem>
				<DropdownDivider />
				<DropdownItem on:click={createAddColumn}>Add Column</DropdownItem>
				<DropdownItem on:click={deleteColumn}>Delete Column</DropdownItem>
				<DropdownDivider />
				<DropdownItem on:click={() => {showCreateSection = false; rowData = []; numRows=8; numCols=13;}}>Exit Editor</DropdownItem>
			</Dropdown>
		</div>	
	
		<div class="w-100 h-100 ml-4 mr-4 mb-4 scrollable-container">
			<table>
				<thead>
					<tr>
						<th class="describers" />
						{#each Array(numCols) as _, i}
							<th class="content describers">{getColumnName(i)}</th>
						{/each}
					</tr>
				</thead>
				<tbody>
					{#each Array(numRows) as _, rowIndex}
						<tr>
							<td class="row-numbering describers"><b>{rowIndex + 1}</b></td>
							{#each Array(numCols) as _, colIndex}
								<td contenteditable="true" class="content" />
							{/each}
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	{/if}
</section>

<style>
	table {
		border-collapse: collapse;
		background-color: azure;
	}

	table, th {
		/* border: 1px solid #236cf1; */
		border: 1px solid black;
		padding: 8px;
		color: #1e1818;
	}

	td {
		padding: 12px;
		/* border: 1px solid #236cf1; */
		border: 1px solid black;
		/* text-align: center; */ /*If needed*/
	}

	.content {
		width: 125px;
		overflow-x: auto;
		white-space: nowrap;
	}

	.row-numbering {
		width: 35px;
		/* border: 1px solid #236cf1; */
		border: 1px solid black;
	}

	.describers {
		/* background-color: #8f9bf1; */
		/* background-color: #3b83cc; */
		background-color: #1E66F2;
		color: azure;
	}

	/* For Implementing Scroll Functionality */
	.scrollable-container { 
		overflow-x: auto; 
		overflow-y: auto; 
		max-height: 385px;
		max-width: fit-content;
	}

	.section-button {
		max-width: 100%;
	}
</style>
