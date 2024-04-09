
       
        !DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Image Slider</title>
<style>
    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
    }
    .slider-container {
        position: relative;
        width: 100%;
        max-width: 800px;
        margin: auto;
        overflow: hidden;
    }
    .slides {
        display: flex;
        transition: transform 0.5s ease;
    }
    .slide {
        min-width: 100%;
        overflow: hidden;
    }
    .slide img {
        width: 100%;
        height: auto;
    }
    .prev, .next {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        font-size: 24px;
        cursor: pointer;
        z-index: 1000;
    }
    .prev {
        left: 10px;
    }
    .next {
        right: 10px;
    }
</style>
</head>
<body>
<div class="slider-container">
    <div class="slides">
        <div class="slide"><img src="image1.jpg" alt="Image 1"></div>
        <div class="slide"><img src="image2.jpg" alt="Image 2"></div>
        <div class="slide"><img src="image3.jpg" alt="Image 3"></div>
        <!-- Add more slides as needed -->
    </div>
    <div class="prev">&#10094;</div>
    <div class="next">&#10095;</div>
</div>

<script>
    const slides = document.querySelector('.slides');
    const slide = document.querySelectorAll('.slide');
    const prevBtn = document.querySelector('.prev');
    const nextBtn = document.querySelector('.next');
    let counter = 1;
    const size = slide[0].clientWidth;

    slides.style.transform = 'translateX(' + (-size * counter) + 'px)';

    // Button listeners
    nextBtn.addEventListener('click', () => {
        if (counter >= slide.length - 1) return;
        slides.style.transition = "transform 0.5s ease-in-out";
        counter++;
        slides.style.transform = 'translateX(' + (-size * counter) + 'px)';
    });

    prevBtn.addEventListener('click', () => {
        if (counter <= 0) return;
        slides.style.transition = "transform 0.5s ease-in-out";
        counter--;
        slides.style.transform = 'translateX(' + (-size * counter) + 'px)';
    });

    // Automatic sliding
    setInterval(() => {
        if (counter >= slide.length - 1) return;
        slides.style.transition = "transform 0.5s ease-in-out";
        counter++;
        slides.style.transform = 'translateX(' + (-size * counter) + 'px)';
    }, 2000);

    // Looping
    slides.addEventListener('transitionend', () => {
        if (slide[counter].id === 'lastClone') {
            slides.style.transition = "none";
            counter = slide.length - 2;
            slides.style.transform = 'translateX(' + (-size * counter) + 'px)';
        }
        if (slide[counter].id === 'firstClone') {
            slides.style.transition = "none";
            counter = slide.length - counter;
            slides.style.transform = 'translateX(' + (-size * counter) + 'px)';
        }
    });
</script>
</body>
</html>
