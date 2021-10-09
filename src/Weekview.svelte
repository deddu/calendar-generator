
<script>
    export let days = [];
    let w=7;
    const dow = {0:'sun',1:'mon',2:'tue',3:'wed',4:'thu',5:'fri',6:'sat'}
    const getDow = x => dow[x.day()];
    
</script>
<style>
	div .cal {
        display: grid;
        grid-template-columns:
        repeat(var(--days-width),  2.5in);
	}
    div .day {
        border:2px solid;
        border-radius: 5%;
        margin: .25in;
        align-self: stretch;
        height:2in;
        width: 2in;
        
    }
    .day .mm {display: none;}
    .day .yy {display: none;}

    .sun, .sat {
        background-color: #eee;
    }
    .first_of_month {
        /* align-self:flex-end; */
        /* grid-area: 4; */
        background-color:skyblue;
    }
    .first_of_month .mm  {
        font-weight:bold;
        display: inherit;
    }

    .first_of_year .yy {
        display: inherit;
        font-weight:700;
    }

</style>
<div> weekview
    <div class='cal'  style="--days-width: {w}">
    <div class='hrow'>  Sun </div>
    <div class='hrow'>  Mon </div>
    <div class='hrow'>  Tue </div>
    <div class='hrow'>  Wed </div>
    <div class='hrow'> Thu </div>
    <div class='hrow'>  Fri </div>
    <div class='hrow'>  Sat </div>
    {#each days as day,i }
		<div id={i} class='day {getDow(day)} {day.date()==1?'first_of_month':''} {day.dayOfYear()==1?'first_of_year':''}'> 
            <div class='yy'>{day.format('YYYY')} </div>
            <div class='mm'>{day.format('MMM')} </div>
            <div class='dd'>{day.format('D')} </div>
        </div>
	{/each}
    </div>
</div>