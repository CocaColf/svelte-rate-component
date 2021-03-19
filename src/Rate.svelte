<script>
    import { createEventDispatcher, onMount } from 'svelte';

    const dispatch = createEventDispatcher();

    export let modelValue = 0;
    export let allowHalf = false;
    export let disabled = false;
    export let allowClear = false;
    export let count = 5;
    export let strokeColor = '#f7ba2a';
    export let backgroundColor = '#c6d1de';
    export let toolTips = [];
    export let icon = 'icon-favorite-filling';

    let mapCountArr = [];

    $: score = Number(modelValue);
    $: touchHalf = modelValue !== Number(modelValue);

    onMount(() => {
        if (count > 0) {
            mapCountArr = [];
            for (let i = 1; i <= count; i++) {
                mapCountArr.push(i);
            }
        }
    })

    const getToolTip = (index) => {
        return toolTips[index] || '';
    } 

    const handleMouseEnter = (item, event) => {
        if (disabled) {
            return;
        }

        if (allowHalf) {
            updateTouchHalf(item, event);
            score = touchHalf ? item - 0.5 : item;
            return;
        }

        score = item;
    }

    const handleMouseLeave = () => {
        if (disabled) {
            return;
        }
        if (allowHalf) {
            touchHalf = Number(modelValue) !== Math.floor(Number(modelValue));
        }

        score = Number(modelValue);
    }

    const updateTouchHalf = (item, event) => {
        let target = document.getElementsByClassName(`star${item}`)[0];

        if (target && event.offsetX <= target.clientWidth / 2) {
            touchHalf = true;
            return;
        }

        touchHalf = false;
    }

    const handleClick = () => {
        if (disabled) {
            return;
        }

        let clearValue = false;
        let emitValue = 0;

        if (allowClear) {
            clearValue = Number(modelValue) === score;
        }

        emitValue = clearValue ? 0 : Number(score);

        dispatch('change', emitValue);
    }
    
</script>

<div class="xl-rate-wrap">
    {#each mapCountArr as item, index (index)}
        <div class="xl-rate-item star{item}"
            style="cursor: {disabled ? 'auto' : 'pointer'}"
            title={getToolTip(index)}
            on:mousemove={(event) => handleMouseEnter(item, event)} 
            on:mouseleave={(event) => handleMouseLeave(item, event)}
            on:click={handleClick} >
            <div class="xl-rate-full">
                <i class="iconfont {icon}"
                    style="color: {item <= score ? strokeColor : backgroundColor}"></i>
            </div>
            
            {#if allowHalf && item - 0.5 <= score && item > score}

            <div class="xl-rate-half">
                <i class="iconfont {icon}" style="color: {strokeColor}"></i>
            </div>

            {/if}

        </div>
    {/each}
</div>

<style>
    .iconfont {
        font-size: 32px;
    }

    .xl-rate-item {
        display: inline-block;
        position: relative;
    }
    .xl-rate-iconfont-main {
        position: relative;
        font-size: 24px;
        margin-right: 8px;
        vertical-align: baseline;
    }
    .xl-rate-half {
        position: absolute;
        left: 0;
        top: 0;
        width: 50%;
        height: 100%;
        overflow: hidden;
    }
</style>
