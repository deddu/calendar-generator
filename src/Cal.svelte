<!-- let dates = Array.from('x'.repeat(365)).map(x=>new Date()); -->
<script>
    import dayjs from 'dayjs';
    import weekday from 'dayjs/plugin/weekday';
    dayjs.extend(weekday);

    export let start='2021-01-01',end='2022-01-01', w=7;
    const s = dayjs(start);
    const e = dayjs(end);
    let daysCount =  e.diff(s,'day');
    let weeksCount = e.diff(s,'week');
    let monthsCount = e.diff(s,'month');

    let days = 'x'.repeat(daysCount).split('').map((x,i)=>s.add(i,'days'));
    const dow = {0:'sun',1:'mon',2:'tue',3:'wed',4:'thu',5:'fri',6:'sat'}
    const getDow = x => dow[x.day()];
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
        margin: .4em;
        align-self: stretch;
        height:10em;
        
    }
    .sun, .sat {
        background-color: gainsboro;
    }
    .first_of_month {
        /* align-self:flex-end; */
        /* grid-area: 4; */
        background-color:blue;
    }
</style>
<div>
    between {start} and {end}, there are {daysCount} days. that is {weeksCount} weeks, or {monthsCount} months
    split by {w}
    <div class='cal'  style="--days-width: {w}">
    {#each days as day,i }
		<div id={i} class='day {getDow(day)} {day.date()==1?'first_of_month':''}'> {day.format('MMM D')} </div>
	{/each}
    </div>
</div>