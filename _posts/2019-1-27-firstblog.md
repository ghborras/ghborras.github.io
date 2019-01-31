---
layout: post
title: Cryptocurrency list with Vue+Axios
---

*{{ page.date | date: "%B %e, %Y" }}*


Js

```js
 new Vue({
    el: '#app',
    data () {
      return {
        info2: null,
        interval: '', 
      }
    },

    mounted () {

        this.refreshCoins();
    },

    methods: {
  
        refreshCoins: function() { 
            this.interval = setTimeout(()=>{
                axios.get('https://api.coinmarketcap.com/v2/ticker/').then(response => {
                this.info2 = response.data;
                this.getBeneficio();
                this.getSaldo();
                });   
            },1000);
        },  
    },

    filters: {

        formatNumber (value) {
            return parseFloat(Math.round(value * 100) / 100).toFixed(2);
        }
      },
  })
```

HTML

```html
    <div id="app">

        .......
         {% raw %}
        <table>
            <tr v-for="currency in info2.data">  
                <td>{{ currency.name }}</td>
                <td>{{ currency.symbol }}</td>
                <td>{{ currency.rank }}</td>
                <td>{{ currency.quotes.USD.percent_change_1h | formatNumber }}</td>
                <td>{{ currency.quotes.USD.percent_change_24h | formatNumber }}</td>
                <td>{{ currency.quotes.USD.percent_change_7d | formatNumber }}</td>
                <td>{{ currency.quotes.USD.price | formatNumber }}</td>
            </tr>
        </table>
        {% endraw %}
        .......

    </div>
```

[close]({{ site.baseurl }}/)
