<script>
    let arr = [];
    let timeTaken, d, startTime, endTime, completed = false;
    let screenWidth = window.innerWidth-50;

    function reload() {
        location.reload();
        return false;
    }

        
    async function bubbleSort() {
        d = new Date();
        startTime = d.getTime()/1000;
        
        let len = arr.length;
        for (let i = 0; i < len; i++) {
        for (let j = 0; j < len; j++) {
            if (arr[j] > arr[j+1]) {
            let tmp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = tmp;
            await new Promise((r) => setTimeout(r, 1));
            } 
        }
        }
        d = new Date();
        endTime = d.getTime()/1000;
        timeTaken = endTime - startTime;
        completed = true;
    }

    async function insertionSort() {
        d = new Date();
        startTime = d.getTime()/1000;
        
        for (let i = 1; i < arr.length; i++) {
        // First, choose the element at index 1
        let current = arr[i];
        let j;
        for (j = i - 1; j >= 0 && arr[j] > current; j--) {
            arr[j + 1] = arr[j];
        }
        arr[j + 1] = current;
        await new Promise((r) => setTimeout(r, 1));
        }
        d = new Date();
        endTime = d.getTime()/1000;
        timeTaken = endTime - startTime;
        completed = true;
    }

    async function gnomeSort() {
        d = new Date();
        startTime = d.getTime()/1000;
        
        for (var i = 1; i < arr.length; i++) {
            if (arr[i-1] > arr[i]) {
            for( ; i > 0 && arr[i-1] > arr[i]; i--) {
                var t = arr[i];
                arr[i] = arr[i-1];
                arr[i-1] = t;
                await new Promise((r) => setTimeout(r, 1));
            }
            }
        }
    d = new Date();
    endTime = d.getTime()/1000;
    timeTaken = endTime-startTime;
    completed = true;
    }

    async function selectionSort() {
        d = new Date();
        startTime = d.getTime()/1000;
        
        let n = arr.length;
            
        for(let i = 0; i < n; i++) {
            let min = i;
            for(let j = i+1; j < n; j++){
                if(arr[j] < arr[min]) {
                    min=j; 
                }
            }
            if (min != i) {
                let tmp = arr[i]; 
                arr[i] = arr[min];
                arr[min] = tmp;
                await new Promise((r) => setTimeout(r, 1));
            }
        }
        d = new Date();
        endTime = d.getTime()/1000;
        timeTaken = endTime-startTime;
        completed = true;
    }

    async function radixBucketSort () {
        d = new Date();
        startTime = d.getTime()/1000;
        
        var idx1, idx2, idx3, len1, len2, radix, radixKey;
        var radices = {}, buckets = {}, num, curr;
        var currLen, radixStr, currBucket;

        len1 = arr.length;
        len2 = 10;  // radix sort uses ten buckets

        // find the relevant radices to process for efficiency        
        for (idx1 = 0;idx1 < len1;idx1++) {
        radices[arr[idx1].toString().length] = 0;
        }

        // loop for each radix. For each radix we put all the arr
        // in buckets, and then pull them out of the buckets.
        for (radix in radices) {          
        // put each array item in a bucket based on its radix value
        len1 = arr.length;
        for (idx1 = 0;idx1 < len1;idx1++) {
            curr = arr[idx1];
            // item length is used to find its current radix value
            currLen = curr.toString().length;
            // only put the item in a radix bucket if the item
            // key is as long as the radix
            if (currLen >= radix) {
            // radix starts from beginning of key, so need to
            // adjust to get redix values from start of stringified key
            radixKey = curr.toString()[currLen - radix];
            // create the bucket if it does not already exist
            if (!buckets.hasOwnProperty(radixKey)) {
                buckets[radixKey] = [];
            }
            // put the array value in the bucket
            buckets[radixKey].push(curr);         
            } else {
            if (!buckets.hasOwnProperty('0')) {
                buckets['0'] = [];
            }
            buckets['0'].push(curr);
            }
        }
        // for current radix, arr are in buckets, now put them
        // back in the array based on their buckets
        // this index moves us through the array as we insert arr
        idx1 = 0;
        // go through all the buckets
        for (idx2 = 0;idx2 < len2;idx2++) {
            // only process buckets with arr
            if (buckets[idx2] != null) {
            currBucket = buckets[idx2];
            // insert all bucket arr into array
            len1 = currBucket.length;
            for (idx3 = 0;idx3 < len1;idx3++) {
                arr[idx1++] = currBucket[idx3];
                await new Promise((r) => setTimeout(r, 1));
            }
            }
        }
        buckets = {};
        }
    d = new Date();
        endTime = d.getTime()/1000;
        timeTaken = endTime-startTime;
        completed = true;
    }

    async function flashSort() {
        d = new Date();
        startTime = d.getTime()/1000;
        
        var max = 0, min = arr[0];
        var n = arr.length;
        var m = ~~(0.45 * n);
        var l = new Array(m);
    
        for (var i = 1; i < n; ++i) {
            if (arr[i] < min) {
                min = arr[i];
            }
            if (arr[i] > arr[max]) {
                max = i;
            }
        }
    
        if (min === arr[max]) {
            return arr;
        }
    
        var c1 = (m - 1) / (arr[max] - min);
    
    
        for (var k = 0; k < m; k++) {
            l[k] = 0;
        }
        for (var j = 0; j < n; ++j) {
            k = ~~(c1 * (arr[j] - min));
            ++l[k];
        }
    
        for (var p = 1; p < m; ++p) {
            l[p] = l[p] + l[p - 1];
        }
    
        var hold = arr[max];
        arr[max] = arr[0];
        arr[0] = hold;
    
        //permutation
        var move = 0, t, flash;
        j = 0; 
        k = m - 1;
    
        while (move < (n - 1)) {
            while (j > (l[k] - 1)) {
                ++j;
                k = ~~(c1 * (arr[j] - min));
            }
            if (k < 0) break;
            flash = arr[j];
            while (j !== l[k]) {
                k = ~~(c1 * (flash - min));
                hold = arr[t = --l[k]];
                arr[t] = flash;
                flash = hold;
                ++move;
                await new Promise((r) => setTimeout(r, 0.1));
            }
            completed = true;
        }
    
        //insertion
        for (j = 1; j < n; j++) {
            hold = arr[j];
            i = j - 1;
            while (i >= 0 && arr[i] > hold) {
                arr[i + 1] = arr[i--];
            }
            arr[i + 1] = hold;
        }
        d = new Date();
        endTime = d.getTime()/1000;
        timeTaken = endTime-startTime;
        completed = true;
    }   

    function shuffle() {
        completed = false;
        arr = [];
        for (let i = 1; i < screenWidth; i++) {
            let num = i/10;
            arr.push(num);
        }

        console.log(arr, Math.max(...arr), screenWidth/100)
        let currentIndex = arr.length,  randomIndex;
        while (currentIndex != 0) {
            randomIndex = Math.floor(Math.random() * currentIndex);
            currentIndex--;
            [arr[currentIndex], arr[randomIndex]] = [arr[randomIndex], arr[currentIndex]];
        }

    }
    
    shuffle()
</script>

<main>
    <button id="shuffle" on:click={reload}>Refresh</button>
    <button id="shuffle" on:click={shuffle}>Shuffle</button>
    <button on:click={bubbleSort}>Bubble Sort</button>
    <button on:click={insertionSort}>Insertion Sort</button>
    <button on:click={gnomeSort}>Gnome Sort</button>
    <button on:click={selectionSort}>Selection Sort</button>
    <button on:click={radixBucketSort}>Radix Bucket Sort</button>
    <button on:click={flashSort}>Flash Sort</button>
</main>
<br>

{#each arr as el, i}
    {#if completed}
        <div id={i} style="position: relative;height: {el * 5}px; background: #52D452;" />
    {:else}
        <div id={i} style="position: relative;height: {el * 5}px; background: #eeeeee;" />
    {/if}
{/each}

<input type="number" placeholder="Number of elements" bind:value={screenWidth} on:change={shuffle}>

<h2>It took: {timeTaken} seconds to sort {screenWidth} elements</h2>
        
<style>
    :root {
        background-color: #161616;
        margin: 0;
    }

    @font-face{
    font-family: 'Atkinson';
    src: url(https://fonts.googleapis.com/css2?family=Atkinson+Hyperlegible&display=swap) format('ttf');
    }

    @font-face{
        font-family: 'AtkinsonBold';
        src: url(https://fonts.googleapis.com/css2?family=Atkinson+Hyperlegible:wght@400;700&display=swap) format('ttf');
    }
    
    #word {
        position: absolute;
        color: #161616;
        font-family: AtkinsonBold, sans-serif;
        bottom: 450px;
        left: 35%;
        font-size: 100px;
    }
    
    h2 {
        color: white;
        font-family: Atkinson, sans-serif;
    }
    
    div {
        width: 1px;
        display: inline-block;
        margin: 0px;
    }
    
    main {
        display: flex;
        justify-content: space-between;;
    }
    
    button {
        padding: 0.5em 1em;
        color: #ff3e00;
        background-color: rgba(255, 62, 0, 0.1);
        border-radius: 2em;
        border: 2px solid rgba(255, 62, 0, 0);
        outline: none;
        width: 150px;
        font-family: AtkinsonBold, sans-serif;
        font-size: 20px;
        cursor: pointer;
    }

    #shuffle {
        background-color: #ff6961;
        color: #FFFDD0;
    }

    button:focus {
        border: 2px solid #ff3e00;
    }

    button:hover, button:active {
        background-color: rgba(255, 62, 0, 0.2);
    }
</style>