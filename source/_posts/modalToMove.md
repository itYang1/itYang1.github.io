---
title: 弹窗可拖拽弹窗
tags:
  - vue
  - css
  - 弹窗
description: 以vue为框架创建的弹窗，可以进行拖拽和调整大小
cover: /image/moveTo.gif
abbrlink: 652fa2ca
---

```
<template>
  <div id="drag">
    <div class="title">
      <h2>这是一个可以拖动的窗口</h2>
      <div>
        <a class="min" href="javascript:;" title="最小化"></a>
        <a class="max" href="javascript:;" title="最大化"></a>
        <a class="revert" href="javascript:;" title="还原"></a>
        <a class="close" href="javascript:;" title="关闭"></a>
      </div>
    </div>
    <div class="resizeL"></div>
    <div class="resizeT"></div>
    <div class="resizeR"></div>
    <div class="resizeB"></div>
    <div class="resizeLT"></div>
    <div class="resizeTR"></div>
    <div class="resizeBR"></div>
    <div class="resizeLB"></div>
    <div class="content">
      ① 窗口可以拖动；<br />
      ② 窗口可以通过八个方向改变大小；<br />
      ③ 窗口可以最小化、最大化、还原、关闭；<br />
      ④ 限制窗口最小宽度/高度。
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      dragMinWidth: 250,
      dragMinHeight: 125,
      get: {
        byId: (id) => {
          return typeof id === "string" ? document.getElementById(id) : id;
        },
        byClass: (sClass, oParent) => {
          var aClass = [];
          var reClass = new RegExp("(^| )" + sClass + "( |$)");
          var aElem = this.get.byTagName("*", oParent);
          for (var i = 0; i < aElem.length; i++)
            reClass.test(aElem[i].className) && aClass.push(aElem[i]);
          return aClass;
        },
        byTagName: (elem, obj) => {
          return (obj || document).getElementsByTagName(elem);
        },
      },
    };
  },

  mounted() {
    const that = this;
    window.onload = () => {
      that.init();
    };
    window.onresize = () => {
      that.init();
    };
  },

  methods: {
    init() {
      let oDrag = document.getElementById("drag");
      console.log("1---------------", oDrag);

      let oTitle = this.get.byClass("title", oDrag)[0];
      let oL = this.get.byClass("resizeL", oDrag)[0];
      let oT = this.get.byClass("resizeT", oDrag)[0];
      let oR = this.get.byClass("resizeR", oDrag)[0];
      let oB = this.get.byClass("resizeB", oDrag)[0];
      let oLT = this.get.byClass("resizeLT", oDrag)[0];
      let oTR = this.get.byClass("resizeTR", oDrag)[0];
      let oBR = this.get.byClass("resizeBR", oDrag)[0];
      let oLB = this.get.byClass("resizeLB", oDrag)[0];
      this.drag(oDrag, oTitle);
      //四角
      this.resize(oDrag, oLT, true, true, false, false);
      this.resize(oDrag, oTR, false, true, false, false);
      this.resize(oDrag, oBR, false, false, false, false);
      this.resize(oDrag, oLB, true, false, false, false);
      //四边
      this.resize(oDrag, oL, true, false, false, true);
      this.resize(oDrag, oT, false, true, true, false);
      this.resize(oDrag, oR, false, false, false, true);
      this.resize(oDrag, oB, false, false, true, false);
      oDrag.style.left =
        (document.documentElement.clientWidth - oDrag.offsetWidth) / 2 + "px";
      oDrag.style.top =
        (document.documentElement.clientHeight - oDrag.offsetHeight) / 2 + "px";
    },

    drag(oDrag, handle) {
      let disX = 0;
      let disY = 0;
      let oMin = this.get.byClass("min", oDrag)[0];
      let oMax = this.get.byClass("max", oDrag)[0];
      let oRevert = this.get.byClass("revert", oDrag)[0];
      let oClose = this.get.byClass("close", oDrag)[0];
      handle = handle || oDrag;
      handle.style.cursor = "move";
      handle.onmousedown = (event) => {
        disX = event.clientX - oDrag.offsetLeft;
        disY = event.clientY - oDrag.offsetTop;
        document.onmousemove = (event) => {
          var iL = event.clientX - disX;
          var iT = event.clientY - disY;
          var maxL = document.documentElement.clientWidth - oDrag.offsetWidth;
          var maxT = document.documentElement.clientHeight - oDrag.offsetHeight;
          iL <= 0 && (iL = 0);
          iT <= 0 && (iT = 0);
          iL >= maxL && (iL = maxL);
          iT >= maxT && (iT = maxT);
          oDrag.style.left = iL + "px";
          oDrag.style.top = iT + "px";
          return false;
        };
        document.onmouseup = () => {
          document.onmousemove = null;
          document.onmouseup = null;
          this.releaseCapture && this.releaseCapture();
        };
        this.setCapture && this.setCapture();
        return false;
      };
      //最大化按钮
      oMax.onclick = () => {
        oDrag.style.top = oDrag.style.left = 0;
        oDrag.style.width = document.documentElement.clientWidth - 2 + "px";
        oDrag.style.height = document.documentElement.clientHeight - 2 + "px";
        this.style.display = "none";
        oRevert.style.display = "block";
      };
      //还原按钮
      oRevert.onclick = () => {
        oDrag.style.width = this.dragMinWidth + "px";
        oDrag.style.height = this.dragMinHeight + "px";
        oDrag.style.left =
          (document.documentElement.clientWidth - oDrag.offsetWidth) / 2 + "px";
        oDrag.style.top =
          (document.documentElement.clientHeight - oDrag.offsetHeight) / 2 +
          "px";
        this.style.display = "none";
        oMax.style.display = "block";
      };
      //最小化按钮
      oMin.onclick = oClose.onclick = () => {
        oDrag.style.display = "none";
        var oA = document.createElement("a");
        oA.className = "open";
        oA.href = "javascript:;";
        oA.title = "还原";
        document.body.appendChild(oA);
        oA.onclick = () => {
          oDrag.style.display = "block";
          document.body.removeChild(this);
          this.onclick = null;
        };
      };
      //阻止冒泡
      oMin.onmousedown =
        oMax.onmousedown =
        oClose.onmousedown =
          (event) => {
            this.onfocus = () => {
              this.blur();
            };
            (event || window.event).cancelBubble = true;
          };
    },

    resize(oParent, handle, isLeft, isTop, lockX, lockY) {
      handle.onmousedown = (event) => {
        var disX = event.clientX - handle.offsetLeft;
        var disY = event.clientY - handle.offsetTop;
        var iParentTop = oParent.offsetTop;
        var iParentLeft = oParent.offsetLeft;
        var iParentWidth = oParent.offsetWidth;
        var iParentHeight = oParent.offsetHeight;
        document.onmousemove = (event) => {
          var iL = event.clientX - disX;
          var iT = event.clientY - disY;
          var maxW =
            document.documentElement.clientWidth - oParent.offsetLeft - 2;
          var maxH =
            document.documentElement.clientHeight - oParent.offsetTop - 2;
          var iW = isLeft ? iParentWidth - iL : handle.offsetWidth + iL;
          var iH = isTop ? iParentHeight - iT : handle.offsetHeight + iT;
          isLeft && (oParent.style.left = iParentLeft + iL + "px");
          isTop && (oParent.style.top = iParentTop + iT + "px");
          iW < this.dragMinWidth && (iW = this.dragMinWidth);
          iW > maxW && (iW = maxW);
          lockX || (oParent.style.width = iW + "px");
          iH < this.dragMinHeight && (iH = this.dragMinHeight);
          iH > maxH && (iH = maxH);
          lockY || (oParent.style.height = iH + "px");
          if (
            (isLeft && iW == this.dragMinWidth) ||
            (isTop && iH == this.dragMinHeight)
          )
            document.onmousemove = null;
          return false;
        };
        document.onmouseup = () => {
          document.onmousemove = null;
          document.onmouseup = null;
        };
        return false;
      };
    },
  },
};
</script>

<style>
body,
div,
h2 {
  margin: 0;
  padding: 0;
}
body {
  background: url(/src/static/image/meiTu.png);
  color: #333;
}
#drag {
  position: absolute;
  top: 100px;
  left: 100px;
  width: 300px;
  height: 160px;
  background: #e9e9e9;
  border: 1px solid #444;
  border-radius: 5px;
  box-shadow: 0 1px 3px 2px #666;
}
#drag .title {
  position: relative;
  height: 27px;
  margin: 5px;
}
#drag .title h2 {
  font-size: 14px;
  height: 27px;
  line-height: 24px;
  border-bottom: 1px solid #a1b4b0;
}
#drag .title div {
  position: absolute;
  height: 19px;
  top: 2px;
  right: 0;
}
#drag .title a,
a.open {
  float: left;
  width: 21px;
  height: 19px;
  display: block;
  margin-left: 5px;
  background: url(/src/static/image/关闭.png) no-repeat;
}
a.open {
  position: absolute;
  top: 10px;
  left: 50%;
  margin-left: -10px;
  background-position: 0 0;
}
a.open:hover {
  background-position: 0 -29px;
}
#drag .title a.min {
  background-position: -29px 0;
}
#drag .title a.min:hover {
  background-position: -29px -29px;
}
#drag .title a.max {
  background-position: -60px 0;
}
#drag .title a.max:hover {
  background-position: -60px -29px;
}
#drag .title a.revert {
  background-position: -149px 0;
  display: none;
}
#drag .title a.revert:hover {
  background-position: -149px -29px;
}
#drag .title a.close {
  background-position: -89px 0;
}
#drag .title a.close:hover {
  background-position: -89px -29px;
}
#drag .content {
  overflow: auto;
  margin: 0 5px;
}
#drag .resizeBR {
  position: absolute;
  width: 14px;
  height: 14px;
  right: 0;
  bottom: 0;
  overflow: hidden;
  cursor: nw-resize;
  /* background: url(/src/static/image/横线.png) no-repeat;
  background-size: 20px 20px; */
}
#drag .resizeL,
#drag .resizeT,
#drag .resizeR,
#drag .resizeB,
#drag .resizeLT,
#drag .resizeTR,
#drag .resizeLB {
  position: absolute;
  background: #000;
  overflow: hidden;
  opacity: 0;
  filter: alpha(opacity=0);
}
#drag .resizeL,
#drag .resizeR {
  top: 0;
  width: 5px;
  height: 100%;
  cursor: w-resize;
}
#drag .resizeR {
  right: 0;
}
#drag .resizeT,
#drag .resizeB {
  width: 100%;
  height: 5px;
  cursor: n-resize;
}
#drag .resizeT {
  top: 0;
}
#drag .resizeB {
  bottom: 0;
}
#drag .resizeLT,
#drag .resizeTR,
#drag .resizeLB {
  width: 8px;
  height: 8px;
  background: #ff0;
}
#drag .resizeLT {
  top: 0;
  left: 0;
  cursor: nw-resize;
}
#drag .resizeTR {
  top: 0;
  right: 0;
  cursor: ne-resize;
}
#drag .resizeLB {
  left: 0;
  bottom: 0;
  cursor: ne-resize;
}
</style>

```
借鉴：https://www.cnblogs.com/limeiky/p/5818474.html