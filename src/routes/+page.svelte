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


<!-- Bases/IP = [(H-HR-3B-2B) + (2B*2) + (3B*3) + (HR*4) + BB]/IP 
I'll calculate Bases/G and Bases/TBF for each player using the provided formula:

Bases/G = [(H-HR-3B-2B) + (2Bx2) + (3Bx3) + (HRx4) + BB]/G
Bases/TBF = [(H-HR-3B-2B) + (2Bx2) + (3Bx3) + (HRx4) + BB]/TBF

Here are the calculations:

Seth Lugo:

H: 177, HR: 16, 3B: 6, 2B: 36
G: 33
Bases/G = [(177-16-6-36) + (36x2) + (6x3) + (16x4) + 48] / 33 = 9.7
era: 14

Paul Skenes:

H: 94, HR: 10, 3B: 1, 2B: 14
G: 23
Bases/G = [(94-10-1-14) + (14x2) + (1x3) + (10x4) + 32] / 23 = 7.48
era: 11.6

Tarik Skubal:

H: 142, HR: 15, 3B: 4, 2B: 24
G: 31
Bases/G = [(142-15-4-24) + (24x2) + (4x3) + (15x4) + 35] / 31 = 8.19
era: 11.9

Shota Imanaga:

H: 149, HR: 27, 3B: 1, 2B: 23
G: 29
Bases/G = [(149-27-1-23) + (23x2) + (1x3) + (27x4) + 28] / 29 = 9.76
era: 14.7

Tyler Anderson:

H: 158, HR: 24, 3B: 3, 2B: 32
G: 31
Bases/G = [(158-24-3-32) + (32x2) + (3x3) + (24x4) + 73] / 31 = 11


Reid Detmers:

H: 98, HR: 18, 3B: 3, 2B: 20
G: 17
Bases/G = [(98-18-3-20) + (20x2) + (3x3) + (18x4) + 38] / 17 = 12.7


Zack Wheeler:

H: 139, HR: 20, 3B: 5, 2B: 28
G: 32
Bases/G = [(139-20-5-28) + (28x2) + (5x3) + (20x4) + 52] / 32 = 9
era: 13

Miles Mikolas:

H: 194, HR: 26, 3B: 4, 2B: 51
G: 32
Bases/G = [(194-26-4-51) + (51x2) + (4x3) + (26x4) + 25] / 32 = 11.1


Lance Lynn:

H: 113, HR: 16, 3B: 1, 2B: 21
G: 23
Bases/G = [(113-16-1-21) + (21x2) + (1x3) + (16x4) + 44] / 23 = 9.9


Tyler Glasnow:

H: 92, HR: 15, 3B: 2, 2B: 27
G: 22
Bases/G = [(92-15-2-27) + (27x2) + (2x3) + (15x4) + 35] / 22 = 9.2
era: 13.6

Blake Snell:

H: 65, HR: 6, 3B: 1, 2B: 13
G: 20
Bases/G = [(65-6-1-13) + (13x2) + (1x3) + (6x4) + 44] / 20 = 7.10
era: 12.33

Logan Webb:

H: 202, HR: 11, 3B: 4, 2B: 35
G: 33
Bases/G = [(202-11-4-35) + (35x2) + (4x3) + (11x4) + 50] / 33 = 9.9
era: 14.49

george kirby 
191. in
bases/g = 10.2
era: 15.8

garret crochett
146 innings
bases/g: 7.7
era: 14.7

-->