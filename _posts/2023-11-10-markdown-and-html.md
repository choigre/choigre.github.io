---
layout: post
title: 코딩 소스 테스트
---
기술적인 코딩 정리

<!-- First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell -->

<!-- ![Geometric pattern with fading gradient]({{ site.baseurl }}/assets/img/sample_feature_img_2.png) -->


{% highlight js %}
// count to ten
for (var i = 1; i <= 10; i++) {
    console.log(i);
}

// count to twenty
var j = 0;
while (j < 20) {
    j++;
    console.log(j);
}
{% endhighlight %}


{% highlight js %}
let ball = document.querySelector('#ball');
ball.addEventListener('mousedown', (e)=>{
    //사전지식 1
    /*
        pageX, pageY - 스크롤을 포함한 좌표값
        clientX, clientY - 스크롤을 제외한 좌표값
        => 스크롤이 없는 화면에서는 pageX = clientX
        offsetX, offsetY - 요소의 좌표값 (부모태그 기준)
        screenX, screenY - 모니터(스크린) 기준 좌표값
        getBoundingClientRect() 요소의 좌표값 = offsetTop, offsetLeft 와 동일함 
        (단, transform:scale(0.5) 와 같은 변형을 주지않았을때, 부모가 static일때) 
        offsetTop, offsetLeft의 부모가 relative이거나 absolue 인경우에는 부모기준으로 left, top값이 정해진다
    */

    //사전지식 2
    /*  ball을 클릭했을때 좌표가 클릭영역을 기준으로 잡히므로
        클릭좌표값부터 요소의 영역 사이의 너비(혹은 높이)만큼
        움직이므로 그 차이만큼 빼야한다
    */

    ball.style.position = 'absolute';
    ball.style.zIndex = 1000;

    let diffX = e.clientX - ball.getBoundingClientRect().left;
    let diffY = e.clientY - ball.getBoundingClientRect().top;

    moveAt(e.pageX, e.pageY);

    function moveAt(pageX, pageY){
        ball.style.left = pageX - diffX + 'px';
        ball.style.top = pageY - diffY + 'px';

        //공이 빠져나가지 않게 페이지안에서만 움직이도록 범위지정하기
        //console.log( ball.getBoundingClientRect().left, ball.getBoundingClientRect().top );

        let newLeft = ball.getBoundingClientRect().left;
        let newTop = ball.getBoundingClientRect().top;

        console.log( newLeft, window.innerWidth - ball.offsetWidth);

        if( newLeft < 0 ){
            newLeft = 0;
            ball.style.left = newLeft;
        }
        /* X 범위를 초과하면 스크롤이 생김, - body내부에서는 안되는듯?? */
        if( newLeft > window.innerWidth - ball.offsetWidth ){
            newLeft = window.innerWidth - ball.offsetWidth;
            ball.style.left = newLeft;
        }

        if( newTop < 0 ) {
            newTop = 0;
            ball.style.top = newTop;
        }
        /* Y 범위를 초과하면 스크롤이 생김, - body내부에서는 안되는듯?? */
        if( newTop > window.innerHeight - ball.offsetHeight ){
            newTop = window.innerHeight - ball.offsetHeight;
            ball.style.top = newTop;
        }
    }

    function moveHandler(e){
        moveAt(e.pageX, e.pageY);
    }

    //mousemove 같은 경우에는 빠르게 마우스를 움직일경우 ball의 영역을 벗어날 수 잇으므로
    //ball.addEventListener('mousemove', func)
    document.addEventListener('mousemove', moveHandler);

    //ball을 움직일때는 움직이는 이벤트의 좌표값을 갱신해야하므로 새로운 함수를 호출해야한다, 
    //moveAt()을 재사용하면 안되는 이유, moveAt()에는 클릭했을때의 좌표값이 이미 저장되어 있으므로!
    ball.addEventListener('mouseup', (e)=>{
        document.removeEventListener('mousemove', moveHandler);
        ball.removeEventListener('mouseup', moveHandler);
    });

});
ball.ondragstart = ()=>{
    return false;
};
{% endhighlight %}
