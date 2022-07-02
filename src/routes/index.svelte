<script>
	import { initializeApp } from 'firebase/app';

	// Add Firebase products that you want to use
	import { getMessaging, getToken } from 'firebase/messaging';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	const firebaseConfig = {
		apiKey: 'AIzaSyAxtx_E08rgGWigQs4BrP1us_2Kijl89jw',
		authDomain: 'okymapp-e42bb.firebaseapp.com',
		databaseURL: 'https://okymapp-e42bb-default-rtdb.firebaseio.com',
		projectId: 'okymapp-e42bb',
		storageBucket: 'okymapp-e42bb.appspot.com',
		messagingSenderId: '147080091155',
		appId: '1:147080091155:web:bad9f99878aea5cc1811e6',
		measurementId: 'G-NQY4L06HWM'
	};

	function requestPermission() {
		console.log('Requesting permission...');
		Notification.requestPermission().then((permission) => {
			if (permission === 'granted') {
				localStorage.setItem('permission', permission);
				console.log('Notification permission granted.');
				goto('/mapa');
			} else {
				localStorage.removeItem('permission');
			}
		});
	}

	function subscribeUser(token) {
		console.log('subscribiendo al usuario', token);
	}

	let app;
	let messaging;

	onMount(() => {
		app = initializeApp(firebaseConfig);
		messaging = getMessaging(app);
		const permission = localStorage.getItem('permission');
		if (permission) {
			goto('/mapa');
		}
	});
</script>

<!-- This example requires Tailwind CSS v2.0+ -->
<div>
	<div>
		<img
			class="h-32 w-full object-cover lg:h-48"
			src="https://www.asuncion.gov.py/wp-content/uploads/2019/05/Drone-Ban%CC%83ado-Inundacion-Rio-Paraguay.jpg"
			alt=""
		/>
	</div>
	<div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="-mt-12 sm:-mt-16 sm:flex sm:items-end sm:space-x-5">
			<div class="flex">
				<img
					class="h-24 w-24 rounded-full ring-4 ring-white sm:h-32 sm:w-32"
					src="https://us.123rf.com/450wm/pshonka/pshonka1602/pshonka160200095/52816258-nube-de-lluvia-icono-de-mapa-plano-del-perno-puntero-del-mapa-marcadores-de-mapa-meteorolog%C3%ADa-clima-.jpg?ver=6"
					alt=""
				/>
			</div>
			<div
				class="mt-6 sm:flex-1 sm:min-w-0 sm:flex sm:items-center sm:justify-end sm:space-x-6 sm:pb-1"
			>
				<div class="sm:hidden md:block mt-6 min-w-0 flex-1">
					<h1 class="text-5xl font-bold text-gray-900">OkymApp</h1>
				</div>
				<div />
				<!-- Heroicon name: solid/mail -->
				<svg
					class="-ml-1 mr-2 h-5 w-5 text-gray-400"
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				/>
			</div>
		</div>
	</div>
</div>
<!-- This example requires Tailwind CSS v2.0+ (Porcentaje de lluvia / ZONA DE RIESGO)
<div>
	<h2 class="text-lg leading-6 font-medium text-gray-900">Porcentaje de inundaciones</h2>
	<dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">
		<div class="px-4 py-5 bg-white shadow rounded-lg overflow-hidden sm:p-6">
			<dt class="text-sm font-medium text-gray-500 truncate">Probabilidades</dt>
			<dd class="mt-1 text-3xl font-semibold text-gray-900">71,897</dd>
		</div>
	</dl>
</div> -->

<!-- This example requires Tailwind CSS v2.0+ -->
<div class="relative bg-white overflow-hidden">
	<div class="max-w-7xl mx-auto">
		<div
			class="relative z-10 pb-8 bg-white sm:pb-16 md:pb-20 lg:max-w-2xl lg:w-full lg:pb-28 xl:pb-32"
		>
			<svg
				class="hidden lg:block absolute right-0 inset-y-0 h-full w-48 text-white transform translate-x-1/2"
				fill="currentColor"
				viewBox="0 0 100 100"
				preserveAspectRatio="none"
				aria-hidden="true"
			>
				<polygon points="50,0 100,0 50,100 0,100" />
			</svg>

			<div>
				<div class="relative pt-6 px-4 sm:px-6 lg:px-8">
					<nav
						class="relative flex items-center justify-between sm:h-10 lg:justify-start"
						aria-label="Global"
					/>
				</div>

				<!--
            Mobile menu, show/hide based on menu open state.
  
            Entering: "duration-150 ease-out"
              From: "opacity-0 scale-95"
              To: "opacity-100 scale-100"
            Leaving: "duration-100 ease-in"
              From: "opacity-100 scale-100"
              To: "opacity-0 scale-95"
          -->
				<div
					class="absolute z-10 top-0 inset-x-0 p-2 transition transform origin-top-right md:hidden"
				/>
			</div>

			<main
				class="mt-10 mx-auto max-w-7xl px-4 sm:mt-12 sm:px-6 md:mt-16 lg:mt-20 lg:px-8 xl:mt-28"
			>
				<div class="sm:text-center lg:text-left">
					<h1 class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl">
						<span class="block xl:inline">Que no te lleve el raudal:</span>
						<span class="block text-indigo-600 xl:inline"> alertas al instante</span>
					</h1>
					<p
						class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0"
					>
						Mantenete al tanto si estás en zona de riesgo y dónde podes ir de manera rápida y
						accecible
					</p>
					<div class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start">
						<div class="rounded-md shadow" />
						<div class="mt-3 sm:mt-0 sm:ml-3">
							<a
								href="#"
								class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-indigo-700 bg-indigo-100 hover:bg-indigo-200 md:py-4 md:text-lg md:px-10"
								on:click={async () => {
									requestPermission();
									const token = await getToken(messaging, {
										vapidKey:
											'BDsqeLFFoH0RxAqPrNSLQ1EFPeW8LPlpXA4Y52xVrfg81W3ZegtOQi1OcN0ayN8-_kZ1ME_3rDEJXL_puBMy6D8'
									});
									subscribeUser(token);
								}}
							>
								Registrate
							</a>
						</div>
					</div>
				</div>
			</main>
		</div>
	</div>
	<div class="lg:absolute lg:inset-y-0 lg:right-0 lg:w-1/2">
		<img
			class="h-56 w-full object-cover sm:h-72 md:h-96 lg:w-full lg:h-full"
			src="https://cdn2.opendemocracy.net/media/images/1.2e16d0ba.fill-1200x630_0kxGgZK.jpg"
			alt=""
		/>
	</div>
</div>
