---
layout: page
title: Evaluation
#description: The evaluation of my courses
img: assets/img/evaluation_illustration.jpg
importance: 3
category: Me as a teacher
#related_publications: einstein1956investigations, einstein1950meaning
---

Below are some of the feedback and evaluations I have received from my students. 
<div class="quote-carousel">
  <div class="quote-slide active">
    <em>"The way you explained complex concepts in a simple and relatable manner was incredibly helpful. Your passion for the subject really inspired me to learn more."</em>
  </div>
  <div class="quote-slide">
    <em>"I appreciated the inclusive and supportive environment you created in the classroom. It made me feel comfortable asking questions and engaging with the material."</em>
  </div>
  <div class="quote-slide">
    <em>"Your use of practical examples and hands-on activities helped me understand the subject matter more deeply. Thank you for making learning so enjoyable."</em>
  </div>
  <div class="quote-slide">
    <em>"The feedback and support you provided throughout the course were invaluable. You truly care about your students' success and it shows."</em>
  </div>
  <div class="quote-slide">
    <em>"Thank you for making math less intimidating and more accessible. Your teaching methods really made a difference for me."</em>
  </div>
  <button class="prev" onclick="prevSlide()">&#10094;</button>
  <button class="next" onclick="nextSlide()">&#10095;</button>
</div>

<style>
.quote-carousel {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  overflow: hidden;
  position: relative;
}

.quote-slide {
  width: 100%;
  display: none;
  padding: 20px;
  box-sizing: border-box;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #ffffff; /* Ensure background is white */
  color: #000000; /* Ensure text color is black */
  font-size: 1.2em; /* Increase font size for better readability */
}

.quote-slide.active {
  display: block;
}

button.prev, button.next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: #f1f1f1;
  border: none;
  padding: 10px;
  cursor: pointer;
  border-radius: 50%;
  user-select: none;
  color: #000000; /* Ensure button text color is black */
}

button.prev {
  left: 10px;
}

button.next {
  right: 10px;
}

button.prev:hover, button.next:hover {
  background-color: #ddd;
}
</style>

<script>
let currentIndex = 0;
const slides = document.querySelectorAll('.quote-slide');

function showSlide(index) {
  slides.forEach((slide, i) => {
    slide.classList.toggle('active', i === index);
  });
}

function nextSlide() {
  currentIndex = (currentIndex + 1) % slides.length;
  showSlide(currentIndex);
}

function prevSlide() {
  currentIndex = (currentIndex - 1 + slides.length) % slides.length;
  showSlide(currentIndex);
}

showSlide(currentIndex);
setInterval(nextSlide, 3000); // Change slide every 3 seconds
</script>
