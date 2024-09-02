# TEST
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Циклический слайдер</title>
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
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            display: none;
        }

        .pagination .arrow {
            display: inline-block;
            width: 20px;
            height: 20px;
            background-color: #333;
            color: #fff;
            text-align: center;
            line-height: 20px;
            border-radius: 50%;
            cursor: pointer;
        }
    </style>
</head>

<body>
    <div class="slider">
        <div class="slide slide-prev">Slide 3</div>
        <div class="slide active">Slide 1</div>
        <div class="slide slide-next">Slide 2</div>
        <div class="pagination">
            <div class="arrow prev">&#8249;</div>
            <div class="arrow next">&#8250;</div>
        </div>
    </div>

    <script>
        const slider = document.querySelector('.slider');
        const slides = document.querySelectorAll('.slide');
        const prevBtn = document.querySelector('.arrow.prev');
        const nextBtn = document.querySelector('.arrow.next');

        let currentSlide = 0;

        function showSlide(n) {
            slides.forEach((slide, index) => {
                let position = index - n;
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
            currentSlide = (currentSlide === 0) ? 2 : currentSlide - 1;
            showSlide(currentSlide);
        });

        nextBtn.addEventListener('click', () => {
            currentSlide = (currentSlide === 2) ? 0 : currentSlide + 1;
            showSlide(currentSlide);
        });

        showSlide(currentSlide);
    </script>
</body>

</html>
