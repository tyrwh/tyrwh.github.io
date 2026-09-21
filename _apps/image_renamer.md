---
title: "Launch the minimal Gradio app"
excerpt: "A demo page to launch a service on Google Cloud Run."
---

Somewhere in this page, there should be something that is launching a Google Cloud Run app. Trying it out now with an event listener.

<script>
window.addEventListener('load', () => {
  fetch('https://gradio-minimal-516395572783.us-central1.run.app/')
    .catch(error => console.error('Request failed:', error));
});
</script>