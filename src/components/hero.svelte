<script>
    export let heroname;
    export let category;
    export let type;
    export let dnlevel;

    let heroimage = heroname + "Hero.png"
    let typeimage = type + ".png"
</script>

<p><img src="/images/type/{typeimage}" alt="{type}" width="25px"/>Bonus {dnlevel}%</p>
<img src="/images/hero/{heroimage}" alt="{heroname}" />
<h3>{category} {heroname} ({type})</h3>