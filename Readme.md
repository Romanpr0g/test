<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        .slider {
            display: flex;
            overflow: hidden;
            width: 440px;
        }
        .slider-track {
            display: flex;
            transition: transform 0.5s ease;
        }
        .slider-item {
            min-width: 100px;
            margin-right: 10px;
        }
        .controls {
            display: flex;
            justify-content: space-between;
            width: 440px;
            margin-top: 10px;
        }
        .control {
            cursor: pointer;
            opacity: 1;
            transition: opacity 0.3s;
        }
        .disabled {
            opacity: 0.5;
            pointer-events: none;
        }
    </style>
</head>
<body>

<section class="category-wrapper">
    <div class="category-container">
        <div class="category-info">
            <h3 class="category-title">Музыка</h3>
            <div class="category-pagination">
                <img class="category-arrow control prev disabled" src="assets/svg/arrow-circle-left.svg" alt="Previous">
                <img class="category-arrow control next" src="assets/svg/arrow-circle-right.svg" alt="Next">
            </div>
        </div>
        <div class="slider">
            <div class="slider-track">
                <img class="slider-item" src="assets/images/first.jfif" alt="Image 1">
                <img class="slider-item" src="assets/images/second.jfif" alt="Image 2">
                <img class="slider-item" src="assets/images/third.jfif" alt="Image 3">
                <img class="slider-item" src="assets/images/fourth.jfif" alt="Image 4">
                <img class="slider-item" src="assets/images/fifth.jfif" alt="Image 5">
                <img class="slider-item" src="assets/images/sixth.jfif" alt="Image 6">
                <img class="slider-item" src="assets/images/seventh.jfif" alt="Image 7">
            </div>
        </div>
    </div>

    <div class="category-container">
        <div class="category-info">
            <h3 class="category-title">Театр</h3>
            <div class="category-pagination">
                <img class="category-arrow control prev disabled" src="assets/svg/arrow-circle-left.svg" alt="Previous">
                <img class="category-arrow control next" src="assets/svg/arrow-circle-right.svg" alt="Next">
            </div>
        </div>
        <div class="slider">
            <div class="slider-track">
                <img class="slider-item" src="assets/images/first.jfif" alt="Image 1">
                <img class="slider-item" src="assets/images/second.jfif" alt="Image 2">
                <img class="slider-item" src="assets/images/third.jfif" alt="Image 3">
                <img class="slider-item" src="assets/images/fourth.jfif" alt="Image 4">
                <img class="slider-item" src="assets/images/fifth.jfif" alt="Image 5">
                <img class="slider-item" src="assets/images/sixth.jfif" alt="Image 6">
                <img class="slider-item" src="assets/images/seventh.jfif" alt="Image 7">
            </div>
        </div>
    </div>
</section>

<script>
    document.querySelectorAll('.category-container').forEach(container => {
        const track = container.querySelector('.slider-track');
        const items = container.querySelectorAll('.slider-item');
        const prevButton = container.querySelector('.prev');
        const nextButton = container.querySelector('.next');

        let position = 0;
        const visibleItems = 4;
        const scrollItems = 2;

        function updateButtons() {
            prevButton.classList.toggle('disabled', position === 0);
            nextButton.classList.toggle('disabled', position >= items.length - visibleItems);
        }

        function moveSlider(direction) {
            position += direction * scrollItems;
            if (position < 0) {
                position = 0;
            } else if (position > items.length - visibleItems) {
                position = items.length - visibleItems;
            }
            track.style.transform = `translateX(-${position * (100 + 10)}px)`;
            updateButtons();
        }

        prevButton.addEventListener('click', () => moveSlider(-1));
        nextButton.addEventListener('click', () => moveSlider(1));

        updateButtons();
    });
</script>

</body>
</html>
