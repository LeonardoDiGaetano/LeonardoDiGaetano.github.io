---
layout: page
title: Evaluation
#description: The evaluation of my courses
img: assets/img/evaluation_illustration.jpg
importance: 6
category: Me as a teacher
#related_publications: einstein1956investigations, einstein1950meaning
---

Below are some of the feedback and evaluations I have received from my students. 

### Instructor Evaluation Table

| Question | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | Responses | Individual Mean | UGS Mean | Pct Rnk |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Q2: The instructor was well prepared for the course. | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 7 | 8 | 17 | 9.2 | 9.1 | 34 |
| Q3: Presentations by the instructor were clear. | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 3 | 5 | 7 | 17 | 8.7 | 8.7 | 35 |
| Q4: The classroom environment encouraged student participation. | 0 | 0 | 0 | 0 | 1 | 0 | 2 | 4 | 1 | 8 | 16 | 8.0 | 8.7 | 20 |
| Q5: The instructor treated the students in a respectful and professional manner. | 0 | 0 | 0 | 0 | 0 | 0 | 4 | 1 | 1 | 11 | 17 | 9.4 | 9.5 | 31 |
| Q6: Feedback was given throughout the course. | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 7 | 7 | 17 | 9.2 | 8.5 | 68 |
| Q7: The instructor was available for appointments and consultations outside of class. | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 2 | 1 | 13 | 17 | 9.8 | 9.4 | 58 |

### Student Testimonials

<div class="quote-carousel">
  <div class="quote-slide active">
    <em>"One of my best TA classes so far, thank you"</em>
  </div>
  <div class="quote-slide">
    <em>"Thank you for your work, open personality made classes fun and interesting"</em>
  </div>
  <div class="quote-slide">
    <em>"Keep the relaxed manner, I think it suited the style of this course very well."</em>
  </div>
  <div class="quote-slide">
    <em>"Fantastic TA, not only prepared but also nice and friendly."</em>
  </div>
  <div class="quote-slide">
    <em>"Very good instructor, maybe finds something sometimes hard to explain but tries doing everything in his power to help. Very well done, wish there were more assistants like him!"</em>
  </div>
  <div class="quote-slide">
    <em>"Leonardo is fully devoted, patient and always available to students. He is always well prepared and I really like his method – I would send him specific questions and he would explain them during TA sessions. He does even more than just focus on the questions by explaining broader mathematical concepts and relevant theory. This helps us strengthen our knowledge to be able to apply it to other questions. In this way, not only does he resolve the problems of one student, but makes the session beneficial for all attending his session. Additionally, I was very grateful that he identified some of my knowledge gaps, and he did it constructively and respectfully. He would always do an effort to answer all of our questions, even if it would take him extra time. Leonardo’s attention, guidance and support were very precious to me as it would help me grasp the concepts which I didn’t understand in class. I sincerely enjoyed the collaboration with him and I wish to have someone like him next semester."</em>
  </div>
  <div class="quote-slide">
    <em>"He was absolutely great, he was the highlight of this course. Extremely kind, well prepared and available. Best TA we could ask for."</em>
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
  background-color: #424246; /* Ensure background is white */
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
