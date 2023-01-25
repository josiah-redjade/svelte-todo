<script lang='ts'>
    type TodoItem = {
        description: string;
        id: string;
        completed: boolean;
    }
    let myArray : TodoItem[] = [
        {
            description: 'Doing the dishes',
            id: crypto.randomUUID(),
            completed: false
        }
    ]

    let description = '';

    const addItem = (e: Event) => {
        e.preventDefault();
        if (!description)
            return;
        myArray = [...myArray, {description, id: crypto.randomUUID(), completed: false }];
        description = '';
    }

    const removeItem = (item: TodoItem) => {
        console.log(item)
        myArray = myArray.filter(arrItem => arrItem.id !== item.id)
    }
</script>

<ul>
    {#each myArray as item, i}
        <li
             on:click={()=>removeItem(item)}
             class:blue={i == 0}
             class:red={i == 1}
             class:green={i == 2}
        >
            {item.description}
        </li>
    {/each}
</ul>

<form on:submit={addItem}>
    <input bind:value={description} type='text'/>
    <br>
    <button type='submit'>Add Item</button>
</form>

<style lang='sass'>
    ul
        text-align: left
        li
            opacity: 1
            transition: 0.2s
            cursor: pointer
            &:hover
                opacity: 0.8
                text-decoration: underline
    button
        margin: 1rem auto

    .red
        color: red
    .green
        color: blue
    .blue
        color: green
    .myclassname
        background: pink
    
</style>
