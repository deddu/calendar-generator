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
        display: grid;
        grid-template-columns:
            repeat(var(--days-width), 2.5in);
        align-items: stretch;
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
    
    .first_of_month .mm  {
        font-weight:bold;
        display: inherit;
    }

    .first_of_year .yy {
        display: inherit;
    }

    .day.padding {
        border:none;
    }

</style>
<div> Monthview
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