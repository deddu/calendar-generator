<!-- let dates = Array.from('x'.repeat(365)).map(x=>new Date()); -->
<script>
    export let days = [];
    let w=31;
    const dow = {0:'sun',1:'mon',2:'tue',3:'wed',4:'thu',5:'fri',6:'sat'}
    const getDow = x => dow[x.day()];
    // const shouldMonthPadding = day => day.daysInMonth() - day.date();
    const isLastOfMonth = day => day.daysInMonth() - day.date()  == 0;
    const getMonthPadding = day => w - day.date();
</script>
<style>
	div .cal {
		/* this will only affect <p> elements in this component */
		color: burlywood;
        display: grid;
        grid-template-columns:
            repeat(var(--days-width), minmax(10px, 1fr));
            /* column-gap: 10px; */
        align-items: stretch;
	}
    div .day {
        border:2px solid;
        border-radius: 5%;
        margin: .4em;
        align-self: stretch;
        height:10em;
        
    }
    .day .mm {display: none;}
    .day .yy {display: none;}
    
    .sun, .sat {
        background-color: gainsboro;
    }
    .first_of_month {
        /* align-self:flex-end; */
        /* grid-area: 4; */
        background-color:blue;
    }
    .first_of_month .mm  {
        font-weight:bold;
        display: inherit;
    }

    .first_of_year .mm {
        color:lawngreen;
    }

    .day.padding {
        border:none;
    }

</style>
<div> weekview
    <div class='cal'  style="--days-width: {w}">
    {#each days as day,i }
		<div id={i} class='day 
         {getDow(day)}
         {day.date()==1?'first_of_month':''}
         {day.dayOfYear()==1?'first_of_year':''}
         {isLastOfMonth(day)?'last_of_month':''}
         '> 
            <div class='mm'>{day.format('MMM')} </div>
            <div class='dd'>{day.format('D')} </div>
            <div class='yy'>{day.format('YYYY')} </div>
        </div>
        <!--pads till month ends-->
        {#if isLastOfMonth(day) }
        {#each Array(getMonthPadding(day)) as _, row}
        <div class='day padding'></div>
        {/each}
  
        {/if}
	{/each}
    </div>
</div>