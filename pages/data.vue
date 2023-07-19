
<template>
    <div v-if="pending">
        <h1>loading ! </h1>
    </div>
    <div v-else-if="error || !data">
        <h1>error </h1>
    </div>
    <div v-else>
      <li v-for="items in data">
        <div class="table-container" role="table">
                    <div class="flex-table header" role="rowgroup">
                        <div class="flex-row first" role="columnheader">1h / 1d / 1w</div>
                        <div class="flex-row" role="columnheader">Name</div>
                        <div class="flex-row" role="columnheader">price € </div>
                        <div class="flex-row" role="columnheader">Price BTC </div>

                    </div>
            <div v-for="coins, index in items" class="flex-table row">
                        <div class="flex-row first" role="cell"><span class="flag-icon flag-icon-gb"></span>
                            <img :src="coins.icon"
                            height="50"
                            /><br>
                            {{ coins.priceChange1h }}/ {{ coins.priceChange1d }} / {{ coins.priceChange1w }}
                        </div>
                        <div class="flex-row" role="cell">{{ coins.symbol }} / {{ coins.name }} </div>
                        <div class="flex-row" role="cell"> {{ coins.price }}</div>
                        <div class="flex-row" role="cell"> {{ coins.priceBtc }}</div>
                </div>
        </div>
      </li>
    </div>


</template>

<script setup>
//const { data, error, pending} = await useFetch('https://api.coinstats.app/public/v1/charts?period=1m&coinId=ethereum')

const { data, error, pending } = await useFetch('https://api.coinstats.app/public/v1/coins?skip=0&limit=40&currency=EUR')

//https://api.coinstats.app/public/v1/news?skip=0&limit=10
//api.coincap.io/v2/assets/bitcoin

</script>

<style lang="scss">
$table-header: #1976D2;
$table-header-border: #1565C0;
$table-border: #d9d9d9;
$row-bg: #f4f2f1;

div {
  box-sizing: border-box;
}

.table-container {
  display: block;
  margin: 2em auto;
  width: 90%;
  max-width: 900px;
}

.flag-icon {
  margin-right: 0.1em;
}
.li {text-decoration: none;}

.flex-table {
  display: flex;
  flex-flow: row wrap;
  border-left: solid 1px $table-border;
  transition: 0.5s;
  &:first-of-type {
    border-top: solid 1px $table-header-border;
    border-left: solid 1px $table-header-border;
  }
  &:first-of-type .flex-row {
    background: $table-header;
    color: white;
    border-color: $table-header-border;
  }
  &.row:nth-child(odd) .flex-row {
    background: $row-bg;
  }
  &:hover {
    background: #F5F5F5;
    transition: 500ms;
  }
}

.flex-row {
  width: calc(100% / 4);
  text-align: center;
  padding: 0.5em 0.5em;
  border-right: solid 1px $table-border;
  border-bottom: solid 1px $table-border;
}

.rowspan {
  display: flex;
  flex-flow: row wrap;
  align-items: flex-start;
  justify-content: center;
}

.column {
  display: flex;
  flex-flow: column wrap;
  width: 75%;
  padding: 0;
  .flex-row {
    display: flex;
    flex-flow: row wrap;
    width: 100%;
    padding: 0;
    border: 0;
    border-bottom: solid 1px $table-border;
    &:hover {
      background: #F5F5F5;
      transition: 500ms;
    }
  }
}

.flex-cell {
  width: calc(100% / 3); //1px = border right
  text-align: center;
  padding: 0.5em 0.5em;
  border-right: solid 1px $table-border;
  //flex: 1 1 33.3%;
  &:last-child {
    // border-right: 0;
  }
}

@media all and (max-width: 767px) {
  .flex-row {
    width: calc(100% / 3); //1px = border right

   &.first {
     width: 100%;
   }
  }

  .column {
    width: 100%;
  }
}

@media all and (max-width: 430px) {

  .flex-table {
    .flex-row {
      border-bottom: 0;
    }
    .flex-row:last-of-type {
      border-bottom: solid 1px $table-border;
    }
  }

  .header {
    .flex-row {
      border-bottom: solid 1px;
    }
  }

  .flex-row {
    width: 100%; //1px = border right

   &.first {
     width: 100%;
     border-bottom: solid 1px $table-border;
   }
  }

  .column {
    width: 100%;
    .flex-row {
      border-bottom: solid 1px $table-border;
    }
  }

  .flex-cell {
    width: 100%; //1px = border right
  }
}
</style>
