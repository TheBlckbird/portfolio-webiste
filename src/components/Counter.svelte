<script lang="ts">
    import { fly } from "svelte/transition";

    let count: number = 0;
    let decrementIsLastClicked = false;

    function decrement() {
        decrementIsLastClicked = true;
        count -= 1;
    }

    function increment() {
        decrementIsLastClicked = false;
        count += 1;
    }

    function reset() {
        count = 0;
    }
</script>

<main>
    <button class="decrement" on:click={decrement}>
        -
    </button>

    {#key count}
        <div class="count" in:fly="{{ y: decrementIsLastClicked ? 20 : -20, duration: 200 }}">
            { count }
        </div>
    {/key}

    <button class="increment" on:click={increment}>
        +
    </button>
</main>

<style lang="scss">
    @import '../styles/global.scss';

    main {
        display: flex;
        gap: 10px;
        align-items: center;
        justify-content: space-between;
        font-size: 24px;
        background: $primary-color;
        border-radius: 8px;
        color: white;

        button {
            font-size: inherit;
            appearance: none;
            border: none;
            background: $primary-color;
            color: inherit;
            border-radius: 8px;
            width: 50px;
            height: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: all .1s;

            &:hover {
                background: $primary-hover;
            }

            &:active {
                background: $primary-active;
            }
        }
    }
</style>