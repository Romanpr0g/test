<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Циклический слайдер с пагинацией</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }

        .slider {
            width: 300px;
            position: relative;
            perspective: 1000px;
            cursor: pointer;
        }

        .slide {
            position: absolute;
            width: 100%;
            height: 200px;
            transition: transform 0.5s;
            border: 1px solid #ccc;
            box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            opacity: 0.5;
        }

        .slide.active {
            transform: translateX(0);
            opacity: 1;
        }

        .slide-prev {
            transform: translateX(-100%);
        }

        .slide-next {
            transform: translateX(100%);
        }

        .pagination {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            display: none;
        }

        .arrow {
            position: absolute;
            top: 0;
            bottom: 0;
            width: 30px;
            background-color: rgba(0, 0, 0, 0.5);
            color: #fff;
            text-align: center;
            line-height: 200px;
            cursor: pointer;
        }

        .arrow.left {
            left: 0;
        }

        .arrow.right {
            right: 0;
        }
    </style>
</head>

<body>
    <div class="slider">
        <div class="slide slide-prev">Slide 3</div>
        <div class="slide active">Slide 1</div>
        <div class="slide slide-next">Slide 2</div>
        <div class="pagination">
            <div class="arrow left">&#8249;</div>
            <div class="arrow right">&#8250;</div>
        </div>
    </div>

    <script>
        const slider = document.querySelector('.slider');
        const slides = document.querySelectorAll('.slide');
        const prevBtn = document.querySelector('.arrow.left');
        const nextBtn = document.querySelector('.arrow.right');

        let currentSlide = 1;

        function showSlide(n) {
            currentSlide = (n + 3) % 3;
            slides.forEach((slide, index) => {
                let position = index - currentSlide;
                slide.classList.remove('active', 'slide-prev', 'slide-next');
                if (position === 0) {
                    slide.classList.add('active');
                } else if (position === -1 || position === 2) {
                    slide.classList.add('slide-prev');
                } else if (position === 1 || position === -2) {
                    slide.classList.add('slide-next');
                }
            });
        }

        function showPagination() {
            const pagination = document.querySelector('.pagination');
            pagination.style.display = 'block';
        }

        slider.addEventListener('mouseenter', showPagination);
        slider.addEventListener('mouseleave', () => {
            const pagination = document.querySelector('.pagination');
            pagination.style.display = 'none';
        });

        prevBtn.addEventListener('click', () => {
            showSlide(currentSlide - 1);
        });

        nextBtn.addEventListener('click', () => {
            showSlide(currentSlide + 1);
        });

        showSlide(currentSlide);
    </script>
</body>

</html>
