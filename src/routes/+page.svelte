<script lang="ts">
  import { onMount } from 'svelte';

    let theme = 'light'; // default theme

    function toggleTheme() {
        theme = theme === 'light' ? 'dark' : 'light';
        document.documentElement.setAttribute('data-theme', theme);
    }

    onMount(() => {
        document.documentElement.setAttribute('data-theme', theme);
    });

    // Calculator
    let price: number = 3000000; // Default list price
    let downPayment: number = 10; // Default down payment percentage
    let vat: number = 12; // Default VAT percentage
    let otherCharges: number = 8.5; // Default other charges percentage
    let result: number | undefined; // This will hold the calculation result

    function compute(): void {
        const dpAmount: number = price * (downPayment / 100);
        const vatAmount: number = price * (vat / 100);
        const otherChargesAmount: number = price * (otherCharges / 100);
        result = price + vatAmount + otherChargesAmount - dpAmount;
    }
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="SMDC Condominium calculator app" />
</svelte:head>

<div class="flex flex-col min-h-screen">
    <header class="flex justify-between items-center p-4 px-8">
        <div>
            <h1 class="text-2xl md:text-3xl font-bold text-center">SMDC Calculator</h1>
        </div>
        <div>
            <label class="flex cursor-pointer justify-end gap-2 items-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5"/><path d="M12 1v2M12 21v2M4.2 4.2l1.4 1.4M18.4 18.4l1.4 1.4M1 12h2M21 12h2M4.2 19.8l1.4-1.4M18.4 5.6l1.4-1.4"/></svg>
                <input type="checkbox" checked={theme === 'dark'} class="toggle theme-controller" on:click={toggleTheme}/>
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path></svg>
            </label>
        </div>
    </header>
    <div class="flex flex-col items-center px-4">
        <div class="w-full max-w-4xl">
            <p class="text-center text-gray-600">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 shadow-lg rounded-lg">
                <div>
                    <div class="form-control">
                        <label class="label" for="list-price">List Price</label>
                        <input type="number" id="list-price" bind:value={price} class="input input-bordered w-full" />
                    </div>
                    <div class="form-control">
                        <label class="label" for="down-payment">Down Payment %</label>
                        <input type="number" id="down-payment" bind:value={downPayment} class="input input-bordered w-full" />
                    </div>
                    <div class="form-control">
                        <label class="label" for="vat">VAT %</label>
                        <input type="number" id="vat" bind:value={vat} class="input input-bordered w-full" />
                    </div>
                    <div class="form-control">
                        <label class="label" for="other-charges">Other Charges %</label>
                        <input type="number" id="other-charges" bind:value={otherCharges} class="input input-bordered w-full" />
                    </div>
                    <button class="btn btn-primary mt-4" on:click={compute}>Compute</button>
                </div>
                <div>
                    {#if result !== undefined}
                    <div class="card bg-base-100 shadow-xl p-4">
                        <h2 class="text-lg font-semibold">Result:</h2>
                        <p class="text-xl">Total Cost: ${result.toLocaleString('en-US', { style: 'currency', currency: 'USD' })}</p>
                    </div>
                    {:else}
                    <div class="card bg-base-100 shadow-xl p-4 h-40 flex items-center justify-center">
                        <p class="text-lg text-gray-500">Results will appear here</p>
                    </div>
                    {/if}
                </div>
            </div>
        </div>
    </div>
</div>

<!-- <div class="flex flex-col min-h-screen">
    <div class="p-4 text-right">
        <label class="flex cursor-pointer justify-end gap-2">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5"/><path d="M12 1v2M12 21v2M4.2 4.2l1.4 1.4M18.4 18.4l1.4 1.4M1 12h2M21 12h2M4.2 19.8l1.4-1.4M18.4 5.6l1.4-1.4"/></svg>
            <input type="checkbox" checked={theme === 'dark'} class="toggle theme-controller" on:click={toggleTheme}/>
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path></svg>
        </label>
    </div>
    <div class="flex items-center justify-center flex-grow">
        <div class="p-4 md:p-8">
            <h1 class="text-2xl md:text-3xl font-bold text-center mb-6">SMDC Condominium Calculator</h1>
            <p class="text-gray-600 text-sm md:text-base mb-6">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="form-control w-full max-w-md mx-auto">
                    <label class="label" for="list-price">
                        <span class="label-text">List Price</span>
                    </label>
                    <input type="number" id="list-price" bind:value={price} class="input input-bordered w-full" />
                    
                    <label class="label" for="down-payment">
                        <span class="label-text">Down Payment %</span>
                    </label>
                    <input type="number" id="down-payment" bind:value={downPayment} class="input input-bordered w-full" />
        
                    <label class="label" for="vat">
                        <span class="label-text">VAT %</span>
                    </label>
                    <input type="number" id="vat" bind:value={vat} class="input input-bordered w-full" />
        
                    <label class="label" for="other-charges">
                        <span class="label-text">Other Charges %</span>
                    </label>
                    <input type="number" id="other-charges" bind:value={otherCharges} class="input input-bordered w-full" />
        
                    <button class="btn btn-primary mt-4" on:click={compute}>Compute</button>
                </div>
                
                {#if result !== undefined}
                <div class="card bg-base-100 shadow-xl p-4">
                    <h2 class="text-lg font-semibold">Result:</h2>
                    <p class="text-xl">Total Cost: ${result.toLocaleString('en-US', { style: 'currency', currency: 'USD' })}</p>
                </div>
                {/if}
            </div>
        </div>
        
    </div>
</div>
 -->
