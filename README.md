<p></p>

<h2 align="center">ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ПРОФЕССИОНАЛЬНОГО ОБРАЗОВАНИЯ <br> «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ» <br> КАФЕДРА ИНФОРМАТИКИ </h2>
<p align="center">Лабораторная работа №7 <br>
по курсу «Web-технологии, языки и средства создания web-приложений» 

<p align="center"><b>"Разработка серверных скриптов"</b><p>
<p align="right"><b>Выполнила: </b> студентка 331 группы Витковская Полина</p>
<p  align="right"><b>Принял: </b> Соболев Е. И., старший преподователь</p>
<br>
<br>
<br>
<p align="center">Южно-Сахалинск <br> СахГУ <br> 2024</p>
<h2> Введение </h2>
<p>Лабораторные работы по дисциплине «Web-технологии, языки и средства создания web-приложений» предназначены для освоения полученных теоретических знаний на практике. Перед началом лабораторной работы были поставлены цели: <br>
<ol>
  <li>Используя PHP, решить задачи.
  <li>Сделать qrcode, parser и отправку электронной почты</li>
</ol>
В соответствии с данными целями необходимо решить следующие задачи:
<ol>
   <li> Написать скрипты для решения данных задач.
   </ol>
Для реализации данной работы будет использоваться Visual Studio Code. Выполнение кода будет происходить в браузере Google Chrome с использованием node.js.
</p>
<h2>Решение задач</h2>

<p>Код на php:</p>
<p>https://www.w3schools.com/php/phptryit.asp?filename=tryphp_compiler</p>

```javascript
<!DOCTYPE html>
<html>
<body>

<?php

// 1.
echo '1 задание.<br><br>';
$var = 'hello';
echo $var[0] . $var[1] . $var[strlen($var) - 1];

// 2.
echo '<br><br><br> 2 задание.<br><br>';
echo 'Количество секунд в часе = '+(60 * 60);

// 3.
echo '<br><br><br> 3 задание.<br><br>';
$var = 1;
$var += 12;
$var -= 14;
$var *= 5;
$var /= 7;
$var += 1;
$var -= 1;
echo $var;

// 4.
echo '<br><br><br> 4 задание.<br><br>';
$a = 3;
echo $a;

// 5.
echo '<br><br><br> 5 задание.<br><br>';
$a = 10;
$b = 2;
echo $a + $b;
echo '<br>';
echo $a - $b;
echo '<br>';
echo $a * $b;
echo '<br>';
echo $a / $b;
echo '<br>';

// 6.
echo '<br><br><br> 6 задание.<br><br>';
$c = 15;
$d = 2;
$result = $c + $d;
echo $result;

// 7.
echo '<br><br><br> 7 задание.<br><br>';
$a = 10;
$b = 2;
$c = 5;
echo $a + $b + $c;

// 8.
echo '<br><br><br> 8 задание.<br><br>';
$a = 17;
$b = 10;
$c = $a - $b;
$d = 7;
echo $result = $c + $d;

// 9.
echo '<br><br><br> 9 задание.<br><br>';
echo $text = 'Привет, Мир!';

// 10.
echo '<br><br><br> 10 задание.<br><br>';
echo $text1 = 'Привет, ' . $text2 = 'Мир!';

// 11.
echo '<br><br><br> 11 задание.<br><br>';
$name = 'Сатору';
echo "Привет, $name!";

// 12.
echo '<br><br><br> 12 задание.<br><br>';
$age = 20;
echo "Мне $age лет!";

// 13.
echo '<br><br><br> 13 задание.<br><br>';
$text = 'abcde';
echo $text[0] . $text[1] . $text[-1];

// 14.
echo '<br><br><br> 14 задание.<br><br>';
$text[0] = '!';
echo $text;

// 15.
echo '<br><br><br> 15 задание.<br><br>';
$num = '12345';
echo array_sum(str_split($num));

// 16.
echo '<br><br><br> 16 задание.<br><br>';
echo 'Количество секунд в часе: ' . 60 * 60 . '<br>';
echo 'Количество секунд в сутках: ' . 60 * 60 * 24 . '<br>';
echo 'Количество секунд в месяце: ' . 60 * 60 * 24 * 30 . '<br>';

// 17.
echo '<br><br><br> 17 задание.<br><br>';
$hour = 11;
$min = 15;
$sec = 42;
echo "$hour:$min:$sec";

// 18.
echo '<br><br><br> 18 задание.<br><br>';
$num = 5;
echo $num * $num;

// 19.
echo '<br><br><br> 19 задание.<br><br>';
$var = 47;
$var += 7;
$var -= 18;
$var *= 10;
$var /= 20;
echo $var;

// 20.
echo '<br><br><br> 20 задание.<br><br>';
$text = 'Я';
$text .= ' хочу';
$text .= ' знать';
$text .= ' PHP!';
echo $text;

// 21.
echo '<br><br><br> 21 задание.<br><br>';
$var = 10;
$var++;
$var++;
$var--;
echo $var;

// 22.
echo '<br><br><br> 22 задание.<br><br>';
$var = 10;
$var += 7;
$var++;
$var--;
$var += 12;
$var *= 7;
$var -= 15;
echo $var;
?>

</body>
</html>

```
<p>app.js</p>

```JavaScript
const express = require('express');
const app = express();
const nodemailer = require('nodemailer');
const QRCode = require('qrcode');
const axios = require('axios');
const fs = require('fs');

app.use(express.static(__dirname + "/public"));

app.get('/', function(req, resp){
    response.sendFile("public/index.html");
});

app.get("/qrcode", async function(req, resp){
    const url = req.query.url;
  
    if (!url) {
      return resp.status(400).send('URL не указан.');
    }
  
    try {
      const qr = await QRCode.toDataURL(url);
      resp.send(`<img src="${qr}" />`);
    } catch (err) {
      resp.status(500).send('Ошибка при создании QR-кода.');
    }
});

app.get("/sendmessage", function(req, resp){
    const email = req.query.email;
    //console.log(email);
    let transporter = nodemailer.createTransport({
        host: '',
    port:'',
    secure: false,
    auth: {
        user:"user",
        pass: "pass",
    },
    }); 

    var mailOptions = {
        from: 'me',
        to: 'you',
        subject: 'Hello from bot',
        text: 'Hello from bot'
    };

    transporter.sendMail(mailOptions);
    resp.send(email);
});

app.get("/parse", async function(req, resp){
    const url = req.query.url;
    
    const response = await axios.get(url); 
    const res = response.data.match(/<span class=\"text-bold color-fg-default\">(.*)<\/span>/g);
    const str = "<span class=\"p-nickname vcard-username d-block\" itemprop=\"additionalName\">";
    let name = "";
    let i = response.data.indexOf(str) + str.length + 1;
    while(response.data[i] != '<'){
        name += response.data[i];
        i++;
    }
    name = name.trim();
    const followers = res[0].substring(res[0].indexOf(">") + 1, res[0].lastIndexOf("<"));
    const following = res[1].substring(res[1].indexOf(">") + 1, res[1].lastIndexOf("<"));
    
    const result = {
        name: name,
        followers: followers,
        following: following,
    };
    resp.send(result);

    if(!fs.existsSync("db.txt")){
        fs.open('db.txt', 'w', (err) => {
            if(err) throw err;
            console.log('File db.txt created');
        }); 
    }
    fs.appendFileSync('db.txt', `name: ${result.name} --followers: ${result.followers} --following: ${result.following}\n`, (err)=>{
        if(err) throw err;
        console.log("Record appended");
    });
});

app.listen(3002, function(req, resp){
    console.log("Server online.")

});
```
<p>index.html</p>

```JavaScript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>lab7</title>
</head>
<body>
    <p><a href="qrcode?url=https://www.youtube.com/@LanaDelRey"><button> QR-Code</button></a></p>
    <p><a href="sendmessage?email=exxxample@exmaple.com"><button> Отправить email</button></a></p>
    <p><a href="parse?url=https://github.com/linariell"><button> Спарсить </button></a></p>
</body>
</html>
```
<p>CodeWars:</p>

```javascript
function breakChocolate(n,m) {
  
  return (n * m === 0) ? 0 : n * m - 1;
}
function digPow(n, p){
  let sum = 0;
  for(let i = 0, j = p; i < n.toString().length; i++, j++){
    sum += Math.pow(parseInt(n.toString()[i]), j);
  }
  
  return sum % n == 0 ? sum / n : -1;

}
function reject(array, predicate) {
  let result = [];
  for(let i in array){
    if(!predicate(array[i])) result.push(array[i]);
  }
  return result;
}
function evaporator(content, evap_per_day, threshold){ 
  let days = 0;
  threshold = threshold * 0.01 * content
  
  while(content >= threshold){
    content *= ((100 - evap_per_day) * 0.01);
    days++;
  }
  return days;
}
var fibsFizzBuzz = function(n) {
    let array = [];
    for(let i = 0; i < n; i++){
      if (i == 0 || i == 1) {
        array.push(1);
      }
      else {
        array.push(array[i - 2] + array[i - 1]);
      }
    }
    for(let i = 0; i < n; i++)
    {
        if(array[i] % 3 == 0 & array[i] % 5 == 0) array[i] = 'FizzBuzz';
        if(array[i] % 3 == 0) array[i] = 'Fizz';
        if(array[i] % 5 == 0) array[i] = 'Buzz';
    }
    return array;
  }
function product(values) {
  let mp = 1;
  for(let i in values){
    mp *= values[i];
  }
  return values == null || values.length == 0 ? null : mp;
}
function alphabetPosition(text) {
  let result = "";
  for (let i = 0; i < text.length; i++){
    let code = text.toUpperCase().charCodeAt(i)
    if (code > 64 && code < 91) result += (code - 64) + " ";
  }

  return result.slice(0, result.length-1);
}
function findEvenIndex(arr)
{
  for(let i = 0; i < arr.length; i++){
    let sum1 = 0;
    for(let j = 0; j < i; j++){
      sum1 += arr[j];
    }
    
    let sum2 = 0;
    for(let j = i + 1; j < arr.length; j++){
      sum2 += arr[j];
    }
    
    if(sum1 == sum2) return i;
  }
  
  return -1;
}
function findAverage(array) {
  let avarage = 0;
  for(let i in array)
    avarage += array[i];
  return array.length == 0 ? 0 : avarage / array.length;
}
function scrollingText(text){
  text = text.toUpperCase();
  let array = [text];
  for(let i = 0; i < text.length - 1; i++){
    let texttemp = text.split("");
    texttemp.push(texttemp.shift());
    text = texttemp.join("");
    array.push(text);
  }
  return array;
}
function bump(str){
  let sum = 0;
  let array = str.split("");
  for(let i in array){
    if(array[i] == "n") sum++;
    if(sum > 15) return "Car Dead";
  }
  return "Woohoo!";
}
function countDevelopers(list) {
  let count = 0;
  for(let i in list)
    if(list[i].continent === 'Europe' && list[i].language === 'JavaScript') count++;
  return count;
}
function removeDuplicateWords (s) {
  let array = s.split(" ");
  let result = [];
  for(let i in array){
    if(result.indexOf(array[i]) == -1)
      result.push(array[i]);
  }
  return result.join(" ");
}
```
<h2>Вывод</h2>
<p>В ходе лабораторной работы были решены задачи на PHP, решены задачи с Codewars.</p>
