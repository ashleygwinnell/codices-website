<script>
	import { onMount } from "svelte";
	import { writable } from "svelte/store";

	const PageState ={
		NONE: "none",
		QK: "qk",
		MOAR: "moar",
		ABOUT: "about",
		PRESS: "press"
	};

	let pageState = writable(PageState.NONE);

	let overQK = false;
	let overMOAR = false;
	
	$: {
		$pageState;
	}
	$: blurbsVisible = $pageState === PageState.ABOUT || $pageState === PageState.PRESS;

	let switchPage = (page) => {
		let prev = $pageState;
		if (
			(page === PageState.ABOUT && $pageState === PageState.ABOUT) ||
			(page === PageState.PRESS && $pageState === PageState.PRESS)
			) {
			page = PageState.NONE;
		}
		$pageState = page;
	};

	let mounted = false;
	onMount(()=>{
		setTimeout(()=>{
			mounted = true;
		}, 100);
	})

</script>

	<!-- Desktop page -->
	<div class="desktop-only">
		<div class="background" class:visible={mounted} ></div>
		<div class="paper-container unselectable" 
			class:move-left={$pageState === PageState.QK} 
			class:move-right={$pageState === PageState.MOAR}
			>
			
			<div class="paper" on:click={()=>{ $pageState = PageState.NONE; }}>
				
				<div class='logo-container'>
					<img src="assets/logo.png" class="logo" title="Codices" alt="Codices" />
				</div>

				<div class="product-container" class:faded-up={blurbsVisible}>
					<div class='fl ta-c ml-5pc w-45pc c-h' style='height:120px;' 
						on:mouseover={(e)=>{ overMOAR = true; }}
						on:mouseout={(e)=>{ overMOAR = false; }}
						on:focus={(e)=>{ overMOAR = true; }}
						on:blur={(e)=>{ overMOAR = false; }}
						on:click|stopPropagation={()=>{ $pageState = PageState.MOAR; }}>
						<img class="w-40pc product-logo" class:over={overMOAR} class:faded-up={$pageState === PageState.MOAR} src="assets/logo-moar-black.png" alt="Moar" title="Moar"/>
						
						<div class="product-logo-full" class:faded-up={$pageState === PageState.MOAR}>
							<img class="w-70pc" src="assets/logo-moar-full.png" alt="Moar" title="Moar" />
							<p>Our livestreaming platform for anyone to create live shows</p>
							<!-- <a class='product-btn moar' href="/" target="new">Find Out More</a> -->
							<a class='product-btn moar' href="/" on:click|preventDefault>Coming Soon</a>
						</div>
					</div>
					<div class='fl ta-c mr-5pc w-45pc c-h' style='height:120px;'
						on:mouseover={(e)=>{ overQK = true; }}
						on:mouseout={(e)=>{ overQK = false; }}
						on:focus={(e)=>{ overQK = true; }}
						on:blur={(e)=>{ overQK = false; }}
						on:click|stopPropagation={()=>{ $pageState = PageState.QK;   }}>
						<img class="w-35pc product-logo" class:over={overQK} class:faded-up={$pageState === PageState.QK}  src="assets/logo-quizkit-black.png" alt="Quiz Kit" title="Quiz Kit" />
						<div class="product-logo-full" class:faded-up={$pageState === PageState.QK}>
							<img class="w-70pc" src="assets/logo-quizkit-full.png" alt="Quiz Kit" title="Quiz Kit" />
							<p>Our Twitch extension for anyone to create live shows.</p>
							<a class='product-btn qk' href="https://www.quizkit.io/" target="new">Find Out More</a>
						</div>
					</div>
				</div>

				<nav class='oa ta-c' class:faded-up={blurbsVisible}>
					<p class="ta-c">
						<a href='/' class:selected={$pageState === PageState.ABOUT} on:click|preventDefault|stopPropagation={()=>{ $pageState = PageState.ABOUT; }}>About</a> &nbsp;|&nbsp; 
						<a href='/' class:selected={$pageState === PageState.PRESS} on:click|preventDefault|stopPropagation={()=>{ $pageState = PageState.PRESS; }}>Press</a> &nbsp;|&nbsp; 
						<a href='mailto:info@codices.io'>Contact</a>
					</p>
				</nav>
				
				<div class='blurb-container' class:faded-up={blurbsVisible}>
					
					<div class="text ta-c" class:visible={$pageState === PageState.ABOUT}>
						<p>We are democratising the creation of live interactive shows.<br/><br/></p>
						<p>Our first product Quiz Kit on has been installed on over 1m Twitch channels and has powered shows seen by over 100m unique viewers across the world.<br/><br/></p>
						<p>In 2022 we are launching Moar, the first platform dedicated to the creation, distribution and community development for live interactive shows.</p>
					</div>
					
					<div class="text ta-c" class:visible={$pageState === PageState.PRESS}>
						<p>For any press enquires please contact <a href='mailto:press@codices.io'>press@codices.io</a></p>
						<p>Our latest media pack for Moar can be found here.</p>
					</div>
				</div>

			</div>
			<div class="moar-swipe" class:opacity1={$pageState === PageState.MOAR}></div>
			<div class="quizkit-swipe" class:opacity1={$pageState === PageState.QK}></div>
		</div>
	</div>

	<!-- Mobile page -->
	<div class='mobile-only unselectable'>
		<div class="background" class:visible={mounted} ></div>
		<header>
			<a href='/' on:click|preventDefault={()=>{ switchPage(PageState.NONE); }}><img src="assets/logo.png" class="logo" title="Codices" alt="Codices" /></a>
		</header>

		<div class="product-container">
			<div class='fl ta-c ml-5pc w-45pc c-h' style='height:120px;' 
				on:mouseover={(e)=>{ overMOAR = true; }}
				on:mouseout={(e)=>{ overMOAR = false; }}
				on:focus={(e)=>{ overMOAR = true; }}
				on:blur={(e)=>{ overMOAR = false; }}
				on:click|stopPropagation={()=>{ $pageState = PageState.MOAR; }}>
				<img class="w-40pc product-logo" class:over={overMOAR} src="assets/logo-moar-white.png" alt="Moar" title="Moar"/>
			</div>
			<div class='fl ta-c mr-5pc w-45pc c-h' style='height:120px;'
				on:mouseover={(e)=>{ overQK = true; }}
				on:mouseout={(e)=>{ overQK = false; }}
				on:focus={(e)=>{ overQK = true; }}
				on:blur={(e)=>{ overQK = false; }}
				on:click|stopPropagation={()=>{ $pageState = PageState.QK;   }}>
				<img class="w-35pc product-logo" class:over={overQK}  src="assets/logo-quizkit-white.png" alt="Quiz Kit" title="Quiz Kit" />
			</div>
		</div>

		
		<div class="moar-swipe" class:opacity1={$pageState === PageState.MOAR}></div>
		<div class="left-swipe" class:opacity1={$pageState === PageState.MOAR}>
			<div class='stripes'></div>
			<div class='container'>
				<div class='w-50pc m-auto ta-c p-70'>
					<img class="w-70pc" src="assets/logo-moar-full.png" alt="Moar" title="Moar" />
					<h3 class="mb-0">Our livestreaming platform for anyone to create live shows</h3>
				</div>
			</div>
			<!-- <a class='product-btn ta-c moar' href="/" target="new">Find Out More</a> -->
			<a class='product-btn ta-c moar' href="/" on:click|preventDefault>Coming Soon</a>

			<div class="right-shadow ta-r"
			class:opacity1={$pageState === PageState.MOAR}
			on:click={()=>{ switchPage(PageState.NONE); }}
			>
			<img class='fr caret-right' src="assets/caret-r.png" alt="Caret" /> 
			</div>
		</div>

		<div class="quizkit-swipe" class:opacity1={$pageState === PageState.QK}></div>
		<div class="right-swipe" class:opacity1={$pageState === PageState.QK}>
			<div class='container'>
				<div class='w-50pc m-auto ta-c p-70'>
					<img class="w-70pc" src="assets/logo-quizkit-full.png" alt="Quiz Kit" title="Quiz Kit" />
					<h3 class="mb-0">Our Twitch extension for anyone to create live shows.</h3>
					
				</div>
			</div>
			<a class='product-btn ta-c qk' href="https://www.quizkit.io/" target="new">Find Out More</a>

			
			<div class="left-shadow" 
				on:click={()=>{ switchPage(PageState.NONE); }} 
				class:opacity1={$pageState === PageState.QK}
				>
				<img class='caret-left' src="assets/caret-l.png" alt="Caret" />
			</div>
		</div>
		


		<nav class='mobile oa ta-c' class:faded-up={blurbsVisible}>
			<p class="ta-c">
				<a href='/' 
					class:selected={$pageState === PageState.ABOUT} 
					on:click|preventDefault|stopPropagation={()=>{ switchPage(PageState.ABOUT); }}>About</a> &nbsp;|&nbsp; 
				<a href='/' 
					class:selected={$pageState === PageState.PRESS} 
					on:click|preventDefault|stopPropagation={()=>{ switchPage(PageState.PRESS); }}>Press</a> &nbsp;|&nbsp; 
				<a href='mailto:info@codices.io'>Contact</a>
			</p>
		</nav>

		<div class='blurb-container' class:faded-up={blurbsVisible}>
					
			<div class="text ta-c" class:visible={$pageState === PageState.ABOUT}>
				<p>We are democratising the creation of live interactive shows.<br/><br/></p>
				<p>Our first product Quiz Kit on has been installed on over 1m Twitch channels and has powered shows seen by over 100m unique viewers across the world.<br/><br/></p>
				<p>In 2022 we are launching Moar, the first platform dedicated to the creation, distribution and community development for live interactive shows.</p>
			</div>
			
			<div class="text ta-c" class:visible={$pageState === PageState.PRESS}>
				<p>For any press enquires please contact <a href='mailto:press@codices.io'>press@codices.io</a></p>
				<p>Our latest media pack for Moar can be found here.</p>
			</div>
		</div>

		<div class='blurb-close ta-c' on:click={()=>{ switchPage(PageState.NONE); }} class:open={blurbsVisible}>
			<img class='caret-bottom' src="assets/caret.png" alt="Caret" />
		</div>

	</div>
