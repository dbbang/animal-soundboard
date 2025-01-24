<script lang="ts">
	import Button from '$lib/components/dumb-button.svelte';
	import ChewFart from '$lib/fart-sounds/chewfart.mp3';
	import Fart1 from '$lib/fart-sounds/fart.mp3';
	import Fart2 from '$lib/fart-sounds/fart2.mp3';
	import Fart3 from '$lib/fart-sounds/fart3.mp3';
	import Fart4 from '$lib/fart-sounds/fart4.mp3';
	import ChildFart from '$lib/fart-sounds/akh.mp3';
	import Wind from '$lib/fart-sounds/wind-woosh.mp3';

	type Animals = {
		name: string;
		img: string;
	};

	const animals: Animals[] = [
		{
			name: 'pig',
			img: 'https://preview.redd.it/i-want-a-pet-pig-experiences-v0-ibtvtydyggec1.jpeg?width=640&crop=smart&auto=webp&s=e3ebb79dc87b57440793f1b1a5c07b3974cda09e'
		},
		{
			name: 'cow',
			img: 'https://upload.wikimedia.org/wikipedia/commons/0/0c/Cow_female_black_white.jpg'
		},
		{
			name: 'chicken',
			img: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRIoa91GFHT65lskWYAmVqurY_LWPT9PovIhA&s'
		},
		{
			name: 'fish',
			img: 'https://www.aqueon.com/-/media/project/oneweb/aqueon/us/blog/ways-to-know-your-fish-are-happy/fish-are-happy-and-healthy-1.png'
		},
		{
			name: 'rabbit',
			img: 'https://hips.hearstapps.com/hmg-prod/images/baby-rabbit-in-meadow-royalty-free-image-1717078659.jpg?crop=0.88763xw:1xh;center,top&resize=1200:*'
		},
		{
			name: 'lamb',
			img: 'https://previews.123rf.com/images/alexis84/alexis841303/alexis84130300292/18755757-cute-lamb.jpg'
		},
		{
			name: 'small child',
			img: 'https://d1amk1w0mr5k0.cloudfront.net/blog/wp-content/uploads/2013/04/WOYC-Non-TT_2.png'
		},
		{
			name: 'duck',
			img: 'https://www.techspot.com/images2/news/bigimage/2025/01/2025-01-22-image-16.jpg'
		},
		{
			name: 'sheep',
			img: 'https://t3.ftcdn.net/jpg/05/74/38/22/360_F_574382292_nAsvz0py4Maa0qqkfMbwqI76kJpDkHmU.jpg'
		}
	];

	let selectedAnimals: string[] = [];

	const toggleSelection = (animal: string) => {
		selectedAnimals = selectedAnimals.includes(animal)
			? selectedAnimals.filter((item) => item !== animal)
			: [...selectedAnimals, animal];
	};

	const clearSelections = () => {
		selectedAnimals = [];
	};

	const playFart = () => {
		let audio: HTMLAudioElement;

		if (selectedAnimals.includes('pig') || selectedAnimals.includes('cow')) {
			audio = new Audio(Fart1);
		} else if (selectedAnimals.includes('small child')) {
			audio = new Audio(ChildFart);
		} else if (selectedAnimals.length >= 2 && selectedAnimals.length <= 3) {
			audio = new Audio(Fart2);
		} else if (selectedAnimals.length >= 4 && selectedAnimals.length <= 5) {
			audio = new Audio(Fart3);
		} else if (selectedAnimals.length >= 6 && selectedAnimals.length <= 7) {
			audio = new Audio(Fart4);
		} else if (selectedAnimals.length >= 8 && selectedAnimals.length <= 9) {
			audio = new Audio(ChewFart);
		} else {
			audio = new Audio(Wind);
		}

		audio.play();
	};
</script>

<div class="bg-pink-500">
	<h1 class="text-center text-4xl italic text-green-50">
		Please select the animals you consumed this week to hear how your fart will sound
	</h1>
	<div class="mx-10 my-10 grid grid-cols-3 grid-rows-3 gap-5">
		{#each animals as { name, img }}
			<div class="flex flex-col items-center">
				<button type="button" class="focus:outline-none" on:click={() => toggleSelection(name)}>
					<img
						src={img}
						alt={name}
						class={`h-40 w-40 object-cover ${
							selectedAnimals.includes(name)
								? 'border-8 border-green-500'
								: 'hover:border hover:border-4 hover:border-yellow-500'
						}`}
					/>
					<p class="text-green-50">{name}</p>
				</button>
			</div>
		{/each}
	</div>

	<div class="mt-4 flex justify-center text-green-100">
		<Button text="Fart!" onClick={playFart} />
	</div>

	<div class="mt-4 flex justify-center text-green-50">
		<Button text="Clear Selection" onClick={clearSelections} />
	</div>
</div>
