# 코드 스타일 가이드

### Dimension

TextSize(sp)

> _[글자크기]

시스템 폰트크기에 영향을 받지 않도록 dp로 정의해서 사용

```
<dimen name="_10sp">10dp</dimen>
<dimen name="_15sp">15dp</dimen>
<dimen name="_20sp">20dp</dimen>
<dimen name="_30sp">30dp</dimen>
```



### String

> [사용하는곳]_[설명]

* all_confirm : 확인
* all_cancel : 취소
* dialog_check_no_show : 다시 보지 않음
* edittext_hint_please_input_new_password : 새 비밀번호를 입력하세요.



### Layout

> [View]_[설명]

| Prefix | 사용                             |
| ------ | -------------------------------- |
| a_     | Activity용 layout                |
| f_     | fragment용 layout                |
| vh_    | RecyclerView Viewholder용 layout |
| i_     | include용 layout                 |
| d_     | dialog용 layout                  |
| v_     | customView용 layout              |



#### 사용 예

* a_main : MainActivity용 layout
* f_home : HomeFragment용 layout
* vh_rolling_banner : ViewHolder의 Rolling Banner용 layout
* i_divider : 아이템 구분 Divider용 layout
* d_exit_confirm : 뒤로 가기시 나갈건지 다시 물어보는 Dialog용 layout
* v_rating_star : 평점 별표시 관련 CustomView

### ID (in xml Layout)

> [View]_[설명]

* 대문자를 축약한 형태
  * TextView -> tv, ImageView -> iv, ConstraintLayout -> cl
* 대문자가 1개일 경우 전부 소문자로
  * Switch -> switch
* CustomView의 경우 알아보기 쉽게 전부 소문자로
  * MyCustomView -> my_custom_view

| View             | Prefix         |
| ---------------- | -------------- |
| ConstraintLayout | cl_            |
| RecyclerView     | rv_            |
| ImageView        | iv_            |
| TextView         | tv_            |
| Switch           | switch_        |
| LinearLayout     | ll_            |
| MyCutsomView     | my_custom_view |
| Chip             | chip_          |

