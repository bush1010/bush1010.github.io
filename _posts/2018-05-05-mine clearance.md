---
layout: post
title: "原生JS~经典扫雷"
description: 分享
tags: 源码
---

***

![alt text](/pic/mine clearance/mine clearance.png)

***



***

![alt text](/pic/mine clearance/mine clearance1.png)

***


  css部分
  通配符 {
            margin: 0;
            padding: 0;
        }
        .wrapper {
            width: 100%;
            height: 700px;
            background: bisque;
            background-size: 100% 100%;
            opacity: 0.8;
        }
        .startGame {
            position: absolute;
            left: 160px;
            top: 50%;
            margin-top: -15px;
            width: 100px;
            height: 36px;
            font-size: 16px;
            color: #eee;
            text-align: center;
            line-height: 36px;
            background: lightseagreen;
            border-radius: 16px;
            cursor: pointer;
        }
        .bombBox {
            display: none;
            width: 140px;
            height: 30px;
            font-size: 20px;
            font-weight: bolder;
            color: brown;
            position: absolute;
            left: 50%;
            top: 50px;
            margin-left: -60px;
        }
        .gameBox {
            display: none;
            width: 500px;
            height: 500px;
            position: absolute;
            left: 50%;
            top: 80px;
            margin-left: -250px;
            transform: perspective(800px) rotateX(30deg);
            box-shadow: 5px 5px 5px rgba(0,0,0,0.3);
            border-top: 1px solid #b25f27;
            border-left: 1px solid #b25f27;
        }
        .closeBox {
            display: none;
            position: absolute;
            width: 100%;
            height: 100%;
            left: 0;
            top: 0;
            background: rgba(0,0,0,0.2);
        }
        .closeImg {
            position: absolute;
            left: 0;
            top: 0;
            right: 0;
            bottom: 0;
            margin: auto;
            width: 220px;
            height: 120px;
            background-size: 100% 100%;
            border: 1px solid red;
            border-radius: 10px;
        }
        .close {
            position: absolute;
            top: 0;
            right: 0;
            width: 30px;
            height: 30px;
            background: url('https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526279467215&di=782bca65ba6ba716b7fbdbf649b5a9e8&imgtype=jpg&src=http%3A%2F%2Fimg4.imgtn.bdimg.com%2Fit%2Fu%3D4135985014%2C651141433%26fm%3D214%26gp%3D0.jpg');
            background-size: 100% 100%;
            border-radius: 50%;
            cursor: pointer;
        }
        .block {
            width: 49px;
            height: 49px;
            background-color: forestgreen;
            border-right: 1px solid #B25F27;
            border-bottom: 1px solid #B25F27;
            box-shadow: 0 0 4px #333 inset;
            float: left;
        }
        .show {
            background-color: red;
        }
        .num {
            background: wheat;
            text-align: center;
            line-height: 49px;
            font-weight: bold;
        }
        .flag {
            background-image: url('https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526294867771&di=62cc912d4ae2f83821379dda72c5038c&imgtype=0&src=http%3A%2F%2Fimg7.ph.126.net%2FxGnwduuVUpoaVv_Ef4hz3w%3D%3D%2F2682175053093655587.jpg');
            background-size: 100% 100%;
        }



        html部分
    <div class="wrapper">
        <div class="startGame">开始游戏</div>
        <div class="bombBox" id="bombBox">
            剩余雷数：<span id="bombNum"></span>
        </div>
        <div class="gameBox" id="gameBox"></div>
        <div class="closeBox" id="closeBox">
            <div class="closeImg" id="closeImg">
                <div class="close" id="close"></div>
            </div>
        </div>
    </div>



    js部分

        var oStartGame = document.getElementsByClassName('startGame')[0];
        var bombBox = document.getElementById('bombBox');
        var gameBox = document.getElementById('gameBox');
        var closeBox = document.getElementsByClassName('closeBox')[0];
        var closeBox = document.getElementById('closeBox');
        var closeImg = document.getElementById('closeImg');
        var closeBtn = document.getElementById('close');
        var bombNum = document.getElementById('bombNum');
        var num;
        var over;
        var block;
        var map = [];
        var startGameBool = true;

        bindEvent();
        function bindEvent(){
            oStartGame.onclick = function (){
                if(startGameBool){
                    bombBox.style.display = 'block';
                    gameBox.style.display = 'block';
                    init();
                    startGameBool = false;
                }
            }
            gameBox.oncontextmenu = function (){
                return false;
            }
            gameBox.onmousedown = function (e){
                var event = e.target;
                if(e.which == 1){
                    leftClick(event);
                }else if(e.which == 3){
                    rightClick(event);
                }
                closeBtn.onclick = function (){
                    closeBox.style.display = 'none';
                    gameBox.style.display = 'none';
                    bombBox.style.display = 'none';
                    gameBox.innerHTML = '';
                    startGameBool = true;
                }
            }
        }

        function init(){
            num = 20;
            over = 20;
            bombNum.innerHTML = over;
            for(var i = 0; i < 10; i++){
                for(var j = 0; j < 10; j++){
                    var con = document.createElement('div');
                    con.classList.add('block');
                    con.setAttribute('id', i + '-' + j);
                    gameBox.appendChild(con);
                    map.push({mine:0});
                }
            }
            block = document.getElementsByClassName('block');
            while(num){
                var index = Math.floor(Math.random() * 100);
                if(map[index].mine === 0){
                    map[index].mine = 1;
                    block[index].classList.add('isLei');
                    num--;
                }
            }
        }

        function leftClick(dom){
            if(dom.classList.contains('flag')){
                return;
            }
            var isLei = document.getElementsByClassName('isLei');
            if(dom && dom.classList.contains('isLei')){
                console.log('gameOver');
                for(var i = 0; i < isLei.length; i++){
                    isLei[i].classList.add('show');
                }
                setTimeout(function (){
                    closeBox.style.display = 'block';
                    closeImg.style.backgroundImage = 'url("https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=3331856368,1061162331&fm=27&gp=0.jpg")';
                }, 500)
            }else{
                var n = 0;
                var posArr = dom && dom.getAttribute('id').split('-');
                var posX = posArr && +posArr[0];
                var posY = posArr && +posArr[1];
                dom && dom.classList.add('num');
                for(var i = posX - 1; i <= posX + 1; i++){
                    for(var j = posY - 1; j <= posY + 1; j++){
                        var aroundBox = document.getElementById(i + '-' + j);
                        if(aroundBox && aroundBox.classList.contains('isLei')){
                            n++;
                        }
                    }
                }
                dom && (dom.innerHTML = n);
                if(n == 0){
                    for(var i = posX - 1; i <= posX + 1; i++){
                        for(var j = posY - 1; j <= posY + 1; j++){
                            var nearBox = document.getElementById(i + '-' + j);
                            if(nearBox && nearBox.length != 0){
                                if(!nearBox.classList.contains('check')){
                                    nearBox.classList.add('check');
                                    leftClick(nearBox);
                                }
                            }
                        }
                    }
                }

            }
        }

        function rightClick(dom){
            if(dom.classList.contains('num')){
                return;
            }
            dom.classList.toggle('flag');
            if(dom.classList.contains('isLei') && dom.classList.contains('flag')){
                over--;
            }
            if(dom.classList.contains('isLei') && !dom.classList.contains('flag')){
                over++;
            }
            bombNum.innerHTML = over;
            if(over == 0){
                closeBox.style.display = 'block';
                closeImg.style.backgroundImage = 'url("https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526295904123&di=af8458af00567fc10baf30dd1c66a51c&imgtype=0&src=http%3A%2F%2Fimgsrc.baidu.com%2Fimage%2Fc0%253Dshijue1%252C0%252C0%252C294%252C40%2Fsign%3D5477740504f41bd5ce5ee0b739b3ebbe%2Fac6eddc451da81cb10b210e35866d01609243143.jpg")';
            }
        }

        
