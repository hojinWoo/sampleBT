# bootstrap template 적용 방법

`$ rails new sampletemplate`

- rails : 4.2.10
- ruby : 2.3.5



### index

`$ rails g controller temp` controller 만들기

```ruby
# controller index(action)
class TempController < ApplicationController
  def index
  end
end
```

```ruby
# config/routes.rb
root 'temp#index'
get 'temp/index' => 'temp#index'
```

> index.html을 index.html.erb에 붙여 넣기



##### css file은 절대경로로 불러올 수 없기 때문에 파일을 옮겨서 생성해줘야 한다. (bootstrap style 경로를 옮긴다)

##### ex) stylesheets/responsive.css →  vendor/assets/stylesheets 밑에다가 옮겨주기.

```css
/* app/assets/stylesheets/application.css인데 파일 이름을
@import를 쓰기 위해 application.scss로 변경*/

/*기존에 있던 line 지우기*/
*= require_tree .
*= require_self

/*index 대신 붙일 때 index.html에 써져 있던 순서대로 써야 한다. 순서 지키기!!*/
@import 'responsive';
```

> 기존 index.html에 있던 css 주석 처리 하기
>
> <head> tag 내용은 `app/views/layouts/application.html.erb`로 옮기기
>
> <body> tag만 지우기(안에 내용이 아닌 tag자체만)



JS코드도 `index.html.erb`에 최하단에 있는 코드들을 `app/assets/javascripts/application.js`에 복붙하고

```javascript
//= require_tree . 지우기

//<script type="text/javascript" src="javascript/ 을
//= require        로 바꾸기

//cf) 만약 CND이 있다면
<script type="text/javascript" src="https://maps.googleapis.com/maps/api/js?key=KEY&region=GB"/>
// app/views/layouts/application.html.erb의 <body> 밑으로 옮기기
```

> javascripts 에 있는 필요한 js 파일들을→  `vendor/assets/javascripts`밑에다가 옮겨주기.



Image는 `app/assets/images`로 옮기기

```erb
<!--파일 경로를 직접 작성하거나 이렇게 쓰면 된다. -->
<img src="<%=asset_path '01.png'%>" alt="">

<!-- 백그라운드 이미지인 경우 -->
.flat-iconbox.style2{
	...
	backgroud-image: url(asset-path('02.png'));
}
```



cf) Atom에서 `ctrl+shift+f`로 전체 파일에서 검색이 가능하다.

cf) erb코드에서 javascript부분 중 나중에 실행시켜야 하는 경우

```javascript
// ex. app/views/controller/index.html.erb
//단순 코드가 아니라 js 코드가 써져 있는 경우//
<% content_for 'javascripts_contents' do %>
	<script type = "text/javascript">
        ...
    	...
    </script>
<% end %>
```

```erb
<!-- app/views/layouts/application.html.erb -->
<%= yield 'javascript_contents' %>
```
