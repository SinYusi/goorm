## 요구사항

- 1 layout 잡아가면서 시맨틱 마크업까지 따라하기
    - 0️⃣ `Header & Navigation Bar` 시작 코드
        
        ```jsx
        <!DOCTYPE html>
        <html>
        <head>
          <style>
            /* Simple Reset CSS */
            * {
              margin: 0;
              padding: 0;
              box-sizing: border-box;
            }
            body {
              font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
              color: #58666e;
              background-color: #f0f3f4;
            }
            li {
              list-style: none;
            }
            a {
              text-decoration: none;
            }
          </style>
        </head>
        <body>
          <div id="wrap">
            <header>
              <a class="logo" href="#home">
                <img src="https://poiemaweb.com/img/logo.png" height="36px">
              </a>
              <nav>
                <ul class="nav-items">
                  <li><a href="#home">Home</a></li>
                  <li><a href="#news">News</a></li>
                  <li><a href="#contact">Contact</a></li>
                  <li><a href="#about">About</a></li>
                </ul>
              </nav>
            </header>
          </div>
        </body>
        </html>
        ```
        
    - 1️⃣ `Header & Navigation Bar` 과정 코드
        
        ```html
        <!DOCTYPE html>
        <html>
          <head>
            <style>
              /* Simple Reset CSS */
              * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
              }
              body {
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                color: #58666e;
                background-color: #f0f3f4;
              }
              li {
                list-style: none;
              }
              a {
                text-decoration: none;
              }
              /* 1번. header 요소 영역 잡아주기 */
              header {
                width: 100%;
                height: 60px;
                z-index: 2000;
                background-color: #fff;
                box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
              }
              /* 2번. navigation bar 우측 정렬하기 */
              nav {
                float: right;
              }
              /* 3번. logo image 수직으로 중앙 정렬하기 */
              .logo {
                display: inline-block;
                height: 36px;
                margin: 12px 0 12px 25px;
              }
              /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
              .logo > img {
                /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                height: 36px;
              }
              /* 4번. navigation bar를 수평 정렬한다 */
              .nav-items > li {
                display: inline-block;
              }
              /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
              .nav-items > li > a {
                line-height: 60px;
                padding: 0 30px;
                color: rgba(0, 0, 0, 0.4);
              }
              /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
              .nav-items > li > a:hover {
                color: rgba(0, 0, 0, 0.8);
              }
            </style>
          </head>
          <body>
            <div id="wrap">
              <header>
                <a class="logo" href="#home">
                  <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                </a>
                <nav>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#news">News</a></li>
                    <li><a href="#contact">Contact</a></li>
                    <li><a href="#about">About</a></li>
                  </ul>
                </nav>
              </header>
            </div>
          </body>
        </html>
        
        ```
        
    - 2️⃣ `Section & Aside` 시작 코드
        
        > header 아래에 div#content-wrap 부분 코드의 HTML만 추가해주시면 됩니다.
        → aside 좌측정렬, section 우측 정렬을 만들어줄 것입니다.
        > 
        
        ```html
        <!DOCTYPE html>
        <html>
          <head>
            <style>
              /* Simple Reset CSS */
              * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
              }
              body {
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                color: #58666e;
                background-color: #f0f3f4;
              }
              li {
                list-style: none;
              }
              a {
                text-decoration: none;
              }
              /* 1번. header 요소 영역 잡아주기 */
              header {
                width: 100%;
                height: 60px;
                z-index: 2000;
                background-color: #fff;
                box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
              }
              /* 2번. navigation bar 우측 정렬하기 */
              nav {
                float: right;
              }
              /* 3번. logo image 수직으로 중앙 정렬하기 */
              .logo {
                display: inline-block;
                height: 36px;
                margin: 12px 0 12px 25px;
              }
              /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
              .logo > img {
                /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                height: 36px;
              }
              /* 4번. navigation bar를 수평 정렬한다 */
              .nav-items > li {
                display: inline-block;
              }
              /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
              .nav-items > li > a {
                line-height: 60px;
                padding: 0 30px;
                color: rgba(0, 0, 0, 0.4);
              }
              /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
              .nav-items > li > a:hover {
                color: rgba(0, 0, 0, 0.8);
              }
            </style>
          </head>
          <body>
            <div id="wrap">
              <header>
                <a class="logo" href="#home">
                  <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                </a>
                <nav>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#news">News</a></li>
                    <li><a href="#contact">Contact</a></li>
                    <li><a href="#about">About</a></li>
                  </ul>
                </nav>
              </header>
              <div id="content-wrap">
                <aside>
                  <h1>Aside</h1>
                  <ul>
                    <li><a href="#" class="active">London</a></li>
                    <li><a href="#">Paris</a></li>
                    <li><a href="#">Tokyo</a></li>
                    <li><a href="#">Newyork</a></li>
                  </ul>
                </aside>
                <section>
                  <article id="london">
                    <h1>London</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="paris">
                    <h1>Paris</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="tokyo">
                    <h1>Tokyo</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="newyork">
                    <h1>Newyork</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                </section>
                <!-- end of content-wrap   -->
              </div>
            </div>
          </body>
        </html>
        
        ```
        
    - 3️⃣ `Section & Aside` 과정 코드
        
        > aside style + navigation hover 시 컬러 구분
        > 
        
        ```html
        <!DOCTYPE html>
        <html>
          <head>
            <meta charset="utf-8" />
            <title>Layout Practice</title>
            <style>
              /* Simple Reset CSS */
              * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
              }
              body {
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                color: #58666e;
                background-color: #f0f3f4;
              }
              li {
                list-style: none;
              }
              a {
                text-decoration: none;
              }
              /* 15번. heading tag크기가 위치한 영역에 따라 다른 것을 방지하기 위해 reset css로 추가하기 */
              h1 {
                font-size: 1.8em;
              }
              h1,
              h2,
              h3,
              h4,
              h5,
              h6,
              p {
                margin: 10px 5px;
              }
        
              /* 1번. header 요소 영역 잡아주기 */
              header {
                /* 9번. navigation bar 상단 고정 -> 스크롤해도 고정 */
                position: fixed;
                top: 0;
        
                width: 100%;
                height: 60px;
                z-index: 2000;
                background-color: #fff;
                box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
              }
              /* 2번. navigation bar 우측 정렬하기 */
              nav {
                float: right;
              }
              /* 3번. logo image 수직으로 중앙 정렬하기 */
              .logo {
                display: inline-block;
                height: 36px;
                margin: 12px 0 12px 25px;
              }
              /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
              .logo > img {
                /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                height: 36px;
              }
              /* 4번. navigation bar를 수평 정렬한다 */
              .nav-items > li {
                display: inline-block;
              }
              /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
              .nav-items > li > a {
                line-height: 60px;
                padding: 0 30px;
                color: rgba(0, 0, 0, 0.4);
              }
              /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
              .nav-items > li > a:hover {
                color: rgba(0, 0, 0, 0.8);
              }
              /* 7번. aside 좌측 정렬, section 우측 정렬 */
              aside {
                /* float: left;
                width: 20%; */
        
                /* 11번. float 지우고 aside도 좌측 고정 */
                position: fixed;
                top: 60px;
                bottom: 0;
        
                width: 200px;
                /* 12번. aside 배경색 바꾸고 style 지정 */
                padding-top: 25px;
                background-color: #333;
              }
        
              /* 13번. aside navigation sytle 지정 */
              aside > ul {
                width: 200px;
              }
              aside > ul > li > a {
                display: block;
                color: #fff;
                padding: 10px 0 10px 20px;
              }
              aside > ul > li > a.active {
                background-color: #4caf50;
              }
              aside > ul > li > a:hover:not(.active) {
                background-color: #555;
              }
              aside > h1 {
                padding: 20px 0 20px 20px;
                color: #fff;
              }
        
              /* 14번, article style 지정 */
              article {
                margin: 10px;
                padding: 25px;
                background-color: white;
              }
        
              section {
                float: right;
                /* width: 80%; */
        
                /* 11-1. 위 width값 지우고 aside 만큼 margin left */
                margin-left: 200px;
              }
              /* 8번. clearfix -> float 프로퍼티가 선언된 두 개의 자식 요소를 포함하는 부모 요소 높이가 정상적인 값을 가지지 못하는 문제 해결 */
              #content-wrap:after {
                content: "";
                display: block;
                clear: both;
              }
              /* 10번. contents영역이 header와 겹치므로 header height 만큼 끌어내리기 */
              #wrap {
                margin-top: 60px;
              }
            </style>
          </head>
          <body>
            <div id="wrap">
              <header>
                <a class="logo" href="#home">
                  <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                </a>
                <nav>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#news">News</a></li>
                    <li><a href="#contact">Contact</a></li>
                    <li><a href="#about">About</a></li>
                  </ul>
                </nav>
              </header>
              <div id="content-wrap">
                <aside>
                  <h1>Aside</h1>
                  <ul>
                    <li><a href="#" class="active">London</a></li>
                    <li><a href="#">Paris</a></li>
                    <li><a href="#">Tokyo</a></li>
                    <li><a href="#">Newyork</a></li>
                  </ul>
                </aside>
                <section>
                  <article id="london">
                    <h1>London</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="paris">
                    <h1>Paris</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="tokyo">
                    <h1>Tokyo</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="newyork">
                    <h1>Newyork</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                </section>
                <!-- end of content-wrap   -->
              </div>
            </div>
          </body>
        </html>
        
        ```
        
    - 4️⃣ `Footer` 시작 코드
        
        > `content-wrap` 끝나는 부분에 추가되는 HTML 코드만 붙혀넣으시면 됩니다.
        > 
        
        ```html
        <!DOCTYPE html>
        <html>
          <head>
            <meta charset="utf-8" />
            <title>Layout Practice</title>
            <style>
              /* Simple Reset CSS */
              * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
              }
              body {
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                color: #58666e;
                background-color: #f0f3f4;
              }
              li {
                list-style: none;
              }
              a {
                text-decoration: none;
              }
              /* 15번. heading tag크기가 위치한 영역에 따라 다른 것을 방지하기 위해 reset css로 추가하기 */
              h1 {
                font-size: 1.8em;
              }
              h1,
              h2,
              h3,
              h4,
              h5,
              h6,
              p {
                margin: 10px 5px;
              }
        
              /* 1번. header 요소 영역 잡아주기 */
              header {
                /* 9번. navigation bar 상단 고정 -> 스크롤해도 고정 */
                position: fixed;
                top: 0;
        
                width: 100%;
                height: 60px;
                z-index: 2000;
                background-color: #fff;
                box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
              }
              /* 2번. navigation bar 우측 정렬하기 */
              nav {
                float: right;
              }
              /* 3번. logo image 수직으로 중앙 정렬하기 */
              .logo {
                display: inline-block;
                height: 36px;
                margin: 12px 0 12px 25px;
              }
              /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
              .logo > img {
                /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                height: 36px;
              }
              /* 4번. navigation bar를 수평 정렬한다 */
              .nav-items > li {
                display: inline-block;
              }
              /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
              .nav-items > li > a {
                line-height: 60px;
                padding: 0 30px;
                color: rgba(0, 0, 0, 0.4);
              }
              /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
              .nav-items > li > a:hover {
                color: rgba(0, 0, 0, 0.8);
              }
              /* 7번. aside 좌측 정렬, section 우측 정렬 */
              aside {
                /* float: left;
                width: 20%; */
        
                /* 11번. float 지우고 aside도 좌측 고정 */
                position: fixed;
                top: 60px;
                bottom: 0;
        
                width: 200px;
                /* 12번. aside 배경색 바꾸고 style 지정 */
                padding-top: 25px;
                background-color: #333;
              }
        
              /* 13번. aside navigation sytle 지정 */
              aside > ul {
                width: 200px;
              }
              aside > ul > li > a {
                display: block;
                color: #fff;
                padding: 10px 0 10px 20px;
              }
              aside > ul > li > a.active {
                background-color: #4caf50;
              }
              aside > ul > li > a:hover:not(.active) {
                background-color: #555;
              }
              aside > h1 {
                padding: 20px 0 20px 20px;
                color: #fff;
              }
        
              /* 14번, article style 지정 */
              article {
                margin: 10px;
                padding: 25px;
                background-color: white;
              }
        
              section {
                float: right;
                /* width: 80%; */
        
                /* 11-1. 위 width값 지우고 aside 만큼 margin left */
                margin-left: 200px;
              }
              /* 8번. clearfix -> float 프로퍼티가 선언된 두 개의 자식 요소를 포함하는 부모 요소 높이가 정상적인 값을 가지지 못하는 문제 해결 */
              #content-wrap:after {
                content: "";
                display: block;
                clear: both;
              }
              /* 10번. contents영역이 header와 겹치므로 header height 만큼 끌어내리기 */
              #wrap {
                margin-top: 60px;
              }
            </style>
          </head>
          <body>
            <div id="wrap">
              <header>
                <a class="logo" href="#home">
                  <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                </a>
                <nav>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#news">News</a></li>
                    <li><a href="#contact">Contact</a></li>
                    <li><a href="#about">About</a></li>
                  </ul>
                </nav>
              </header>
              <div id="content-wrap">
                <aside>
                  <h1>Aside</h1>
                  <ul>
                    <li><a href="#" class="active">London</a></li>
                    <li><a href="#">Paris</a></li>
                    <li><a href="#">Tokyo</a></li>
                    <li><a href="#">Newyork</a></li>
                  </ul>
                </aside>
                <section>
                  <article id="london">
                    <h1>London</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="paris">
                    <h1>Paris</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="tokyo">
                    <h1>Tokyo</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="newyork">
                    <h1>Newyork</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                </section>
                <!-- end of content-wrap   -->
              </div>
              <footer>© Copyright 2016 ungmo2</footer>
            </div>
          </body>
        </html>
        
        ```
        
    - 5️⃣ `Footer` 과정 코드
        
        ```html
        <!DOCTYPE html>
        <html>
          <head>
            <meta charset="utf-8" />
            <title>Layout Practice</title>
            <style>
              /* Simple Reset CSS */
              * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
              }
              body {
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                color: #58666e;
                background-color: #f0f3f4;
              }
              li {
                list-style: none;
              }
              a {
                text-decoration: none;
              }
              /* 15번. heading tag크기가 위치한 영역에 따라 다른 것을 방지하기 위해 reset css로 추가하기 */
              h1 {
                font-size: 1.8em;
              }
              h1,
              h2,
              h3,
              h4,
              h5,
              h6,
              p {
                margin: 10px 5px;
              }
        
              /* 1번. header 요소 영역 잡아주기 */
              header {
                /* 9번. navigation bar 상단 고정 -> 스크롤해도 고정 */
                position: fixed;
                top: 0;
        
                width: 100%;
                height: 60px;
                z-index: 2000;
                background-color: #fff;
                box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
              }
              /* 2번. navigation bar 우측 정렬하기 */
              nav {
                float: right;
              }
              /* 3번. logo image 수직으로 중앙 정렬하기 */
              .logo {
                display: inline-block;
                height: 36px;
                margin: 12px 0 12px 25px;
              }
              /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
              .logo > img {
                /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                height: 36px;
              }
              /* 4번. navigation bar를 수평 정렬한다 */
              .nav-items > li {
                display: inline-block;
              }
              /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
              .nav-items > li > a {
                line-height: 60px;
                padding: 0 30px;
                color: rgba(0, 0, 0, 0.4);
              }
              /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
              .nav-items > li > a:hover {
                color: rgba(0, 0, 0, 0.8);
              }
              /* 7번. aside 좌측 정렬, section 우측 정렬 */
              aside {
                /* float: left;
                width: 20%; */
        
                /* 11번. float 지우고 aside도 좌측 고정 */
                position: fixed;
                top: 60px;
                bottom: 0;
        
                width: 200px;
                /* 12번. aside 배경색 바꾸고 style 지정 */
                padding-top: 25px;
                background-color: #333;
              }
        
              /* 13번. aside navigation sytle 지정 */
              aside > ul {
                width: 200px;
              }
              aside > ul > li > a {
                display: block;
                color: #fff;
                padding: 10px 0 10px 20px;
              }
              aside > ul > li > a.active {
                background-color: #4caf50;
              }
              aside > ul > li > a:hover:not(.active) {
                background-color: #555;
              }
              aside > h1 {
                padding: 20px 0 20px 20px;
                color: #fff;
              }
        
              /* 14번, article style 지정 */
              article {
                margin: 10px;
                padding: 25px;
                background-color: white;
              }
        
              section {
                float: right;
                /* width: 80%; */
        
                /* 11-1. 위 width값 지우고 aside 만큼 margin left */
                margin-left: 200px;
              }
              /* 8번. clearfix -> float 프로퍼티가 선언된 두 개의 자식 요소를 포함하는 부모 요소 높이가 정상적인 값을 가지지 못하는 문제 해결 */
              #content-wrap:after {
                content: "";
                display: block;
                clear: both;
              }
              /* 10번. contents영역이 header와 겹치므로 header height 만큼 끌어내리기 */
              #wrap {
                margin-top: 60px;
              }
        
              /* 16번. footer를 aside위에 올리기 */
              footer {
                position: absolute;
                height: 60px;
                width: 100%;
                padding: 0 25px;
                line-height: 60px;
                color: #8a8c8f;
                border-top: 1px solid #dee5e7;
                background-color: #f2f2f2;
              }
            </style>
          </head>
          <body>
            <div id="wrap">
              <header>
                <a class="logo" href="#home">
                  <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                </a>
                <nav>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#news">News</a></li>
                    <li><a href="#contact">Contact</a></li>
                    <li><a href="#about">About</a></li>
                  </ul>
                </nav>
              </header>
              <div id="content-wrap">
                <aside>
                  <h1>Aside</h1>
                  <ul>
                    <li><a href="#" class="active">London</a></li>
                    <li><a href="#">Paris</a></li>
                    <li><a href="#">Tokyo</a></li>
                    <li><a href="#">Newyork</a></li>
                  </ul>
                </aside>
                <section>
                  <article id="london">
                    <h1>London</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="paris">
                    <h1>Paris</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="tokyo">
                    <h1>Tokyo</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                  <article id="newyork">
                    <h1>Newyork</h1>
                    <p>
                      Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                      elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                      enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                      nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                      reprehenderit in voluptate velit essa cillum dolare eu tugial
                      nulla pariatur Excepteur sint accaecat cupidatat non proident,
                      sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </p>
                  </article>
                </section>
                <!-- end of content-wrap   -->
              </div>
              <footer>© Copyright 2016 ungmo2</footer>
            </div>
          </body>
        </html>
        
        ```
        
- 2 위  레이아웃을 반응형으로 제작
    - 요구사항
        - 모바일, 태블릿, 데스크탑 3단계로 구분
        - Non Mobile First Method로 정의
        - breakpoint media query 코드
            
            ```html
            <!DOCTYPE html>
            <html>
            <head>
              <meta name="viewport" content="width=device-width, initial-scale=1.0">
              <style>
                /* Media Query */
                /* for Desktop: 801px ~ */
                /* 여기에 따로 미디어 쿼리 쓰지 않아도 이 영역의 코드는 데스크탑을 위한 코드입니다. */
            
                /* for tablet: ~ 800px */
                @media screen and (max-width: 800px) {
            
                }
                /* for smartphone: ~ 480px */
                @media screen and (max-width: 480px) {
            
                }
              </style>
            </head>
            ...
            ```
            
            여기서 주의할 점은 CSS 적용 우선 순위에 따라 나중에 선언된 스타일이 우선 적용된다는 것.
            즉, 만약 모바일 스타일을 태블릿 스타일보다 먼저 기술하면 최종적으로 태블릿용 스타일이 적용된다는 뜻
            따라서, Non Mobile fist 방식의 경우, max-width 값이 큰 것부터 기술해야 함
            (만약 반대로 쓴다면 모바일 너비에서도 가장 마지막에 작성된 데스크탑 스타일이 적용)
            
    - 화면 너비 줄였을 때 header navigation bar 깨지는 현상 수정하기
        - tablet
            
            ![image.png](attachment:6d3f57a0-fe64-4f66-9241-64c11b90e0b0:image.png)
            
            1. header 영역의 높이를 2배로 넓히고, logo & navigation bar를 center로 옮긺
            2. aside, section 영역도 header의 height만큼 내림
            3. logo & navigation 상단, 하단으로 분리 배치하기 위해 float을 해제해 block 요소를 만듦
            
            ```css
            /* for tablet: ~ 800px */
            @media screen and (max-width: 800px) {
              /* 시각적으로 반응형 확인용 백그라운드 */
              /* body {
                background-color: lightgreen;
              } */ 
              
              /* 1번 */
              header {
                height: 120px;
                text-align: center;
              }
              
              /* 3번 */
              nav {
                float: none;
              }
              
               /* 2번 */
              #wrap {
                /* margin-top = header height */
                margin-top: 120px;
              }
              aside {
                top: 120px;
              }
            }
            ```
            
        - mobile
            
            ![image.png](attachment:66604469-f405-4cea-807a-f08f3a908898:image.png)
            
            ![image.png](attachment:9ad5354a-9ecd-4022-9f8d-a31827832af5:image.png)
            
            1. 기존 코드에서 nav 요소 내에 클릭할 수 있는 navigation icon을 만들기 위한 html 추가
                1. `label tag`의 `for` 프로퍼티 값과 `input tag`의 `id` 프로퍼티값이 일치하여야 한다.
                → input checkbox 요소의 id 프로퍼티값과 label 요소의 for 프로퍼티값을 일치시켜 연동하면 label 요소를 클릭하여도 input checkbox 요소가 클릭됨.
                
                ```html
                <nav>
                  <input class="nav-toggle" id="nav-toggle" type="checkbox">
                  <label class="navicon" for="nav-toggle"><span class="navicon-bar"></span></label>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                ...
                ```
                
            2. `navicon`은 header 우측에 배치
            3. `label tag > span tag` 스타일을 정의로 내부 막대 1개를 표기
            → `span tag`는 내부 막대 혹은 `X 표시`를 위해 정의
            4. 가상 요소 선택자를 사용하여 내부 막대 앞뒤 공간에 내부 막대를 추가.
            5. 위치 지정을 위해 가상 요소의 부모 요소인 `span (.navicon-bar)`에 `relative` 추가
            6. input checkbox tag가 checked 되어 있을 때 X 표시로 보이도록 만들기
            → + transition 효과까지
            7. 이제 모바일 레이아웃 이외의 경우 보이지 않도록 display none 해줌
            8. 모바일에 header 다시 60px로 되돌리고, navicon을 보이게 해줌
            9. 마지막으로 navigation icon 클릭하면 navigation item 표시되도록 구현
            - 실습용 코드
                
                ```html
                <!DOCTYPE html>
                <html>
                  <head>
                    <meta charset="utf-8" />
                    <title>Layout Practice</title>
                    <style>
                      /* Simple Reset CSS */
                      * {
                        margin: 0;
                        padding: 0;
                        box-sizing: border-box;
                      }
                      body {
                        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                        color: #58666e;
                        background-color: #f0f3f4;
                      }
                      li {
                        list-style: none;
                      }
                      a {
                        text-decoration: none;
                      }
                      /* 15번. heading tag크기가 위치한 영역에 따라 다른 것을 방지하기 위해 reset css로 추가하기 */
                      h1 {
                        font-size: 1.8em;
                      }
                      h1,
                      h2,
                      h3,
                      h4,
                      h5,
                      h6,
                      p {
                        margin: 10px 5px;
                      }
                
                      /* 1번. header 요소 영역 잡아주기 */
                      header {
                        /* 9번. navigation bar 상단 고정 -> 스크롤해도 고정 */
                        position: fixed;
                        top: 0;
                
                        width: 100%;
                        height: 60px;
                        z-index: 2000;
                        background-color: #fff;
                        box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
                      }
                      /* 2번. navigation bar 우측 정렬하기 */
                      nav {
                        float: right;
                      }
                      /* 3번. logo image 수직으로 중앙 정렬하기 */
                      .logo {
                        display: inline-block;
                        height: 36px;
                        margin: 12px 0 12px 25px;
                      }
                      /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
                      .logo > img {
                        /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                        height: 36px;
                      }
                      /* 4번. navigation bar를 수평 정렬한다 */
                      .nav-items > li {
                        display: inline-block;
                      }
                      /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
                      .nav-items > li > a {
                        line-height: 60px;
                        padding: 0 30px;
                        color: rgba(0, 0, 0, 0.4);
                      }
                      /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
                      .nav-items > li > a:hover {
                        color: rgba(0, 0, 0, 0.8);
                      }
                
                      /* 1번 - 반응형 레이아웃 실습 */
                      .navicon {
                        /* cursor: pointer;
                        height: 60px;
                        padding: 28px 15px;
                        position: absolute;
                        top: 0;
                        right: 0;
                        user-select: none; */
                      }
                      .navicon-bar {
                        /* display: block;
                        width: 20px;
                        height: 3px;
                        background-color: #333;
                        position: relative; */
                
                        /* 4번 - 반응형 레이아웃 실습 */
                        /* transition: background-color 0.2s ease-out; */
                      }
                
                      /* 2번 - 반응형 레이아웃 실습 */
                      /* 막대를 3개로 만들어줍니다 이때 위치 지정을 위해 .navicon-bar 에 relative 속성 추가 */
                      .navicon-bar::before,
                      .navicon-bar::after {
                        /* background-color: #333;
                        content: "";
                        display: block;
                        height: 100%;
                        width: 100%;
                        position: absolute; */
                      }
                      .navicon-bar::before {
                        /* top: -7px; */
                      }
                      .navicon-bar::after {
                        /* top: 7px; */
                      }
                
                      /* 3번 - 반응형 레이아웃 실습 */
                      /* input checkbox의 checked를 이용하여 클릭되었을때,아닐때 구분하여 스타일 지정 */
                      /*  .nav-toggle:checked ~ .navicon => .nav-toggle:checked 다음 형제 요소 .navicon 모두 선택한다는 의미 */
                      .nav-toggle:checked ~ .navicon > .navicon-bar {
                        /* background: transparent; */
                      }
                      .nav-toggle:checked ~ .navicon > .navicon-bar::before {
                        /* transform: rotate(45deg);
                        top: 0; */
                      }
                      .nav-toggle:checked ~ .navicon > .navicon-bar::after {
                        /* transform: rotate(-45deg);
                        top: 0; */
                      }
                
                      /* 7번. aside 좌측 정렬, section 우측 정렬 */
                      aside {
                        /* float: left;
                        width: 20%; */
                
                        /* 11번. float 지우고 aside도 좌측 고정 */
                        position: fixed;
                        top: 60px;
                        bottom: 0;
                
                        width: 200px;
                        /* 12번. aside 배경색 바꾸고 style 지정 */
                        padding-top: 25px;
                        background-color: #333;
                      }
                
                      /* 13번. aside navigation sytle 지정 */
                      aside > ul {
                        width: 200px;
                      }
                      aside > ul > li > a {
                        display: block;
                        color: #fff;
                        padding: 10px 0 10px 20px;
                      }
                      aside > ul > li > a.active {
                        background-color: #4caf50;
                      }
                      aside > ul > li > a:hover:not(.active) {
                        background-color: #555;
                      }
                      aside > h1 {
                        padding: 20px 0 20px 20px;
                        color: #fff;
                      }
                
                      /* 14번, article style 지정 */
                      article {
                        margin: 10px;
                        padding: 25px;
                        background-color: white;
                      }
                
                      section {
                        float: right;
                        /* width: 80%; */
                
                        /* 11-1. 위 width값 지우고 aside 만큼 margin left */
                        margin-left: 200px;
                      }
                      /* 8번. clearfix -> float 프로퍼티가 선언된 두 개의 자식 요소를 포함하는 부모 요소 높이가 정상적인 값을 가지지 못하는 문제 해결 */
                      #content-wrap:after {
                        content: "";
                        display: block;
                        clear: both;
                      }
                      /* 10번. contents영역이 header와 겹치므로 header height 만큼 끌어내리기 */
                      #wrap {
                        margin-top: 60px;
                      }
                
                      /* 16번. footer를 aside위에 올리기 */
                      footer {
                        position: absolute;
                        height: 60px;
                        width: 100%;
                        padding: 0 25px;
                        line-height: 60px;
                        color: #8a8c8f;
                        border-top: 1px solid #dee5e7;
                        background-color: #f2f2f2;
                      }
                
                      /* 5번 - 반응형 레이아웃 실습 */
                      .nav-toggle {
                        /* display: none; */
                      }
                      .navicon {
                        /* display: none; */
                      }
                
                      /* for tablet: ~ 800px */
                      @media screen and (max-width: 800px) {
                        body {
                          background-color: lightgreen;
                        }
                        header {
                          height: 120px;
                          text-align: center;
                        }
                        nav {
                          float: none;
                        }
                        #wrap {
                          /* margin-top = header height */
                          margin-top: 120px;
                        }
                        aside {
                          top: 120px;
                        }
                      }
                
                      /* for smartphone: ~ 480px */
                      @media screen and (max-width: 480px) {
                        /* 6번 - 반응형 레이아웃 실습 */
                        header {
                          /* height: 60px; */
                        }
                        .nav-items {
                          /* display: none; */
                        }
                        .navicon {
                          /* display: block; */
                        }
                
                        /* 7번 - 반응형 레이아웃 실습 */
                        #wrap {
                          /* 컨텐츠의 여백은 헤더 높이에 따라 조정필요함. margin-top = header height */
                          /* margin-top: 60px; */
                        }
                        aside {
                          /* top: 60px; */
                        }
                
                        /* 8번 - 반응형 레이아웃 실습 */
                        .nav-toggle:checked ~ .nav-items {
                          /* display: block;
                          width: 100%;
                          background-color: #fff;
                          box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05); */
                        }
                        .nav-items > li {
                          /* display: block; */
                        }
                        .nav-items > li > a {
                          /* line-height: 50px; */
                        }
                      }
                    </style>
                  </head>
                  <body>
                    <div id="wrap">
                      <header>
                        <a class="logo" href="#home">
                          <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                        </a>
                        <nav>
                          <input class="nav-toggle" id="nav-toggle" type="checkbox" />
                          <label class="navicon" for="nav-toggle"
                            ><span class="navicon-bar"></span
                          ></label>
                          <ul class="nav-items">
                            <li><a href="#home">Home</a></li>
                            <li><a href="#news">News</a></li>
                            <li><a href="#contact">Contact</a></li>
                            <li><a href="#about">About</a></li>
                          </ul>
                        </nav>
                      </header>
                      <div id="content-wrap">
                        <aside>
                          <h1>Aside</h1>
                          <ul>
                            <li><a href="#" class="active">London</a></li>
                            <li><a href="#">Paris</a></li>
                            <li><a href="#">Tokyo</a></li>
                            <li><a href="#">Newyork</a></li>
                          </ul>
                        </aside>
                        <section>
                          <article id="london">
                            <h1>London</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                          <article id="paris">
                            <h1>Paris</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                          <article id="tokyo">
                            <h1>Tokyo</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                          <article id="newyork">
                            <h1>Newyork</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                        </section>
                        <!-- end of content-wrap   -->
                      </div>
                      <footer>© Copyright 2016 ungmo2</footer>
                    </div>
                  </body>
                </html>
                
                ```
                
            - 완성 코드
                
                ```html
                <!DOCTYPE html>
                <html>
                  <head>
                    <meta charset="utf-8" />
                    <title>Layout Practice</title>
                    <style>
                      /* Simple Reset CSS */
                      * {
                        margin: 0;
                        padding: 0;
                        box-sizing: border-box;
                      }
                      body {
                        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                        color: #58666e;
                        background-color: #f0f3f4;
                      }
                      li {
                        list-style: none;
                      }
                      a {
                        text-decoration: none;
                      }
                      /* 15번. heading tag크기가 위치한 영역에 따라 다른 것을 방지하기 위해 reset css로 추가하기 */
                      h1 {
                        font-size: 1.8em;
                      }
                      h1,
                      h2,
                      h3,
                      h4,
                      h5,
                      h6,
                      p {
                        margin: 10px 5px;
                      }
                
                      /* 1번. header 요소 영역 잡아주기 */
                      header {
                        /* 9번. navigation bar 상단 고정 -> 스크롤해도 고정 */
                        position: fixed;
                        top: 0;
                
                        width: 100%;
                        height: 60px;
                        z-index: 2000;
                        background-color: #fff;
                        box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
                      }
                      /* 2번. navigation bar 우측 정렬하기 */
                      nav {
                        float: right;
                      }
                      /* 3번. logo image 수직으로 중앙 정렬하기 */
                      .logo {
                        display: inline-block;
                        height: 36px;
                        margin: 12px 0 12px 25px;
                      }
                      /* 3-1번. img 태그에 부여한 height 어트리뷰트를 css로 옮기기 */
                      .logo > img {
                        /* 높이 36px + margin top 12px + margin bottom 12px = 60px */
                        height: 36px;
                      }
                      /* 4번. navigation bar를 수평 정렬한다 */
                      .nav-items > li {
                        display: inline-block;
                      }
                      /* 5번. navigation bar를 수직정렬하기 위해 텍스트높이를 header height과 동일하게 60px로 고정 */
                      .nav-items > li > a {
                        line-height: 60px;
                        padding: 0 30px;
                        color: rgba(0, 0, 0, 0.4);
                      }
                      /* 6번. navigation bar위에 마우스 올라오면 Navigation item 텍스트 색상이 변경되도록 */
                      .nav-items > li > a:hover {
                        color: rgba(0, 0, 0, 0.8);
                      }
                
                      /* 1번 - 반응형 레이아웃 실습 */
                      .navicon {
                        cursor: pointer;
                        height: 60px;
                        padding: 28px 15px;
                        position: absolute;
                        top: 0;
                        right: 0;
                        user-select: none;
                      }
                      .navicon-bar {
                        display: block;
                        width: 20px;
                        height: 3px;
                        background-color: #333;
                        position: relative;
                
                        /* 4번 - 반응형 레이아웃 실습 */
                        transition: background-color 0.2s ease-out;
                      }
                
                      /* 2번 - 반응형 레이아웃 실습 */
                      /* 막대를 3개로 만들어줍니다 이때 위치 지정을 위해 .navicon-bar 에 relative 속성 추가 */
                      .navicon-bar::before,
                      .navicon-bar::after {
                        background-color: #333;
                        content: "";
                        display: block;
                        height: 100%;
                        width: 100%;
                        position: absolute;
                      }
                      .navicon-bar::before {
                        top: -7px;
                      }
                      .navicon-bar::after {
                        top: 7px;
                      }
                
                      /* 3번 - 반응형 레이아웃 실습 */
                      /* input checkbox의 checked를 이용하여 클릭되었을때,아닐때 구분하여 스타일 지정 */
                      /*  .nav-toggle:checked ~ .navicon => .nav-toggle:checked 다음 형제 요소 .navicon 모두 선택한다는 의미 */
                      .nav-toggle:checked ~ .navicon > .navicon-bar {
                        background: transparent;
                      }
                      .nav-toggle:checked ~ .navicon > .navicon-bar::before {
                        transform: rotate(45deg);
                        top: 0;
                      }
                      .nav-toggle:checked ~ .navicon > .navicon-bar::after {
                        transform: rotate(-45deg);
                        top: 0;
                      }
                
                      /* 7번. aside 좌측 정렬, section 우측 정렬 */
                      aside {
                        /* float: left;
                        width: 20%; */
                
                        /* 11번. float 지우고 aside도 좌측 고정 */
                        position: fixed;
                        top: 60px;
                        bottom: 0;
                
                        width: 200px;
                        /* 12번. aside 배경색 바꾸고 style 지정 */
                        padding-top: 25px;
                        background-color: #333;
                      }
                
                      /* 13번. aside navigation sytle 지정 */
                      aside > ul {
                        width: 200px;
                      }
                      aside > ul > li > a {
                        display: block;
                        color: #fff;
                        padding: 10px 0 10px 20px;
                      }
                      aside > ul > li > a.active {
                        background-color: #4caf50;
                      }
                      aside > ul > li > a:hover:not(.active) {
                        background-color: #555;
                      }
                      aside > h1 {
                        padding: 20px 0 20px 20px;
                        color: #fff;
                      }
                
                      /* 14번, article style 지정 */
                      article {
                        margin: 10px;
                        padding: 25px;
                        background-color: white;
                      }
                
                      section {
                        float: right;
                        /* width: 80%; */
                
                        /* 11-1. 위 width값 지우고 aside 만큼 margin left */
                        margin-left: 200px;
                      }
                      /* 8번. clearfix -> float 프로퍼티가 선언된 두 개의 자식 요소를 포함하는 부모 요소 높이가 정상적인 값을 가지지 못하는 문제 해결 */
                      #content-wrap:after {
                        content: "";
                        display: block;
                        clear: both;
                      }
                      /* 10번. contents영역이 header와 겹치므로 header height 만큼 끌어내리기 */
                      #wrap {
                        margin-top: 60px;
                      }
                
                      /* 16번. footer를 aside위에 올리기 */
                      footer {
                        position: absolute;
                        height: 60px;
                        width: 100%;
                        padding: 0 25px;
                        line-height: 60px;
                        color: #8a8c8f;
                        border-top: 1px solid #dee5e7;
                        background-color: #f2f2f2;
                      }
                
                      /* 5번 - 반응형 레이아웃 실습 */
                      .nav-toggle {
                        display: none;
                      }
                      .navicon {
                        display: none;
                      }
                
                      /* for tablet: ~ 800px */
                      @media screen and (max-width: 800px) {
                        body {
                          background-color: lightgreen;
                        }
                        header {
                          height: 120px;
                          text-align: center;
                        }
                        nav {
                          float: none;
                        }
                        #wrap {
                          /* margin-top = header height */
                          margin-top: 120px;
                        }
                        aside {
                          top: 120px;
                        }
                      }
                
                      /* for smartphone: ~ 480px */
                      @media screen and (max-width: 480px) {
                        /* 6번 - 반응형 레이아웃 실습 */
                        header {
                          height: 60px;
                        }
                        .nav-items {
                          display: none;
                        }
                        .navicon {
                          display: block;
                        }
                        /* 7번 - 반응형 레이아웃 실습 */
                        #wrap {
                          /* margin-top = header height */
                          margin-top: 60px;
                        }
                        aside {
                          top: 60px;
                        }
                        /* 8번 - 반응형 레이아웃 실습 */
                        .nav-toggle:checked ~ .nav-items {
                          display: block;
                          width: 100%;
                          background-color: #fff;
                          box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
                        }
                        .nav-items > li {
                          display: block;
                        }
                        .nav-items > li > a {
                          line-height: 50px;
                        }
                      }
                    </style>
                  </head>
                  <body>
                    <div id="wrap">
                      <header>
                        <a class="logo" href="#home">
                          <img src="https://poiemaweb.com/img/logo.png" height="36px" />
                        </a>
                        <nav>
                          <input class="nav-toggle" id="nav-toggle" type="checkbox" />
                          <label class="navicon" for="nav-toggle"
                            ><span class="navicon-bar"></span
                          ></label>
                          <ul class="nav-items">
                            <li><a href="#home">Home</a></li>
                            <li><a href="#news">News</a></li>
                            <li><a href="#contact">Contact</a></li>
                            <li><a href="#about">About</a></li>
                          </ul>
                        </nav>
                      </header>
                      <div id="content-wrap">
                        <aside>
                          <h1>Aside</h1>
                          <ul>
                            <li><a href="#" class="active">London</a></li>
                            <li><a href="#">Paris</a></li>
                            <li><a href="#">Tokyo</a></li>
                            <li><a href="#">Newyork</a></li>
                          </ul>
                        </aside>
                        <section>
                          <article id="london">
                            <h1>London</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                          <article id="paris">
                            <h1>Paris</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                          <article id="tokyo">
                            <h1>Tokyo</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                          <article id="newyork">
                            <h1>Newyork</h1>
                            <p>
                              Lorem Ipsum dolor sit anet, consecterur adipisicing elit, sed do
                              elusmod tempor incididunt ut labore el dolore magna aliqua, Ut
                              enimi ad irinim veniam, quis nostrud exercitation ullarco laboris
                              nisi ut aliquip ex ea commado consequat. Duis aute inure delar in
                              reprehenderit in voluptate velit essa cillum dolare eu tugial
                              nulla pariatur Excepteur sint accaecat cupidatat non proident,
                              sunt in culpa qui officia deserunt mollit anim id est laborum.
                            </p>
                          </article>
                        </section>
                        <!-- end of content-wrap   -->
                      </div>
                      <footer>© Copyright 2016 ungmo2</footer>
                    </div>
                  </body>
                </html>
                
                ```
                
- 3 위 실습 수정
    - 요구사항
        - tablet, desktop일 때에는 article이 2열로 배치, mobile일 때는 1열로 배치되도록 제작
        - tablet ~ desktop
            
            ![image.png](attachment:22f0165b-2518-460e-8b3c-ed7f06ee6c55:image.png)
            
        - mobile
            
            ![image.png](attachment:d5dab0ad-c6ba-4f91-9835-2dcefce92ed1:image.png)
            
    - 정답 코드
        
        ```html
        <!DOCTYPE html>
        <html>
          <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <meta http-equiv="X-UA-Compatible" content="ie=edge">
            <style>
              /* Simple Reset CSS */
              * {
                margin: 0; padding: 0;
                box-sizing: border-box;
              }
              body {
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
                color: #58666e;
                background-color: #f0f3f4;
                -webkit-font-smoothing: antialiased;
                -webkit-text-size-adjus: 100%;  /* iphone font size 변경 방지 */
              }
              li { list-style: none; }
              a { text-decoration: none; }
              h1, h2, h3, h4, h5, h6, p {
                margin: 10px 5px;
              }
              h1 { font-size: 1.8em; }
        
              #wrap {
                width: 100%;
                /* margin-top = header height */
                margin-top: 60px;
              }
        
              /* Navigation bar */
              header {
                /* for sticky header */
                position: fixed;
                top: 0;
        
                width: 100%;
                height: 60px;
                z-index: 2000;
                background-color: #fff;
                box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
              }
              .logo {
                display: inline-block;
                height: 36px;
                margin: 12px 0 12px 25px;
              }
              .logo > img { height: 36px; }
              nav {
                float: right;
              }
              .nav-items {
                margin-right: 20px;
              }
              .nav-items > li {
                display: inline-block; /* 가로정렬 */
              }
              .nav-items > li > a {
                line-height: 60px; /* for Vertical Centering */
                padding: 0 30px;   /* nav item간 간격 */
                color: rgba(0,0,0,0.4);
              }
              .nav-items > li > a:hover {
                color: rgba(0,0,0,0.8);
              }
        
              /* navigation icon for Mobile Layout */
              .navicon {
                cursor: pointer;
                height: 60px;
                padding: 28px 15px;
                position: absolute;
                top: 0; right: 0;
        
                -webkit-user-select: none;  /* Chrome all / Safari all */
                -moz-user-select: none;     /* Firefox all */
                -ms-user-select: none;      /* IE 10+ */
                user-select: none;          /* Likely future */
              }
              /* nav icon의 내부 막대 */
              .navicon-bar {
                background-color: #333;
                display: block;
                position: relative;
                /* navigation icon animation */
                transition: background-color .2s ease-out;
                width: 20px;
                height: 3px;
              }
              .navicon-bar::before,
              .navicon-bar::after {
                background-color: #333;
                content: "";
                display: block;
                height: 100%;
                position: absolute;
                /* navigation icon animation */
                transition: all .2s ease-out;
                width: 100%;
              }
              .navicon-bar::before {
                top: -7px;
              }
              .navicon-bar::after {
                top: 7px;
              }
              /* toggle navigation icon */
              .nav-toggle:checked ~ .navicon > .navicon-bar {
                background: transparent;
              }
              .nav-toggle:checked ~ .navicon > .navicon-bar::before {
                transform: rotate(45deg);
                top: 0;
              }
              .nav-toggle:checked ~ .navicon > .navicon-bar::after {
                transform: rotate(-45deg);
                top: 0;
              }
        
              /* contents */
              /* clearfix */
              #content-wrap:after {
                content: "";
                display: block;
                clear: both;
              }
              aside {
                /* for fixed side bar */
                position: fixed;
                top: 60px;
                bottom: 0;
        
                width: 200px;  /* 너비 고정 */
                padding-top: 25px;
                background-color: #333;
              }
              /* aside navigation */
              aside > ul {
                width: 200px;
              }
              aside > ul > li > a {
                display: block;
                color: #fff;
                padding: 10px 0 10px 20px;
              }
              aside > ul > li > a.active {
                background-color: #4CAF50;
              }
              aside > ul > li > a:hover:not(.active) {
                background-color: #555;
              }
              aside > h1 {
                padding: 20px 0 20px 20px;
                color: #fff;
              }
              /* Section */
              section {
                float: right;
                margin-left: 200px;  /*aside width*/
              }
              article {
                width: 48.5%;
                margin: 1%;
                padding: 25px;
                background-color: white;
                float: left;
              }
              article:nth-of-type(2n) {
                margin-left: 0;
              }
              article:nth-of-type(n+3) {
                margin-top: 0;
              }
              /* footer */
              footer {
                /* footer를 aside위에 올리기 위해 사용(부유객체) */
                position: absolute;
                height: 60px;
                width: 100%;
                padding: 0 25px;
                line-height: 60px;
                color: #8a8c8f;
                border-top: 1px solid #dee5e7;
                background-color: #f2f2f2;
              }
        
              .nav-toggle {
                display: none;
              }
              .navicon {
                display: none;
              }
        
              /* Media Query */
              /* for tablet: ~ 800px */
              @media screen and (max-width: 800px) {
                header {
                  height: 120px;
                  text-align: center;
                }
                nav {
                  float: none;
                  margin-right: 0;
                }
                #wrap {
                  /* margin-top = header height */
                  margin-top: 120px;
                }
                aside {
                  top: 120px;
                }
        
                article {
                  width: inherit;
                  display: block;
                  margin: 10px;
                  float: none;
                }
                article:nth-of-type(2n) {
                  margin: 10px;
                }
                article:nth-of-type(n+2) {
                  margin-top: 0;
                }
              }
              /* for smartphone: ~ 480px */
              @media screen and (max-width: 480px) {
                header {
                  height: 60px;
                }
                .nav-items {
                  display: none;
                }
                .navicon {
                  display: block;
                }
                #wrap {
                  /* margin-top = header height */
                  margin-top: 60px;
                }
                aside {
                  top: 60px;
                  position: static;
                  width: 100%;
                  padding: 5px 0;
                }
                /* aside navigation */
                aside > ul {
                  width: 100%;
                }
                aside > h1 {
                  padding: 5px 0 10px 20px;
                  color: #fff;
                }
                section {
                  float: none;
                  margin-left: 0;
                }
                /* View navigation item */
                .nav-toggle:checked ~ .nav-items {
                  display: block;
                  width: 100%;
                  background-color: #fff;
                  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
                }
                .nav-items > li  {
                  display: block;
                }
                .nav-items > li > a {
                  line-height: 50px;
                }
              }
            </style>
          </head>
          <body>
            <div id="wrap">
              <header>
                <a class="logo" href="#home"><img src="https://poiemaweb.com/img/logo.png"></a>
                <nav>
                  <input class="nav-toggle" id="nav-toggle" type="checkbox">
                  <label class="navicon" for="nav-toggle"><span class="navicon-bar"></span></label>
                  <ul class="nav-items">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#news">News</a></li>
                    <li><a href="#contact">Contact</a></li>
                    <li><a href="#about">About</a></li>
                  </ul>
                </nav>
              </header>
        
              <div id="content-wrap">
                <aside>
                  <h1>Aside</h1>
                  <ul>
                    <li><a href="#" class="active">London</a></li>
                    <li><a href="#">Paris</a></li>
                    <li><a href="#">Tokyo</a></li>
                    <li><a href="#">Newyork</a></li>
                  </ul>
                </aside>
                <section>
                  <article id="london">
                    <h1>London</h1>
                    <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
                    <p>Standing on the River Thames, London has been a major settlement for two millennia,its history going back to its founding by the Romans, who named it Londinium.</p>
                    <p>London, also referred to as Greater London, is one of 9 regions of England and the top-level subdivision covering most of the city's metropolis. The small ancient City of London at its core once comprised the whole settlement, but as its urban area grew, the Corporation of London resisted attempts to amalgamate the city with its suburbs, causing "London" to be defined in a number ways for different purposes.</p>
                  </article>
                  <article id="paris">
                    <h1>Paris</h1>
                    <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
                    <p>Standing on the River Thames, London has been a major settlement for two millennia,its history going back to its founding by the Romans, who named it Londinium.</p>
                    <p>London, also referred to as Greater London, is one of 9 regions of England and the top-level subdivision covering most of the city's metropolis. The small ancient City of London at its core once comprised the whole settlement, but as its urban area grew, the Corporation of London resisted attempts to amalgamate the city with its suburbs, causing "London" to be defined in a number ways for different purposes.</p>
                  </article>
                  <article id="tokyo">
                    <h1>Tokyo</h1>
                    <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
                    <p>Standing on the River Thames, London has been a major settlement for two millennia,its history going back to its founding by the Romans, who named it Londinium.</p>
                    <p>London, also referred to as Greater London, is one of 9 regions of England and the top-level subdivision covering most of the city's metropolis. The small ancient City of London at its core once comprised the whole settlement, but as its urban area grew, the Corporation of London resisted attempts to amalgamate the city with its suburbs, causing "London" to be defined in a number ways for different purposes.</p>
                  </article>
                  <article id="newyork">
                    <h1>Newyork</h1>
                    <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
                    <p>Standing on the River Thames, London has been a major settlement for two millennia,its history going back to its founding by the Romans, who named it Londinium.</p>
                    <p>London, also referred to as Greater London, is one of 9 regions of England and the top-level subdivision covering most of the city's metropolis. The small ancient City of London at its core once comprised the whole settlement, but as its urban area grew, the Corporation of London resisted attempts to amalgamate the city with its suburbs, causing "London" to be defined in a number ways for different purposes.</p>
                  </article>
                </section>
                <!-- end of content-wrap -->
              </div>
              <footer>© Copyright 2016 ungmo2</footer>
            <!-- end of wrap   -->
            </div>
          </body>
        </html>
        ```