<script lang="ts">
import * as d3 from 'd3'

let htmlContainer='',
options = '';

const apis = {
    type: {
        path: 'https://api-v3.mbta.com/routes?filter[type]='
    }
}

//const api = 'https://api-v3.mbta.com/stops?filter[route]=Red';
//const api = 'https://api-v3.mbta.com/routes?filter[type]=';
//const containerAttributes=[{name:'class',value:'classes'},{name:'id',value:'ids'}]
// graph showing how frequently a stop is visited by the train on a given day
// option to select a line
// request all lines

//let htmlContainer='';

// async function renderRedLineStops(){
//     await fetch(api).then(res=>{
//         return res.json();
//     }).then(data=>{
//         data.data.map(item=>{
//             return htmlContainer+=`<li>${item.attributes.name}</li>`;
//         });
//     });
// }

//renderRedLineStops();

//let options = '';

let railType;

function test(){
    return getRoutes(this.value);
}

class MbtaForms {
    constructor(){
        this.heading = '';
    }
}



async function getRoutes(){
    console.log('test');
    await fetch(apis.type.path + this.value)
    .then(res=>{
        return res.json();
    })
    .then(data=>{
        options='';
        data.data.forEach(item=>{
            let option = document.createElement('option');
            option.innerHTML=item.attributes.long_name;
            options+=option.outerHTML;
        });
    });
}



getRoutes();

//setRouteMenu(options);

</script>

<form>
    <legend><h1>Build Graph</h1></legend>
    <fieldset>
        <select name="railType" id="railType" on:change="{getRoutes}">
            <option value="0" selected>Light Rail</option>
            <option value="1">Heavy Rail</option>
            <option value="2">Commuter Rail</option>
            <option value="3">Bus</option>
            <option value="4">Ferry</option>
        </select>
    </fieldset>
    <fieldset>
        <select id="test">
            {@html options}
        </select>
    </fieldset>
</form>
<div id="graph">
</div>
<div>{@html htmlContainer}</div>

<style>
:global(li) {
list-style-type: none;
}
</style>