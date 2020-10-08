<template>
  <div id="agenda" class="area" v-if="agendaBody">
    <div class="wrapper">
      <div class="title">
        <h2><span>議</span>程</h2>
      </div>
      <div class="agenda-table content">
        <table>
          <thead>
              <tr>
                <th>時間</th>
                <th>流程</th>
                <th>講者</th>
              </tr>
          </thead>
          <tbody class="afternoon" v-html="agendaBody" />
        </table>
        <ul>
          <li>※最新議程資訊，敬請鎖定本活動官網</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: function() {
    return {
      agendaBody: null
    }
  },
  mounted() {
    const timestr = new Date().getTime();
    axios.get(`agenda-body.html?${timestr}`).then(response => {
      this.agendaBody = response.data;
    }).catch(error => {
      console.log(error);
    });
  }
}
</script>

<style>
.agenda-table {
  position: relative;
  background: white;
  padding: 1em;
  color: #505050;
}
.agenda-table.content {
  max-width: 1280px;
}
.agenda-table table {
  width: 100%;
  border-collapse: collapse;
}
.agenda-table th {
  padding: 0.6em 0.8em;
}
.agenda-table td {
  padding: 0.8em;
}
.agenda-table td[colspan="2"] {
  text-align: center;
}
.agenda-table td span {
  display: inline-block;
  background: #f09819;
  color: white;
  padding: 0.2em 0.8em;
}
.agenda-table .controller tr:last-child td {
  color: white;
  text-align: center;
  padding: 1.5em 1em;
  border-top: solid 1px #ccc;
  border-bottom: solid 1px #ccc;
}
.agenda-table ol {
  display: inline-block;
  margin-top: 0;
  text-align: left;
  padding-left: 1em;
}
.agenda-table ol li {
  list-style: decimal;
  letter-spacing: inherit;
}
.controller td label {
  display: inline-block;
  min-width: 30%;
  margin: 0 2.5%;
  cursor: pointer;
  padding: 0.4em 0.6em;
  border-radius: 10px;
  background: #b4b4b4;
  transition: .5s;
}
.controller td label.active {
  background: #f09819;
}
.controller td label input {
  display: none;
}
.agenda-table thead th {
  color: white;
  font-weight: 400;
  letter-spacing: 0.2em;
  background: #f09819;
  border-right: solid 2px white;
}
.agenda-table thead th:last-child {
  border-right: none;
}
.agenda-table tbody td:first-child {
  width: 1px;
  white-space: nowrap;
}
.agenda-table > ul {
  margin: 2em 0;
}
.agenda-table tbody th {
  color: white;
  border: none;
  background: rgba(240, 152, 25, .65);
}

@media (hover: hover) {
}

@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {
}

@media screen and (max-width: 640px) {
  .agenda-table {
    padding: 0.5em;
  }
}

@media screen and (min-width: 481px) {
  .agenda-table thead th:nth-child(2) {
    width: 45%;
  }
  .agenda-table td,
  .agenda-table th {
    border-bottom: solid 1px #ccc;
  }
  .agenda-table tr:last-child td,
  .agenda-table tr:last-child th {
    border-bottom: none;
  }
  .agenda-table td span {
    font-size: .9em;
  }
}

@media screen and (max-width: 480px) {
  #agenda .content {
    padding: 0;
  }
  .agenda-table {
    padding: 0;
  }
  #agenda .area-box::before {
    display: none;
  }
  .agenda-table table,
  .agenda-table tbody,
  .agenda-table tr,
  .agenda-table td,
  .agenda-table th {
    display: block;
    text-align: center;
  }
  .agenda-table thead {
    display: none;
  }
  .agenda-table tr {
    margin: 0.8em 0;
    border: solid 1px #ccc;
  }
  .agenda-table tbody td:first-child {
    width: 100%;
    background-color: #f09819;
    color: white;
    padding: 0.6em 0.8em;
  }
  .agenda-table tbody td:first-child:before {
    content: '時間: ';
  }
  .agenda-table .controller tr {
    border: none;
  }
  .agenda-table .controller tr:last-child td {
    background: none;
    border: none;
    padding-left: 0;
    padding-right: 0;
  }
  .controller td:before {
    display: none;
  }
  .controller td label {
    width: 45%;
    font-size: 0;
  }
  .controller td label::before {
    content: attr(data-title);
    font-size: 1rem;
    display: block;
    padding: 1em 0.6em;
  }
  .agenda-table tbody td[colspan="3"]:first-child:before {
    display: none;
  }
}

</style>
