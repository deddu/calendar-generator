<!-- let dates = Array.from('x'.repeat(365)).map(x=>new Date()); -->
<script>
    import dayjs from 'dayjs';
    import weekday from 'dayjs/plugin/weekday';
    import dayOfYear from 'dayjs/plugin/dayOfYear';
    import Weekview from './Weekview.svelte';
    import Monthview from './Monthview.svelte';

    dayjs.extend(weekday);
    dayjs.extend(dayOfYear);

    export let start='2021-01-01', end='2022-01-01', caltype='weekly';

    let  s = dayjs(start);
    let e =  dayjs(end);
    // let days, daysCount,weeksCount,monthsCount,paddeddays;
    
    $:  s = dayjs(start);
    $: e =  dayjs(end);
        //start laying out days with a sunday/monday based on locale.
    $: pad = s.weekday();
    $: daysCount =  e.diff(s,'day');
    $: weeksCount = e.diff(s,'week');
    $: monthsCount = e.diff(s,'month');
    $: paddeddays = daysCount>0 ? 'x'.repeat(daysCount+pad).split('').map((x,i)=>s.subtract(pad,'days').add(i,'days')):[];
    $: days = daysCount>0? 'x'.repeat(daysCount).split('').map((x,i)=>s.add(i,'days')):[];
    
    
    const dow = {0:'sun',1:'mon',2:'tue',3:'wed',4:'thu',5:'fri',6:'sat'}
    const getDow = x => dow[x.day()];
    
</script>
<style>
	.main {
        font-family: 'Merriweather', serif;
        font-size: .25in;
	}
    
</style>
<div class='main'>
    between {start} and {end}, there are {daysCount} days. that is {weeksCount} weeks, or {monthsCount} months
    split {caltype}
    {#if caltype=='weekly'}
    <Weekview days={paddeddays}></Weekview>
    {/if}
    {#if caltype=='monthly'}
    <Monthview days={days}></Monthview>
    {/if}
</div>