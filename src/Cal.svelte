<!-- let dates = Array.from('x'.repeat(365)).map(x=>new Date()); -->
<script>
    import dayjs from 'dayjs';
    import weekday from 'dayjs/plugin/weekday';
    import dayOfYear from 'dayjs/plugin/dayOfYear';
    import Weekview from './Weekview.svelte';
    import Monthview from './Monthview.svelte';

    dayjs.extend(weekday);
    dayjs.extend(dayOfYear);

    export let start='2021-01-01',end='2022-01-01', caltype='weekly';

    let  s = dayjs(start);
    let e =  dayjs(end);
    $: s = dayjs(start);
    $: e =  dayjs(end);
    //start laying out days with a sunday/monday based on locale.
    let pad = s.weekday();
    let daysCount =  e.diff(s,'day');
    let weeksCount = e.diff(s,'week');
    let monthsCount = e.diff(s,'month');

    let paddeddays = 'x'.repeat(daysCount+pad).split('').map((x,i)=>s.subtract(pad,'days').add(i,'days'));
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
        border-radius: 5%;
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
    split by {caltype}
    {#if caltype=='weekly'}
    <Weekview days={paddeddays}></Weekview>
    {/if}
    {#if caltype=='monthly'}
    <Monthview days={days}></Monthview>
    {/if}
</div>