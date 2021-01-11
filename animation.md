## 烟花追随 动画

> sketch_min.js
```js
var Sketch = function () {
    "use strict";


    function e(e) {
        return "[object Array]" == Object.prototype.toString.call(e)
    }


    function t(e) {
        return "function" == typeof e
    }


    function n(e) {
        return "number" == typeof e
    }


    function o(e) {
        return "string" == typeof e
    }


    function r(e) {
        return E[e] || String.fromCharCode(e)
    }


    function i(e, t, n) {
        for (var o in t)(n || !e.hasOwnProperty(o)) && (e[o] = t[o]);
        return e
    }


    function u(e, t) {
        return function () {
            e.apply(t, arguments)
        }
    }


    function a(e) {
        var n = {};
        for (var o in e) n[o] = t(e[o]) ? u(e[o], e) : e[o];
        return n
    }


    function c(e) {
        function n(n) {
            t(n) && n.apply(e, [].splice.call(arguments, 1))
        }


        function u(e) {
            for (_ = 0; _ < J.length; _++) G = J[_], o(G) ? O[(e ? "add" : "remove") + "EventListener"].call(O, G, k, !1) : t(G) ? k = G : O = G
        }


        function c() {
            L(T), T = I(c), U || (n(e.setup), U = t(e.setup), n(e.resize)), e.running && !j && (e.dt = (B = +new Date) - e.now, e.millis += e.dt, e.now = B, n(e.update), e.autoclear && K && e.clear(), n(e.draw)), j = ++j % e.interval
        }


        function l() {
            O = Y ? e.style : e.canvas, D = Y ? "px" : "", e.fullscreen && (e.height = w.innerHeight, e.width = w.innerWidth), O.height = e.height + D, O.width = e.width + D, e.retina && K && X && (O.height = e.height * X, O.width = e.width * X, O.style.height = e.height + "px", O.style.width = e.width + "px", e.scale(X, X)), U && n(e.resize)
        }


        function s(e, t) {
            return N = t.getBoundingClientRect(), e.x = e.pageX - N.left - w.scrollX, e.y = e.pageY - N.top - w.scrollY, e
        }


        function f(t, n) {
            return s(t, e.element), n = n || {}, n.ox = n.x || t.x, n.oy = n.y || t.y, n.x = t.x, n.y = t.y, n.dx = n.x - n.ox, n.dy = n.y - n.oy, n
        }


        function g(e) {
            if (e.preventDefault(), W = a(e), W.originalEvent = e, W.touches)
                for (M.length = W.touches.length, _ = 0; _ < W.touches.length; _++) M[_] = f(W.touches[_], M[_]);
            else M.length = 0, M[0] = f(W, V);
            return i(V, M[0], !0), W
        }


        function h(t) {
            for (t = g(t), q = (Q = J.indexOf(z = t.type)) - 1, e.dragging = /down|start/.test(z) ? !0 : /up|end/.test(z) ? !1 : e.dragging; q;) o(J[q]) ? n(e[J[q--]], t) : o(J[Q]) ? n(e[J[Q++]], t) : q = 0
        }


        function p(t) {
            F = t.keyCode, H = "keyup" == t.type, Z[F] = Z[r(F)] = !H, n(e[t.type], t)
        }


        function v(t) {
            e.autopause && ("blur" == t.type ? b : C)(), n(e[t.type], t)
        }


        function C() {
            e.now = +new Date, e.running = !0
        }


        function b() {
            e.running = !1
        }


        function P() {
            (e.running ? b : C)()
        }


        function A() {
            K && e.clearRect(0, 0, e.width, e.height)
        }


        function S() {
            R = e.element.parentNode, _ = x.indexOf(e), R && R.removeChild(e.element), ~_ && x.splice(_, 1), u(!1), b()
        }
        var T, k, O, R, N, _, D, B, G, W, z, F, H, q, Q, j = 0,
            M = [],
            U = !1,
            X = w.devicePixelRatio,
            Y = e.type == m,
            K = e.type == d,
            V = {
                x: 0,
                y: 0,
                ox: 0,
                oy: 0,
                dx: 0,
                dy: 0
            },
            J = [e.element, h, "mousedown", "touchstart", h, "mousemove", "touchmove", h, "mouseup", "touchend", h, "click", y, p, "keydown", "keyup", w, v, "focus", "blur", l, "resize"],
            Z = {};
        for (F in E) Z[E[F]] = !1;
        return i(e, {
            touches: M,
            mouse: V,
            keys: Z,
            dragging: !1,
            running: !1,
            millis: 0,
            now: 0 / 0,
            dt: 0 / 0,
            destroy: S,
            toggle: P,
            clear: A,
            start: C,
            stop: b
        }), x.push(e), e.autostart && C(), u(!0), l(), c(), e
    }
    for (var l, s, f = "E LN10 LN2 LOG2E LOG10E PI SQRT1_2 SQRT2 abs acos asin atan ceil cos exp floor log round sin sqrt tan atan2 pow max min".split(" "), g = "__hasSketch", h = Math, d = "canvas", p = "webgl", m = "dom", y = document, w = window, x = [], v = {
            fullscreen: !0,
            autostart: !0,
            autoclear: !0,
            autopause: !0,
            container: y.body,
            interval: 1,
            globals: !0,
            retina: !1,
            type: d
        }, E = {
            8: "BACKSPACE",
            9: "TAB",
            13: "ENTER",
            16: "SHIFT",
            27: "ESCAPE",
            32: "SPACE",
            37: "LEFT",
            38: "UP",
            39: "RIGHT",
            40: "DOWN"
        }, C = {
            CANVAS: d,
            WEB_GL: p,
            WEBGL: p,
            DOM: m,
            instances: x,
            install: function (t) {
                if (!t[g]) {
                    for (var o = 0; o < f.length; o++) t[f[o]] = h[f[o]];
                    i(t, {
                        TWO_PI: 2 * h.PI,
                        HALF_PI: h.PI / 2,
                        QUATER_PI: h.PI / 4,
                        random: function (t, o) {
                            return e(t) ? t[~~(h.random() * t.length)] : (n(o) || (o = t || 1, t = 0), t + h.random() * (o - t))
                        },
                        lerp: function (e, t, n) {
                            return e + n * (t - e)
                        },
                        map: function (e, t, n, o, r) {
                            return (e - t) / (n - t) * (r - o) + o
                        }
                    }), t[g] = !0
                }
            },
            create: function (e) {
                return e = i(e || {}, v), e.globals && C.install(self), l = e.element = e.element || y.createElement(e.type === m ? "div" : "canvas"), s = e.context = e.context || function () {
                    switch (e.type) {
                        case d:
                            return l.getContext("2d", e);
                        case p:
                            return l.getContext("webgl", e) || l.getContext("experimental-webgl", e);
                        case m:
                            return l.canvas = l
                    }
                }(), e.container.appendChild(l), C.augment(s, e)
            },
            augment: function (e, t) {
                return t = i(t || {}, v), t.element = e.canvas || e, t.element.className += " sketch", i(e, t, !0), c(e)
            }
        }, b = ["ms", "moz", "webkit", "o"], P = self, A = 0, S = "AnimationFrame", T = "request" + S, k = "cancel" + S, I = P[T], L = P[k], O = 0; O < b.length && !I; O++) I = P[b[O] + "Request" + S], L = P[b[O] + "Cancel" + T];
    return P[T] = I = I || function (e) {
        var t = +new Date,
            n = h.max(0, 16 - (t - A)),
            o = setTimeout(function () {
                e(t + n)
            }, n);
        return A = t + n, o
    }, P[k] = L = L || function (e) {
        clearTimeout(e)
    }, C
}();

```

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <title>Pisual Mouse</title>
    <style>
        body{
            background-color: #1a1a1a;
        }
    </style>
    <script type="text/javascript" src="./js/sketch_min.js"></script>
</head>
<body id="body">
    <div id="test" style=" position:fixed;top:0px;z-index:20;"></div>
    <script>
        function Particle(x, y, radius) {
            this.init(x, y, radius);
        }
        Particle.prototype = {
            init: function (x, y, radius) {
                this.alive = true;
                this.radius = radius || 10;
                this.wander = 0.15;
                this.theta = random(TWO_PI);
                this.drag = 0.92;
                this.color = '#fff';
                this.x = x || 0.0;
                this.y = y || 0.0;
                this.vx = 0.0;
                this.vy = 0.0;
            },
            move: function () {
                this.x += this.vx;
                this.y += this.vy;
                this.vx *= this.drag;
                this.vy *= this.drag;
                this.theta += random(-0.5, 0.5) * this.wander;
                this.vx += sin(this.theta) * 0.1;
                this.vy += cos(this.theta) * 0.1;
                this.radius *= 0.96;
                this.alive = this.radius > 0.5;
            },
            draw: function (ctx) {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, TWO_PI);
                ctx.fillStyle = this.color;
                ctx.fill();
            }
        };
        var MAX_PARTICLES = 280;
        var COLOURS = ['#69D2E7', '#A7DBD8', '#E0E4CC', '#F38630', '#FA6900', '#FF4E50', '#F9D423'];
        // var COLOURS = ['#eee', '#d09', '#ccc', '#1a1a', '#902', '#f09', '#f90'];
        var particles = [];
        var pool = [];
        var demo = Sketch.create({
            container: document.getElementById('test')
        });
        console.log(demo)
        demo.setup = function () {
            var i, x, y;
            x = (demo.width * 0.5) + random(-100, 100);
            y = (demo.height * 0.5) + random(-100, 100);
            demo.spawn(0, 999);
        };
        demo.spawn = function (x, y) {
            if (particles.length >= MAX_PARTICLES)
                pool.push(particles.shift());
            particle = pool.length ? pool.pop() : new Particle();
            particle.init(x, y, random(5, 40));
            particle.wander = random(0.5, 2.0);
            particle.color = random(COLOURS);
            particle.drag = random(0.9, 0.99);
            theta = random(TWO_PI);
            force = random(2, 8);
            particle.vx = sin(theta) * force;
            particle.vy = cos(theta) * force;
            particles.push(particle);
        };
        demo.update = function () {
            var i, particle;
            for (i = particles.length - 1; i >= 0; i--) {
                particle = particles[i];
                if (particle.alive)
                    particle.move();
                else
                    pool.push(particles.splice(i, 1)[0]);
            }
        };
        demo.draw = function () {
            demo.globalCompositeOperation = 'lighter';
            for (var i = particles.length - 1; i >= 0; i--) {
                particles[i].draw(demo);
            }
        };
        demo.mousemove = function () {
            var particle, theta, force, touch, max, i, j, n;
            for (i = 0, n = demo.touches.length; i < n; i++) {
                touch = demo.touches[i], max = random(1, 8);
                for (j = 0; j < max; j++) {
                    demo.spawn(touch.x+20, touch.y+20);
                }
            }
        };
        demo.click = function () {
            var particle, theta, force, touch, max, i, j, n;
            for (i = 0, n = demo.touches.length; i < n; i++) {
                touch = demo.touches[i], max = random(1, 40);
                for (j = 0; j < max; j++) {
                    demo.spawn(touch.x, touch.y);
                }
            }
        };

        // //  点击效果
        // function demoClick() {
        //  var particle, theta, force, touch, max, i, j, n;
        //  for (i = 0, n = 10; i < n; i++) {
        //      touch = {
        //          dx: 5,
        //          dy: -3,
        //          ox: 1441,
        //          oy: 431,
        //          x: 1446,
        //          y: 428,
        //      };
        //      for (j = 0; j < 100; j++) {
        //          console.log(touch.x, touch.y)
        //          demo.spawn(touch.x, touch.y);
        //      }
        //  }
        // };
        // demoClick()
    </script>


</body>


</html>

```


## Loading 动画

> HTML

```html
  <!--loading框 圆环-->
    <!-- <div class="loadingCircle">
        <div class="LoaderCircle">
            <div class="tips">
                努力加载中
            </div>
        </div>
    </div> -->
    <!--loading框 三线旋转-->
    <!-- <div class="loadingThreeLine">
        <div class="line_one"></div>
        <div class="line_two"></div>
        <div class="line_three"></div>
        <div class="tips">
            加载中
        </div>
    </div> -->
    <!-- loading 多线条翻转 -->
    <!-- <div class="loadingRect">
        <div class="rect">
            <div class="rect1"></div>
            <div class="rect2"></div>
            <div class="rect3"></div>
            <div class="rect4"></div>
            <div class="rect5"></div>
        </div>
        <div class="tips">
            努力加载中...
        </div>
    </div> -->

    <!-- loading 多圆弹跳过渡 -->
    <!-- <div class="loadingBounce">
        <div class="bounce">
            <div class="bounce1"></div>
            <div class="bounce2"></div>
            <div class="bounce3"></div>
        </div>
        <div class="tips">
            努力加载中...
        </div>
    </div> -->
    <!-- loading 圆转圈过渡 -->
    <!-- <div class="loadingCircle">
        <div class="circle">
            <div class="circle-container container1">
              <div class="circle1"></div>
              <div class="circle2"></div>
              <div class="circle3"></div>
              <div class="circle4"></div>
            </div>
            <div class="circle-container container2">
              <div class="circle1"></div>
              <div class="circle2"></div>
              <div class="circle3"></div>
              <div class="circle4"></div>
            </div>
            <div class="circle-container container3">
              <div class="circle1"></div>
              <div class="circle2"></div>
              <div class="circle3"></div>
              <div class="circle4"></div>
            </div>
          </div>
          <div class="tips">
            努力加载中...
        </div>
    </div> -->
```

```css
/* ------------------ loading 圆环 ------------------ */
.loadingCircle {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #0009;
    z-index: 100;
}

.loadingCircle .LoaderCircle {
    position: relative;
    height: 80px;
    width: 80px;
    margin: 60% auto 0 35%;
}

.loadingCircle .tips {
    position: absolute;
    left: 50%;
    top: 60%;
    margin-left: -20px;
    width: 70px;
    font-size: 14px;
    font-weight: 500;
    color: #fff;
}

.loadingCircle .LoaderCircle::after,
.loadingCircle .LoaderCircle::before {
    content: "";
    width: 80px;
    height: 80px;
    position: absolute;
    border: solid 14px transparent;
    border-radius: 50%;
    -webkit-animation: circles 1.4s linear infinite;
    animation: circles 1.4s linear infinite;
}

.loadingCircle .LoaderCircle::before {
    border-top-color: #FFA995;
    border-bottom-color: #FFA995;
}

.loadingCircle .LoaderCircle::after {
    border-left-color: #fff;
    border-right-color: #fff;
    -webkit-animation-delay: 0.7s;
    animation-delay: 0.7s;
}

@keyframes circles {
    0% {
        -webkit-transform: rotate(0deg) scale(1);
        transform: rotate(0deg) scale(1);
    }

    50% {
        -webkit-transform: rotate(180deg) scale(1);
        transform: rotate(180deg) scale(1);
    }

    100% {
        -webkit-transform: rotate(360deg) scale(1);
        transform: rotate(360deg) scale(1);
    }
}

/* ------------------ loading 三线旋转 ------------------ */
.loadingThreeLine {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #0009;
    z-index: 100;
}

.loadingThreeLine .tips {
    position: absolute;
    left: 50%;
    top: 43.5%;
    margin-left: -25px;
    width: 70px;
    font-size: 16px;
    font-weight: 400;
    color: #fff;
}

.loadingThreeLine .line_one {
    width: 80px;
    height: 80px;
    position: absolute;
    left: 50%;
    top: 45%;
    margin: -42px 0 0 -42px;
    border: 2px solid #fff;
    border-radius: 80px 80px 80px 80px;
    border-right-color: transparent;
    border-top-color: transparent;
}

.loadingThreeLine .line_two {
    width: 100px;
    height: 100px;
    position: absolute;
    left: 50%;
    top: 45%;
    margin: -52px 0 0 -52px;
    border: 2px solid #fff;
    border-radius: 100px 100px 100px 100px;
    border-right-color: transparent;
    border-left-color: transparent;
}

.loadingThreeLine .line_three {
    width: 120px;
    height: 120px;
    position: absolute;
    left: 50%;
    top: 45%;
    margin: -62px 0 0 -62px;
    border: 2px solid #fff;
    border-radius: 120px 120px 120px 120px;
    border-right-color: transparent;
}

@-webkit-keyframes line1 {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }

    20% {
        -webkit-transform: rotate(720deg);
        transform: rotate(720deg);
    }

    50% {
        -webkit-transform: rotate(1080deg);
        transform: rotate(1080deg);
    }

    75% {
        -webkit-transform: rotate(1300deg);
        transform: rotate(1300deg);
    }

    100% {
        -webkit-transform: rotate(2500deg);
        transform: rotate(2500deg);
    }
}

@keyframes line1 {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }

    20% {
        -webkit-transform: rotate(720deg);
        transform: rotate(720deg);
    }

    50% {
        -webkit-transform: rotate(1080deg);
        transform: rotate(1080deg);
    }

    75% {
        -webkit-transform: rotate(1300deg);
        transform: rotate(1300deg);
    }

    100% {
        -webkit-transform: rotate(2500deg);
        transform: rotate(2500deg);
    }
}

.loadingThreeLine .line_one {
    -webkit-animation: line1 14s ease-in-out 1s infinite alternate;
    animation: line1 15s ease-in-out 1s infinite alternate;
}

@-webkit-keyframes line2 {
    from {
        -webkit-transform: rotate(360deg);
        transform: rotate(360deg);
    }

    to {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
}

@keyframes line2 {
    from {
        -webkit-transform: rotate(360deg);
        transform: rotate(360deg);
    }

    to {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
}

.loadingThreeLine .line_two {
    -webkit-animation: line2 3s ease-in-out infinite;
    animation: line2 3s ease-in-out infinite;
}

@-webkit-keyframes line3 {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }

    20% {
        -webkit-transform: rotate(720deg);
        transform: rotate(720deg);
    }

    50% {
        -webkit-transform: rotate(1080deg);
        transform: rotate(1080deg);
    }

    75% {
        -webkit-transform: rotate(1300deg);
        transform: rotate(1300deg);
    }

    100% {
        -webkit-transform: rotate(2500deg);
        transform: rotate(2500deg);
    }
}

@keyframes line3 {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }

    20% {
        -webkit-transform: rotate(720deg);
        transform: rotate(720deg);
    }

    50% {
        -webkit-transform: rotate(1080deg);
        transform: rotate(1080deg);
    }

    75% {
        -webkit-transform: rotate(1300deg);
        transform: rotate(1300deg);
    }

    100% {
        -webkit-transform: rotate(2500deg);
        transform: rotate(2500deg);
    }
}

.loadingThreeLine .line_three {
    -webkit-animation: line3 20s ease-in-out infinite;
    animation: line3 20s ease-in-out infinite;
}

/* ------------------ loading 多线条翻转 ------------------ */
.loadingRect {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #0009;
    z-index: 100;
}

.loadingRect .tips {
    position: absolute;
    left: 50%;
    top: 43%;
    margin-left: -45px;
    width: 100px;
    font-size: 16px;
    font-weight: 500;
    color: #fff;
}

.loadingRect .rect {
    margin: 0 auto;
    margin-top: 200px;
    width: 50px;
    height: 60px;
    text-align: center;
    font-size: 10px;
}

.loadingRect .rect>div {
    background-color: #fff;
    height: 100%;
    width: 6px;
    display: inline-block;
    -webkit-animation: stretchdelay 1.2s infinite ease-in-out;
    animation: stretchdelay 1.2s infinite ease-in-out;
}

.loadingRect .rect .rect2 {
    -webkit-animation-delay: -1.1s;
    animation-delay: -1.1s;
}

.loadingRect .rect .rect3 {
    -webkit-animation-delay: -1.0s;
    animation-delay: -1.0s;
}

.loadingRect .rect .rect4 {
    -webkit-animation-delay: -0.9s;
    animation-delay: -0.9s;
}

.loadingRect .rect .rect5 {
    -webkit-animation-delay: -0.8s;
    animation-delay: -0.8s;
}

@-webkit-keyframes stretchdelay {

    0%,
    40%,
    100% {
        -webkit-transform: scaleY(0.4)
    }

    20% {
        -webkit-transform: scaleY(1.0)
    }
}

@keyframes stretchdelay {

    0%,
    40%,
    100% {
        transform: scaleY(0.4);
        -webkit-transform: scaleY(0.4);
    }

    20% {
        transform: scaleY(1.0);
        -webkit-transform: scaleY(1.0);
    }
}

/* ------------------ loading 多圆弹跳过渡 ------------------ */
.loadingBounce {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #0009;
    z-index: 100;
}

.loadingBounce .tips {
    position: absolute;
    left: 50%;
    top: 43%;
    margin-left: -45px;
    width: 100px;
    font-size: 16px;
    font-weight: 500;
    color: #fff;
}

.loadingBounce .bounce {
    margin: 0 auto 0;
    margin-top: 200px;
    width: 150px;
    text-align: center;
}

.loadingBounce .bounce>div {
    width: 30px;
    height: 30px;
    background-color: #fff;
    border-radius: 100%;
    display: inline-block;
    -webkit-animation: bouncedelay 1.4s infinite ease-in-out;
    animation: bouncedelay 1.4s infinite ease-in-out;
    /* 当动画开始时防止第一帧闪烁 */
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
}

.loadingBounce .bounce .bounce1 {
    -webkit-animation-delay: -0.32s;
    animation-delay: -0.32s;
}

.loadingBounce .bounce .bounce2 {
    -webkit-animation-delay: -0.16s;
    animation-delay: -0.16s;
}

@-webkit-keyframes bouncedelay {

    0%,
    80%,
    100% {
        -webkit-transform: scale(0.0)
    }

    40% {
        -webkit-transform: scale(1.0)
    }
}

@keyframes bouncedelay {

    0%,
    80%,
    100% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
    }

    40% {
        transform: scale(1.0);
        -webkit-transform: scale(1.0);
    }
}

/* ------------------ loading 圆转圈过渡 ------------------ */
.loadingCircle {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #0009;
    z-index: 100;
}

.loadingCircle .tips {
    position: absolute;
    left: 50%;
    top: 43%;
    margin-left: -45px;
    width: 100px;
    font-size: 16px;
    font-weight: 500;
    color: #fff;
}

.loadingCircle .circle {
    margin: 0 auto;
    margin-top: 200px;
    width: 50px;
    height: 50px;
    position: relative;
}

.loadingCircle .container1>div,
.loadingCircle .container2>div,
.loadingCircle .container3>div {
    width: 16px;
    height: 16px;
    background-color: #fff;
    border-radius: 100%;
    position: absolute;
    -webkit-animation: bouncedelay 1.2s infinite ease-in-out;
    animation: bouncedelay 1.2s infinite ease-in-out;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
}

.loadingCircle .circle .circle-container {
    position: absolute;
    width: 100%;
    height: 100%;
}

.loadingCircle .container2 {
    -webkit-transform: rotateZ(45deg);
    transform: rotateZ(45deg);
}

.loadingCircle .container3 {
    -webkit-transform: rotateZ(90deg);
    transform: rotateZ(90deg);
}

.loadingCircle .circle1 {
    top: 0;
    left: 0;
}

.loadingCircle .circle2 {
    top: 0;
    right: 0;
}

.loadingCircle .circle3 {
    right: 0;
    bottom: 0;
}

.loadingCircle .circle4 {
    left: 0;
    bottom: 0;
}

.loadingCircle .container2 .circle1 {
    -webkit-animation-delay: -1.1s;
    animation-delay: -1.1s;
}

.loadingCircle .container3 .circle1 {
    -webkit-animation-delay: -1.0s;
    animation-delay: -1.0s;
}

.loadingCircle .container1 .circle2 {
    -webkit-animation-delay: -0.9s;
    animation-delay: -0.9s;
}

.loadingCircle .container2 .circle2 {
    -webkit-animation-delay: -0.8s;
    animation-delay: -0.8s;
}

.loadingCircle .container3 .circle2 {
    -webkit-animation-delay: -0.7s;
    animation-delay: -0.7s;
}

.loadingCircle .container1 .circle3 {
    -webkit-animation-delay: -0.6s;
    animation-delay: -0.6s;
}

.loadingCircle .container2 .circle3 {
    -webkit-animation-delay: -0.5s;
    animation-delay: -0.5s;
}

.loadingCircle .container3 .circle3 {
    -webkit-animation-delay: -0.4s;
    animation-delay: -0.4s;
}

.loadingCircle .container1 .circle4 {
    -webkit-animation-delay: -0.3s;
    animation-delay: -0.3s;
}

.loadingCircle .container2 .circle4 {
    -webkit-animation-delay: -0.2s;
    animation-delay: -0.2s;
}

.loadingCircle .container3 .circle4 {
    -webkit-animation-delay: -0.1s;
    animation-delay: -0.1s;
}

@-webkit-keyframes bouncedelay {

    0%,
    80%,
    100% {
        -webkit-transform: scale(0.0)
    }

    40% {
        -webkit-transform: scale(0.8)
    }
}

@keyframes bouncedelay {
    0%,
    80%,
    100% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
    }
    40% {
        transform: scale(0.8);
        -webkit-transform: scale(0.8);
    }
}

```

## vue移动端返回按钮拖拽（仿IOS）

```vue
<template>
  <!-- 悬浮 -->
  <div id="float_button" @touchmove.prevent>
    <div
      @click="onBtnClicked"
      ref="floatButton"
      class="float_info"
      :style="{
        left: left + 'px',
        top: top + 'px',
      }"
    >
      <img src="../assets/icon/back4.png" alt="返回" srcset="" />
    </div>
  </div>
</template>
<script>
export default {
  name: "",
  components: {},
  data() {
    return {
      clientWidth: 0,
      clientHeight: 0,
      timer: null,
      currentTop: 0,
      left: 0,
      top: 0,
    };
  },
  props: {
    gapWidth: {
      // 距离左右两边距离
      type: Number,
      default: 0,
    },
    coefficientHeight: {
      // 从上到下距离比例
      type: Number,
      default: 0.4,
    },
  },
  computed: {},
  methods: {
    //   点击的时候置行父组件方法
    onBtnClicked() {
      this.$emit("backGoTo");
    },
    handleScrollStart() {
      this.timer && clearTimeout(this.timer);
      this.timer = setTimeout(() => {
        this.handleScrollEnd();
      }, 300);
      this.currentTop =
        document.documentElement.scrollTop || document.body.scrollTop;
      if (this.left > this.clientWidth / 2) {
        this.left = this.clientWidth - this.itemWidth / 2;
      } else {
        this.left = -this.itemWidth / 2;
      }
    },
    handleScrollEnd() {
      let scrollTop =
        document.documentElement.scrollTop || document.body.scrollTop;
      if (scrollTop === this.currentTop) {
        if (this.left > this.clientWidth / 2) {
          this.left = this.clientWidth - this.itemWidth - this.gapWidth;
        } else {
          this.left = this.gapWidth;
        }
        clearTimeout(this.timer);
      }
    },
  },
  created() {
    this.clientWidth = document.documentElement.clientWidth;
    this.clientHeight = document.documentElement.clientHeight;
    this.left = this.clientWidth - this.itemWidth - this.gapWidth;
    this.top = this.clientHeight * this.coefficientHeight;
  },
  mounted() {
    this.$nextTick(() => {
      const floatButton = this.$refs.floatButton;
      floatButton.addEventListener("touchstart", () => {
        floatButton.style.transition = "none";
      });
      // 在拖拽的过程中，组件应该跟随手指的移动而移动。
      floatButton.addEventListener("touchmove", (e) => {
        // console.log("移动中", e);
        if (e.targetTouches.length === 1) {
          // 一根手指
          let touch = e.targetTouches[0];
          this.left = touch.clientX - 20;
          // 判断是否超出
          if (touch.clientY - 25 <= 0) {
            this.top = 0;
          } else {
            this.top = touch.clientY - 25;
          }
        }
      });
      // 拖拽结束以后，重新调整组件的位置并重新设置过度动画。
      floatButton.addEventListener("touchend", () => {
        floatButton.style.transition = "all 0.3s";
        if (this.left > document.documentElement.clientWidth / 2) {
          this.left = document.documentElement.clientWidth - this.$refs.floatButton.offsetWidth;
        } else {
          this.left = 0;
        }
      });
    });
  },
  beforeDestroy() {
    // 移除监听页面滚动
    window.removeEventListener("scroll", this.handleScrollStart);
  },
};
</script>
<style lang='scss'>
#float_button {
  .float_info {
    position: fixed;
    bottom: 436px;
    left: 0;
    width: 40px;
    height: 40px;
    display: flex;
    flex-flow: column;
    justify-content: center;
    align-items: center;
    box-shadow: 0 6px 20px 10px rgba(0, 0, 0, 0.1);
    color: #666666;
    transition: all 0.3s;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    z-index: 999;
    cursor: pointer;
    .text {
      font-size: 24px;
      color: #fff;
    }
    img {
      width: 20px;
      height: 20px;
    }
  }
}
</style>
```