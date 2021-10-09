<!-- let dates = Array.from('x'.repeat(365)).map(x=>new Date()); -->
<script>
    export let days = [];
    let w=7;
    const dow = {0:'sun',1:'mon',2:'tue',3:'wed',4:'thu',5:'fri',6:'sat'}
    const getDow = x => dow[x.day()];
    
</script>
<style>
	div .cal {
		/* this will only affect <p> elements in this component */
		color: burlywood;
        display: grid;
        grid-template-columns:
        repeat(var(--days-width),  2.5in);
        /* column-gap: 10px; */
        /* align-items: stretch; */
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
        background-color: gainsboro;
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
        color:lawngreen;
        font-weight:bold;
    }

</style>
<div> weekview
    <div class='cal'  style="--days-width: {w}">
    {#each days as day,i }
		<div id={i} class='day {getDow(day)} {day.date()==1?'first_of_month':''} {day.dayOfYear()==1?'first_of_year':''}'> 
            <div class='yy'>{day.format('YYYY')} </div>
            <div class='mm'>{day.format('MMM')} </div>
            <div class='dd'>{day.format('D')} </div>
        </div>
	{/each}
    </div>
</div>