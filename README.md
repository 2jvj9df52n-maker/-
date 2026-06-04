<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>我的博客主页</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Helvetica+Neue:wght@400;600;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

body {
    background: #f5f5f7;
    color: #1d1d1f;
    line-height: 1.6;
}

/* ===== 顶部导航（毛玻璃） ===== */
header {
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 999;
    padding: 14px 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    background: rgba(255,255,255,0.6);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(0,0,0,0.06);
    transition: all 0.3s ease;
}

header.scrolled {
    background: rgba(255,255,255,0.85);
    box-shadow: 0 2px 20px rgba(0,0,0,0.08);
}

header h1 {
    font-size: 20px;
    font-weight: 700;
}

nav a {
    margin-left: 18px;
    text-decoration: none;
    color: #1d1d1f;
    font-weight: 500;
    position: relative;
}

nav a.active::after {
    content: "";
    position: absolute;
    left: 0;
    bottom: -6px;
    width: 100%;
    height: 2px;
    background: #007aff;
    border-radius: 2px;
}

/* ===== 页面布局 ===== */
.container {
    max-width: 900px;
    margin: 120px auto 60px;
    padding: 0 20px;
}

/* ===== 进入动画 ===== */
.fade {
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease;
}

.fade.show {
    opacity: 1;
    transform: translateY(0);
}

/* ===== 个人介绍 ===== */
.intro {
    text-align: center;
    margin-bottom: 80px;
}

.intro img {
    width: 110px;
    height: 110px;
    border-radius: 50%;
    margin-bottom: 20px;
}

.intro h2 {
    font-size: 30px;
    margin-bottom: 10px;
}

.intro p {
    color: rgba(60,60,67,0.7);
}

/* ===== 博客列表 ===== */
.blog-list {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    margin-bottom: 80px;
}

.blog-item {
    background: #fff;
    padding: 22px;
    border-radius: 18px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.06);
    transition: transform 0.25s ease;
}

.blog-item:hover {
    transform: translateY(-6px);
}

.blog-item h3 {
    margin-bottom: 8px;
}

.blog-item p {
    color: rgba(60,60,67,0.7);
    font-size: 14px;
}

/* ===== 联系方式 ===== */
.contact {
    text-align: center;
    background: #fff;
    padding: 40px 20px;
    border-radius: 18px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.06);
}

.contact h3 {
    margin-bottom: 20px;
}

.contact a {
    display: inline-block;
    margin: 0 8px;
    padding: 10px 18px;
    border-radius: 12px;
    background: #007aff;
    color: #fff;
    text-decoration: none;
    font-weight: 500;
    transition: 0.2s;
}

.contact a:hover {
    background: #0051a8;
}

/* footer */
footer {
    text-align: center;
    padding: 30px;
    color: rgba(60,60,67,0.6);
    font-size: 13px;
}
</style>
</head>

<body>

<header id="header">
    <h1>我的博客</h1>
    <nav>
        <a href="#intro" class="active">关于</a>
        <a href="#blog">博客</a>
        <a href="#contact">联系</a>
    </nav>
</header>

<div class="container">

    <section id="intro" class="intro fade">
        <img src="https://via.placeholder.com/120" alt="">
        <h2>你好，我是博主</h2>
        <p>写点代码，也写点生活。</p>
    </section>

    <section id="blog" class="blog-list fade">
        <div class="blog-item">
            <h3>第一篇文章</h3>
            <p>这里是文章摘要，用来展示内容核心。</p>
        </div>
        <div class="blog-item">
            <h3>第二篇文章</h3>
            <p>这里是文章摘要，用来展示内容核心。</p>
        </div>
        <div class="blog-item">
            <h3>第三篇文章</h3>
            <p>这里是文章摘要，用来展示内容核心。</p>
        </div>
    </section>

    <section id="contact" class="contact fade">
        <h3>联系我</h3>
        <a href="mailto:example@email.com">Email</a>
        <a href="#">GitHub</a>
        <a href="#">Twitter</a>
    </section>

</div>

<footer>
    © 2026 我的博客 · All Rights Reserved
</footer>

<script>
// ===== header 滚动效果 =====
const header = document.getElementById("header");

window.addEventListener("scroll", () => {
    if (window.scrollY > 10) {
        header.classList.add("scrolled");
    } else {
        header.classList.remove("scrolled");
    }
});

// ===== 滚动进入动画 =====
const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add("show");
        }
    });
}, { threshold: 0.15 });

document.querySelectorAll(".fade").forEach(el => observer.observe(el));

// ===== 导航高亮 =====
const sections = document.querySelectorAll("section");
const navLinks = document.querySelectorAll("nav a");

window.addEventListener("scroll", () => {
    let current = "";

    sections.forEach(section => {
        const top = section.offsetTop - 150;
        if (window.scrollY >= top) {
            current = section.id;
        }
    });

    navLinks.forEach(link => {
        link.classList.remove("active");
        if (link.getAttribute("href") === "#" + current) {
            link.classList.add("active");
        }
    });
});
</script>

</body>
</html>
