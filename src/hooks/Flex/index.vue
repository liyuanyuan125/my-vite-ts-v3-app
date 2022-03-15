<template>
  <div class="pictures-adaptive">
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
    <div class="wrap"><img src="../../assets/girl.jpeg"  /></div>
  </div>
</template>

<script lang="ts">
/**
 * 情况1 一张图，完整展示整张图
 * 情况2 2-3图，无法展示完整，一排最多3张
 * 情况3 4张图，无法完整展示，每排2张，共2排
 * 情况4 5-9图，无法展示完整，一排最多3张
 */
</script>

<style scoped>
.pictures-adaptive {
  display: flex;
  flex-wrap: wrap;
  width: 600px;
  margin: 0 auto;
}
/* 相对定位，img相对于.wrap相对定位 */
.wrap {
  position: relative;
  overflow: hidden;
  margin-bottom: 2%;
}

/* 大于1张图片时，img标签的样式 */
.wrap:not(:nth-child(1):nth-last-child(1)) img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/*  2张图片  */
.wrap:nth-child(1):nth-last-child(2),
.wrap:nth-child(2):nth-last-child(1),
/*  4张图片  */
.wrap:nth-child(1):nth-last-child(4),
.wrap:nth-child(2):nth-last-child(3),
.wrap:nth-child(3):nth-last-child(2),
.wrap:nth-child(4):nth-last-child(1)
{
  width: 49%;
  padding-bottom: 49%;
}
/* 每行的两张图片中间间隔2%的宽度 */
/*  2张图片  */
.wrap:nth-child(2):nth-last-child(1),
/*  4张图片  */
.wrap:nth-child(2):nth-last-child(3),
.wrap:nth-child(4):nth-last-child(1)
{
  margin-left: 2%;
}

/*  3张图片  */
.wrap:nth-child(1):nth-last-child(3),
.wrap:nth-child(2):nth-last-child(2),
.wrap:nth-child(3):nth-last-child(1) 
{
  width: 32%;
  padding-bottom: 32%;
}

/*  间隔  */
.wrap:nth-child(2):nth-last-child(2),
.wrap:nth-child(3):nth-last-child(1) 
{
  margin-left: 2%;
}


/*  5张以上图片  */
.wrap:nth-child(n + 5),
.wrap:nth-child(1):nth-last-child(n + 5),
.wrap:nth-child(1):nth-last-child(n + 5) ~ .wrap
{
  width: 32%;
  padding-bottom: 32%;
}

/*  间隔  */
.wrap:nth-child(n + 5):not(:nth-child(3n + 1)),
.wrap:nth-child(1):nth-last-child(n + 5) ~ .wrap:not(:nth-child(3n + 1))
{
  margin-left: 2%;
}

</style>
