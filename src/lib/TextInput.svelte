<script>
    let name = "world";
    let min = 0;
    let max = 100;
    let type = "range";
    let number1 = 0; 
    let number2 = 0; 

    $:sum = number1 + number2;
</script>

<input bind:value={number1} />
<h1>Hello {name.slice(0,1).toLocaleUpperCase()+name.slice(1).toLowerCase()} !</h1>


<input type=range {min} {max} bind:value={number1}>
<input type=range {min} {max} bind:value={number2}>
<p>{sum}</p>