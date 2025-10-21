# Feedback

## Você gostou das receitas?

<div id="feedback-form" style="text-align: center; margin: 2rem 0;">
  <div style="margin-bottom: 1rem;">
    <button class="rating-btn" data-rating="1" style="font-size: 2rem; margin: 0 0.5rem; background: none; border: none; cursor: pointer;">😞</button>
    <button class="rating-btn" data-rating="2" style="font-size: 2rem; margin: 0 0.5rem; background: none; border: none; cursor: pointer;">😕</button>
    <button class="rating-btn" data-rating="3" style="font-size: 2rem; margin: 0 0.5rem; background: none; border: none; cursor: pointer;">😐</button>
    <button class="rating-btn" data-rating="4" style="font-size: 2rem; margin: 0 0.5rem; background: none; border: none; cursor: pointer;">😊</button>
    <button class="rating-btn" data-rating="5" style="font-size: 2rem; margin: 0 0.5rem; background: none; border: none; cursor: pointer;">😍</button>
  </div>
  <div id="feedback-message" style="margin-top: 1rem; font-weight: bold;"></div>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const buttons = document.querySelectorAll('.rating-btn');
  const message = document.getElementById('feedback-message');
  
  buttons.forEach(button => {
    button.addEventListener('click', function() {
      const rating = this.dataset.rating;
      
      buttons.forEach(btn => btn.style.opacity = '0.3');
      this.style.opacity = '1';
      
      fetch('/api/feedback', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ rating: parseInt(rating) })
      }).then(() => {
        message.textContent = 'Obrigado pelo seu feedback!';
      }).catch(() => {
        message.textContent = 'Feedback salvo localmente!';
      });
    });
  });
});
</script>
