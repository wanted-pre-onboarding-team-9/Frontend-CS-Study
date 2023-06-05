# Flex

> **Flex(Flexible)**  
> 잘 구부러지는, 유연한

Flexbox로 레이아웃을 구성한다는 것은 박스를 유연하게 늘리거나 줄여서 레이아웃을 잡는 것을 의미하며, 요소의 사이즈가 불명확하거나 동적으로 변화할 때에도 유연한 레이아웃을 실현할 수 있다는 장점을 가집니다.

## display: flex

Flex는 부모 요소(flex-container)와 자식 요소(flex-item)로 구성됩니다. 부모 요소에  `disflay:flex` 속성을 지정하면 Flex의 속성들을 사용할 수 있습니다. Flex의 속성은 부모 요소에 적용하는 것과, 자식 요소에 적용하는 속성으로 나뉩니다.

## 부모 요소에 적용하는 Flex 속성

### flex-direction: 정렬 축 설정

```
.container {
  flex-direction: row; // 가로 정렬(기본값 )
  flex-direction: row-reverse;
  flex-direction: column; // 세로 정렬
  flex-direction: column-reverse;
}
```

### flex-wrap: 줄 바꿈 설정

하위 요소들의 크기가 상위 요소의 크기를 넘으면 자동을 줄을 바꿀 것인지 정하는 속성입니다.  설정하지 않으면 줄 바꿈을 하지 않습니다.

```
.container {
  flex-wrap: nowrap; // 줄바꿈을 하지 않고 빠져나감 (기본값)
  flex-wrap: wrap;
  flex-wrap: wrap-reverse; // 줄바꿈 + 아이템 역순 배치
}
```

### justify-content: 축 수평 방향 정렬

축과 수평 방향으로 어떻게 정렬할 것인지 정하는 속성입니다. 요소들이 가로로 정렬되어 있으면 가로 방향으로 어떻게 정렬할지, 세로로 정렬되어 있으면 세로 방향으로 어떻게 정렬할 것인지 정합니다.

```
.container {
  justify-content: flex-start; // 시작점으로 정렬(row(가로)인 경우 왼쪽, column(세로)인 경우 위쪽)
  justify-content: flex-end; // 아이템들을 끝점으로 정렬
  justify-content: center; // 가운데 정렬
  justify-content: space-between; // 아이템들 사이에 균일한 간격을 만들어줌(첫번째, 마지막 아이템은
  justify-content: space-around; // 아이템들 둘레에 균일한 간격을 만들어줌
  justify-content: space-evenly; // 아이템 사이와 양 끝에 균일한 간격을 만들어줌
}
```

![image](https://github.com/sena-22/untitled/assets/110877564/d0fce97d-1649-4860-b85d-0d9a8c186718)

[출처](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#aa-justify-content")

### align-items: 수직 축 방향 정렬

요소를 축의 수직 방향으로 어떻게 정렬할지 정하는 속성입니다.

```
.container {
	align-items: stretch; // 수직축 방향으로 늘리는 속성(기본값)
	align-items: flex-start; // 시작점
	align-items: flex-end; // 끝점
	align-items: center; // 가운데
	align-items: baseline; // 텍스트 베이스라인 기준으로 정렬
}
```

![image](https://github.com/sena-22/untitled/assets/110877564/4faa9f8a-d0cf-4f03-89af-a80b3e5863fc)

## 자식 요소에 적용하는 Flex 속성

> flex: <grow(팽창 지수)> <shrink(수축 지수)> <basis(기본 크기)>

**기본값**

```
flex: 0 1 auto; // 순서대로 grow shrink basis를 나타냅니다.
```

### flex-grow(팽창 지수)

요소의 크기가 얼마나 늘어날 것인지를 의미하는 속성입니다. 여러 자식 요소가 있을 때 남는 공간을 자식들이 어느 비율로 차지할 지 정할 수 있습니다.  **자식 요소의** **grow 값 / 자식 요소들의 grow 값의 총합**의 비율로 빈 공간을 가져갑니다.

```
<main>
  <div id="box1" class="box">box1</div> // flex-grow: 6
  <div id="box2" class="box">box2</div> // flex-grow: 3
  <div id="box3" class="box">box3</div> // flex-grow: 1
</main>
```

위의 예시에서 box1은 box1의 grow 6 / grow의 총합 6 + 3 +1  = 3/5만큼의 공간을 차지합니다.

### flex-shring(수축 지수)

grow와 반대로 요소의 크기가 설정한 비율만큼 작아지는 속성입니다. 0으로 설정하면 flex-basis보다 작아지지 않아서 고정폭을 만들 수 있습니다.

```
.flex-item {
  flex-shrink: 0;
  width: 100px;
}
```

### flex-basis(기본 크기)

아이템의 기본 크기를 설정합니다. flex-direction이 row일 때는 너비, column일 때는 높이를 설정합니다.

```
.flex-item {
  flex-basis: auto | <width>;
}
```

# Grid

Grid는 2차원 레이아웃 시스템으로, Flex보다 복잡한 레이아웃을 표현할 수 있습니다.

## Grid의 주요 용어

### Grid Container

display:grid;를 적용하는 Grid의 전체 영역을 의미합니다.

### Grid Item

Grid Container의 자식 요소들을 가리킵니다. 여기서 자식은 직계 자식만을 의미하므로, Item의 자식 요소는 제외됩니다.

### Grid Line

Grid 구조를 이루는 분할선입니다. 행 또는 열의 양쪽에 위치합니다.

### Grid Cell

Grid의 한 칸을 가리킵니다. Grid Cell 안에 실제 <div>와 같은 아이템이 들어가게 됩니다.

### Grid Track

Grid의 행 또는 열을 가리킵니다.

## display: grid

Grid는 Flex와 마찬가지로 부모 요소에 `display: grid;`를 설정하여 사용하고, 부모 요소인 컨테이너와 자식 요소인 아이템에 각각의 속성을 설정할 수 있습니다.

## 부모 요소에 적용하는 Grid 속성

### grid-template-rows, grid-template-columns: 그리드의 형태 정의

Grid Track의 크기를 지정하는 속성입니다. 여러 단위로 사용이 가능합니다.

```
.container {
	grid-template-columns: 200px 200px 500px;
	grid-template-columns: 1fr 1fr 1fr // 1:1:1로 3개의 column 생성
	grid-template-columns: repeat(3, 1fr) // 1fr 3번 반복
    // auto-fill: 개수를 미리 정하지 않고 너비가 허용되는 한 셀을 최대로 채움
    // minmax: 최소값, 최대값 지정
    grid-template-columns: repeat(auto-fill, minmax(20%, auto));

	grid-template-rows: 200px 200px 500px;
	grid-template-rows: 1fr 1fr 1fr
	grid-template-rows: repeat(3, 1fr)
}
```

### row-gap, column-gap, gap: 간격 생성

Grid Cell 사이의 간격을 지정하는 속성입니다.

```
row-gap: 10px; // row 간격 10px
column-gap: 10px; // column 간격 10px
gap: 10px; // row와 column의 간격
gep: 10px 20px; // row의 간격, column의 간격
```

### grid-auto-columns, grid-auto-rows: 간격 생성

grid-template-columns 또는 grid-template-rows로 설정되지 않은 트랙의 크기를 지정하는 속성입니다.

```
.container {
	grid-auto-rows: minmax(100px, auto);
}
```

### grid-template-areas: 이름으로 Grid 정의

```
#page {
 grid-template-areas:
    "head head"
    "nav  main"
    "nav  foot";
}

#page > header {
  grid-area: head;
  background-color: #8ca0ff;
}
```

## 자식 요소에 적용하는 Grid 속성

### grid-column-start, grid-column-end, grid-column, grid-row-start, grid-row-end, grid-row: 각 셀의 영역 지정

```
.item:nth-child(1) {
	grid-column-start: 1;
	grid-column-end: 3;
	grid-row-start: 1;
	grid-row-end: 2;
}

.item:nth-child(1) {
	grid-column: 1 / 3;
	grid-row: 1 / 2;
}
```

# Flex와 Grid의 차이점

Flex는 한 방향 레이아웃이기 때문에 수평, 혹은 수직으로만 나눌 수 있고,  Grid는 두 방향 레이아웃이어서 수평, 수직을 동시에 나눌 수 있습니다.

## wrap

![image](https://github.com/sena-22/untitled/assets/110877564/f4ed4ff6-3474-41ca-92b8-c83d2cda824d) <br/>
[출처](https://css-tricks.com/quick-whats-the-difference-between-flexbox-and-grid/)<br/>

Flex의 경우 선택적으로 래핑이 가능합니다. flex에서 wrapping을 허용하면 요소들이 한 줄을 채우면 다음 줄로 넘어가게 됩니다. 다음 줄에서 일어나는 정렬은 이전 줄과 무관하고, 따라서 벽돌처럼 보이는 레이아웃을 구현할 수 있습니다.

Gird는 래핑을 하더라도 다음 줄로 넘어간 요소도 같은 그리드 라인을 따라 배치됩니다.

```
[1] [2] [3]
[4] [5]
[6]
```

![image](https://github.com/sena-22/untitled/assets/110877564/59d63241-93f3-4d11-adce-3bc2f9125649) <br/>
[출처](https://css-tricks.com/quick-whats-the-difference-between-flexbox-and-grid/) <br>

Flex는 요소가 끝나는 위치를 정할 수 없습니다. 하지만 Grid는 행과 열의 크기를 선언한 후에 모두 명시적으로 배치가 가능합니다.

## Overlapping

요소를 중첩시킬 때 Flex는 마진을 음수로 두거나 absolute 같은 다른 속성들을 사용해야 하지만, Grid는 요소를 같은 그리드 셀에 배치하고 z-index를 통해 중첩이 가능합니다.

> Flex는 가로 혹은 세로만 고려하면 되는 소규모 레이아웃에 적합하고,  
> Grid는 가로와 세로를 모두 고려해야 하는 대규모 레이아웃에 적합합니다.

flex와 grid를 이용하여 화면 크기에 따른 요소 이동을 간단하게 구현해보았습니다.
grid의 경우 `grid-template-columns` 속성을 `repeat(auto-fit, minmax(200px, 1fr))`로 설정하면 최소값이 200px이고 남은 공간은 1fr을 통해 공평하게 분할합니다.
flex의 경우 `flex-basis`를 `200px`으로 설정하고 `flex-wrap` 속성을 사용하여 공간이 모자라면 밑으로 내려가게 됩니다.[여기](https://codesandbox.io/s/grid-flex-responsive-84bg34?file=/src/styles.css:296-314)에서 적용한 모습을 확인할 수 있습니다.
(`flex-grow`속성은 한 줄에서 차지하는 크기를 조절하는 것이기 때문에 자동으로 줄바꿈이 되게 하려면`flex-wrap` 속성을 사용해야 합니다.)

> **Flex와 Grid를 시각적으로 학습해볼 수 있는 곳**  
> [🐸 FLEXBOX FROGGY](https://flexboxfroggy.com/#ko)  
> [🪴 GRID GARDEN](https://cssgridgarden.com/#ko)

> **참고자료**  
> [Relationship of grid layout to other layout methods](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_grid_layout/Relationship_of_grid_layout_with_other_layout_methods)  
> [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)  
> [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)  
> [Quick! What’s the Difference Between Flexbox and Grid?](https://css-tricks.com/quick-whats-the-difference-between-flexbox-and-grid/)  
> [이번에야말로 CSS Grid를 익혀보자](https://studiomeal.com/archives/533)  
> [이번에야말로 CSS Flex를 익혀보자](https://studiomeal.com/archives/197)  
> [PoiemaWeb CSS3 Flexbox Layout](https://poiemaweb.com/css3-flexbox)
