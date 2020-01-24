var mysql = require('mysql');
const express = require('express')
const app = express();

app.get('/app1', (req, res) => {

  var con = mysql.createConnection({
    host: "35.193.118.123",
    door: "3306",
    database: "ops_challenge",
    user: "challenge",
    password: "#Ch4L13ngE@Pwd#",
  });
  


  con.connect(function(err) {
    if (err) throw err;
    

    con.query("select count(*)  as cont, stage_to, weekofyear(update_date) as sem_ano from deals_updates where year(update_date) = 2017 group by stage_to , weekofyear(update_date)" , function (err,result,fields){
      if (err) throw err;

      var html = "<html><button onclick='location.reload()'>Refrescar a Página</button><form><input type=number id='myInput' onkeyup='myFunction()' placeholder='Busca por semana..'><input type='submit' value='Buscar'></form><table id = 'myTable' border=1><tr><td>Estagio</td><td>Semana</td><td>Negócios</td><tr>"
      for (i = 0; i < result.length; i++) {
          html = html + "<tr><td> " + result[i].stage_to  + "</td><td>" +
                                      result[i].sem_ano + "</td><td>" +  
                                      result[i].cont + "</td></tr>"
         
      }
      html = html + "</table><script>"
      function myFunction() {
        var input, filter, table, tr, td, i, numberValue;
        input = document.getElementById('Semana');
        filter = input.value.toUpperCase();
        table = document.getElementById('myTable');
        tr = table.getElementsByTagNumber('tr');
        for (i = 0; i < tr.length; i++) {
          td = tr[i].getElementsByTagNumber('td')[0];
          if (td) {
            numberValue = td.numberContent || td.innerNumber;
            if (numberValue.toUpperCase().indexOf(filter) > -1) {
              tr[i].style.display = '';
            } else {
              tr[i].style.display = 'none';
            }
          }       
        }
      }
      "</script></html>"
     
      res.send(html);
     
    });
  });

  //res.send('Hello World!')
});

app.get('/app2', (req, res) => {

  var con = mysql.createConnection({
    host: "35.193.118.123",
    door: "3306",
    database: "ops_challenge",
    user: "challenge",
    password: "#Ch4L13ngE@Pwd#",
  });
  


  con.connect(function(err) {
    if (err) throw err;
    

    con.query("select count(*)  as cont, weekofyear(add_date) as sem_ano from deals where year(add_date) = 2017 group by  weekofyear(add_date)" , function (err,result,fields){
      if (err) throw err;

      var html = "<html><button onclick='location.reload()'>Refrescar a Página</button><form><input type=number id='myInput' onkeyup='myFunction()' placeholder='Busca por semana..'><input type='submit' value='Buscar'></form><table border=1><tr><td>Semana</td><td>Negócios</td><tr>"
      for (i = 0; i < result.length; i++) {
          html = html + "<tr><td> " + 
                                      result[i].sem_ano + "</td><td>" +  
                                      result[i].cont + "</td></tr>"
        
      }
      html = html + "</table><script>"
      function myFunction() {
        var input, filter, table, tr, td, i, numberValue;
        input = document.getElementById('Semana');
        filter = input.value.toUpperCase();
        table = document.getElementById('myTable');
        tr = table.getElementsByTagNumber('tr');
        for (i = 0; i < tr.length; i++) {
          td = tr[i].getElementsByTagNumber('td')[0];
          if (td) {
            numberValue = td.numberContent || td.innerNumber;
            if (numberValue.toUpperCase().indexOf(filter) > -1) {
              tr[i].style.display = '';
            } else {
              tr[i].style.display = 'none';
            }
          }       
        }
      }
      "</script></html>"
     
      res.send(html);
     
    });
  });

});

app.listen(3010, () => {
  console.log('Example app listening on port 3306!')
});
