### Flex布局
   **容器的属性**
   
    

1. flex-direction(主轴方向)：

    + row
    + row-reverse
    + column
    + column-reverse
 
+     flex-wrap(换行):
    + nowrap
    + wrap
    + wrap-reverse

+ flex wrap(以上两个属性的结合)
+ justify-content(主轴上的对齐方式)
    + flex-start
    + flex-end
    + center
    + space-between
    + space-around
+ align-items(交叉轴)
    + flex-start
    + flex-end
    + center
    + stretch
    + baseline
+ align-content(多根轴线对齐)
    + flex-start
    + flex-end
    + center
    + space-between
    + space-around
    + stretch

**项目的属性**

1. order排列顺序
2. flex-grow放大比例，默认为零、
3. flex-shrink缩小比例，负值无效，默认为1
4. flex-basis分配多余空间时占据的主轴空间，默认auto
5. flex(上面三个值的综合)
6. align-self(覆盖align-items)
    


----------
### Grid布局

**容器属性**

1. grid-template-columns 50% 50% 或 repeat（2，50%）或1fr 1fr
2. grid-template-rows
3. grid-template(前面rows/后面columns)


**项目属性**

1. grid-column-start
2. grid-column-end:4=>到第四行线,并非第四格
3. grid-row-start
4. grid-row-end
5. grid-column
6. grid-row
7. grid-area(rowstart/columnstart/rowend/columnend)
