---
title: "Gradio demo app"
excerpt: "A simple demo Gradio app to demonstrate Cloud Run hosting."
---

Somewhere in this page, there should be something that is launching a Google Cloud Run app. Trying it out now with an event listener.

<script>
window.addEventListener('load', () => {
  fetch('https://gradio-minimal-516395572783.us-central1.run.app/')
    .catch(error => console.error('Request failed:', error));
});
</script>