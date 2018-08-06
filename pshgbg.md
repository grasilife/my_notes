# transition和animation

transition为过度效果,animation为持续干某件事
```css
.th_color {
  background: $background_table;
  color: $table_color;
  transition: background 0.5s;
  -moz-transition: background 0.5s;
  -webkit-transition: background 0.5s;
  -o-transition: background 0.5s;
}

.th_color_false {
  background: $background3;
  color: $table_color;
  transition: background 0.5s;
  -moz-transition: background 0.5s;
  -webkit-transition: background 0.5s;
  -o-transition: background 0.5s;
}
```
只发生一次
```plain
@keyframes mymove
{
from {top:0px;}
to {top:200px;}
}
div
{
width:100px;
height:100px;
background:red;
position:relative;
animation:mymove 3s;
}
```
持续变化
