<script>
</script>

<main>
	<h1 class="mb-4 text-4xl text-center mt-12 font-Inter  font-extrabold leading-none tracking-tight text-white md:text-5xl lg:text-6xl dark:text-white">Online API Tool</h1>
<p class="mb-6 mt-10 text-lg font-normal text-center 9CA3AF lg:text-xl sm:px-16 xl:px-48 dark:text-gray-400">Our Online API Tool is a versatile and user-friendly platform designed to simplify the process of working with APIs. Just like Postman, it provides developers and teams with powerful features for testing, documenting, and managing APIs. Whether you're building, testing, or monitoring APIs, our tool offers a comprehensive suite of tools to streamline your workflow. With an intuitive interface, collaboration features, and extensive customization options, it's the ideal choice for any development project. Elevate your API development and management experience with our Online API Tool and unlock the full potential of your APIs.</p>

<div class="border-2 rounded-md w-4/6 ml-64 mt-20 h-auto ">
	<p class="text-white ml-6 mt-8">Enter URL</p>
	<form>
  
	  <!-- Text Area -->
	  <div class="flex ml-5">
		  <button id="dropdown-button" data-dropdown-toggle="dropdown" class="flex-shrink-0 z-10 inline-flex items-center py-2.5 px-4 text-sm font-medium text-center text-green-400 bg-gray-600 border border-gray-300 dark:border-gray-700 dark:text-white rounded-l-lg hover:bg-gray-900 focus:ring-4 focus:outline-none focus:ring-gray-300 dark:bg-gray-600 dark:hover:bg-gray-700 dark:focus:ring-gray-800" type="button">Select a Method <svg class="w-2.5 h-2.5 ml-2.5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
	  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 4 4 4-4"/>
	</svg></button>
		  <div id="dropdown" class="z-10 hidden bg-gray-900 divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700">
			  <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdown-button">
			  <li>
				  <a href="#" class="block px-4 py-2 text-green-400 hover:bg-gray-900 dark:hover:bg-gray-600 dark:hover:text-white">GET</a>
			  </li>
			  <li>
				  <a href="#" class="block px-4 py-2  text-green-400 hover:bg-gray-900 dark:hover:bg-gray-600 dark:hover:text-white">POST</a>
			  </li>
			  <li>
				  <a href="#" class="block px-4 py-2  text-green-400 hover:bg-gray-900 dark:hover:bg-gray-600 dark:hover:text-white">PUT</a>
			  </li>
			  <li>
				  <a href="#" class="block px-4 py-2  text-green-400 hover:bg-gray-900 dark:hover:bg-gray-600 dark:hover:text-white">DELETE</a>
			  </li>
			  <li>
				  <a href="#" class="block px-4 py-2  text-green-400 hover:bg-gray-900 dark:hover:bg-gray-600 dark:hover:text-white">HEAD</a>
			  </li>
			  </ul>
		  </div>
		  <div class="relative w-4/5">
			  <input type="search" id="search-dropdown" class="block p-2.5 w-full z-20 text-sm text-white bg-gray-600 rounded-r-lg border-l-gray-100 border-l-2 border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:border-blue-500" placeholder="" required>
			  <button type="submit" class="absolute top-0 right-0 p-2.5 h-full text-sm font-medium text-black bg-green-200 rounded-r-lg border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Send</button>
	  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"/>
  
		  </div>
	  </div>
  </form>
  <div>

	<div class="bg-gray-900">
 
		<div class="flex flex-wrap mt-5 ml-10">
			<div class="flex items-center mr-4">
				<input id="red-radio" type="radio" value="" name="colored-radio" class="w-6 h-6 text-green-600 bg-gray-100 border-gray-300 focus:ring-green-500 dark:focus:ring-green-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
				<label for="red-radio" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-300 pl-3">Text</label>
			</div>
			<div class="flex items-center mr-4">
				<input id="green-radio" type="radio" value="" name="colored-radio" class="w-6 h-6 text-green-600 bg-gray-100 border-gray-300 focus:ring-green-500 dark:focus:ring-green-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
				<label for="green-radio" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-300 pl-3">JavaScript</label>
			</div>
			<div class="flex items-center mr-4">
				<input checked id="purple-radio" type="radio" value="" name="colored-radio" class="w-6 h-6 text-green-600 bg-gray-100 border-gray-300 focus:ring-green-500 dark:focus:ring-green-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
				<label for="purple-radio" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-300 pl-3">JSON</label>
			</div>
			<div class="flex items-center mr-4">
				<input id="teal-radio" type="radio" value="" name="colored-radio" class="w-6 h-6 text-green-600 bg-gray-100 border-gray-300 focus:ring-green-500 dark:focus:ring-green-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
				<label for="teal-radio" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-300 pl-3">HTML</label>
			</div>
			<div class="flex items-center mr-4">
				<input id="yellow-radio" type="radio" value="" name="colored-radio" class="w-6 h-6 text-green-600 bg-gray-100 border-gray-300 focus:ring-green-500 dark:focus:ring-green-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
				<label for="yellow-radio" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-300 pl-3">XML</label>
			</div>
		</div>
	  
		<!-- Input -->
		<div class="relative w-full mb-16">
	  
	  
		  <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your message</label>
		  <textarea id="message" rows="4" class="block p-2.5 w-full overflow-y-scroll text-sm text-white bg-gray-600 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder=""></textarea>
		  
		  </div>
	  
		  <div class="mb-6 h-auto  relative">
			<textarea id="message" rows="4" class="block p-2.5 w-full overflow-y-scroll text-sm text-white bg-gray-600 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder=""></textarea>
			<!-- <input type="text" id="large-input" class="block w-full h-fit overflow-y-scroll p-4 text-white border border-gray-300 rounded-lg bg-gray-600 sm:text-md focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"> -->
			<button type="submit" class="absolute top-0 right-0 p-2.5 mt-12  mr-7  text-sm font-medium text-black bg-green-200 rounded-md border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Copy</button>
		  </div>
		</div>

	</div>
</main>

<style>
	
</style>
