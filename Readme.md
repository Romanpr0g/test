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

<div class="slider-wrapper">
    <div class="slider">
        <div class="slider-track">
            <img class="slider-item" src="image1.jpg" alt="Image 1">
            <img class="slider-item" src="image2.jpg" alt="Image 2">
            <img class="slider-item" src="image3.jpg" alt="Image 3">
            <img class="slider-item" src="image4.jpg" alt="Image 4">
            <img class="slider-item" src="image5.jpg" alt="Image 5">
            <img class="slider-item" src="image6.jpg" alt="Image 6">
        </div>
    </div>
    <div class="controls">
        <img id="prev" class="control disabled" src="prev.svg" alt="Previous">
        <img id="next" class="control" src="next.svg" alt="Next">
    </div>
</div>

<script>
    const track = document.querySelector('.slider-track');
    const items = document.querySelectorAll('.slider-item');
    const prevButton = document.getElementById('prev');
    const nextButton = document.getElementById('next');

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
</script>

</body>
</html>
