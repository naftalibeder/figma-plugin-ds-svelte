<script lang="ts">
    import Icon from './../Icon/index.svelte';

    export let id = null;
    export let type: 'text' | 'number' | 'date' = 'text';

    // text, number, date
    export let value = null;
    export let name = null;
    export let iconText = null;
    export let borders = false;
    export let disabled = false;
    export let iconName = null;
    export let spin = false;
    export let invalid = false;
    export let errorMessage = 'Error message';
    export let placeholder = 'Input something here...';

    // number, date
    export let min: string;
    export let max: string;
    export let step: string;

    export { className as class };

    let className = '';

    function updateType(node) {
        node.type = type;
    }
</script>

{#if iconName || iconText}
    <div class="input {className}">
        <div class="icon">
            <Icon {iconName} {iconText} {spin} color="black3"/>
        </div>
        <input 
            use:updateType
            on:input
            on:change
            on:keydown
            on:focus
            on:blur
            bind:value={value}
            {id}
            {name}
            {disabled}
            {placeholder}
            {errorMessage}
            {min}
            {max}
            {step}
            class="indent"
            class:borders={borders}
            class:invalid={invalid}
        >
        {#if invalid}
            <div class="error">
                {errorMessage}
            </div>
        {/if}
    </div>
{:else}
    <div class="input {className}">
        <input 
            use:updateType
            on:input
            on:change
            on:keydown
            on:focus
            on:blur
            bind:value={value}
            {id}
            {name}
            {disabled}
            {placeholder}
            {errorMessage}
            {min}
            {max}
            {step}
            class:borders={borders}
            class:invalid={invalid}
        >
        {#if invalid}
            <div class="error">
                {errorMessage}
            </div>
        {/if}
    </div>
{/if}
<style>

    .input {
        position: relative;
        transition: flex 0s 0.2s; 
    }

    input {
        font-size: var(--font-size-xsmall);
        font-weight: var(--font-weight-normal);
        letter-spacing: var( --font-letter-spacing-neg-xsmall);
        line-height: var(--line-height);
        position: relative;
        display: flex;
        overflow: visible;
        align-items: center;
        width: 100%;
        height: 30px;
        margin: 1px 0 1px 0;
        padding: var(--size-xxsmall) var(--size-xxxsmall) var(--size-xxsmall) var(--size-xxsmall);
        color: var(--black8);
        border: 1px solid transparent;
        border-radius: var(--border-radius-small);
        outline: none;
        background-color: var(--white);
    }
    input:hover, input:placeholder-shown:hover {
		color: var(--black8);
		border: 1px solid var(--black1);
        background-image: none;
	}
	input::selection {
		color: var(--black);
		background-color: var(--blue3);
	}
	input::placeholder {
		color: var(--black3);
		border: 1px solid transparent;
	}
	input:placeholder-shown {
		color: var(--black8);
        border: 1px solid var(--black1);
        background-image: none;
	}
    input:focus:placeholder-shown {
        border: 1px solid var(--blue);
        outline: 1px solid var(--blue);
        outline-offset: -2px;
    }
	input:disabled:hover {
		border: 1px solid transparent;
	}
	input:active, input:focus {

		color: var(--black);
        border: 1px solid var(--blue);
        outline: 1px solid var(--blue);
        outline-offset: -2px;
	}
	input:disabled {
		position: relative;
		color: var(--black3);
        background-image: none;
	}
	input:disabled:active {
        outline: none;
    }

    .borders {
        border: 1px solid var(--black1);
        background-image: none;
    }
    .borders:disabled {
        border: 1px solid transparent;
        background-image: none;
    }
    .borders:disabled:placeholder-shown {
        border: 1px solid transparent;
        background-image: none;
    }
    .borders:disabled:placeholder-shown:active {
        border: 1px solid transparent;
        outline: none;
    }
    .borders:placeholder-shown {
        border: 1px solid var(--black1);
        background-image: none;
    }
    
    .indent {
        padding-left: 32px;
    }

    .invalid, .invalid:hover, .invalid:focus {
        border: 1px solid var(--red);
        outline: 1px solid var(--red);
        outline-offset: -2px;
    }

    .icon {
        position: absolute;
		top: -1px;
		left: 0;
        width: var(--size-medium);
        height: var(--size-medium);
        z-index: 1;
    }

    .error {
        color: var(--red);
        font-size: var(--font-size-xsmall);
        font-weight: var(--font-weight-normal);
        letter-spacing: var( --font-letter-spacing-neg-xsmall);
        line-height: var(--line-height);
        padding-top: var(--size-xxxsmall);
        padding-left: var(--size-xxsmall);
    }

</style>