<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
      body{
        background-color: black;
      }
.heart {
  background-color: red;
  display: inline-block;
  height: 50px;
  margin: 0 10px;
  position: relative;
  top: 0;
  transform: rotate(-45deg);
  position: absolute; 
  left: 45%; top: 45%;
  width: 50px;
}
 
.heart:before,
.heart:after {
  content: "";
  background-color: red;
  border-radius: 50%;
  height: 50px;
  position: absolute;
  width: 50px;
}
 
.heart:before {
  top: -25px;
  left: 0;
}
 
.heart:after {
  left: 25px;
  top: 0;
}
@keyframes heartbeat {
  0% {
    transform: scale( 1 );    
  }
  20% {
    transform: scale( 1.25 ) 
      translateX(5%) 
      translateY(5%);
  } 
  40% {
    transform: scale( 1.5 ) 
      translateX(9%) 
      translateY(10%);
  }
}
.heart {
  animation: heartbeat 1s infinite; // our heart has infinite heartbeat :)
  ...
}
    </style>
    <style>

      marquee{
       font-family:tahoma;
       width: 100%;
       padding: 10px 0;
       background-color: #e70606;
       color: #fff;
      font-size: larger;
      }
      
      </style>
</head>
<body>
    <div class="heart"></div>
    <marquee>i love you my love </marquee>
    
</body>
</html>
