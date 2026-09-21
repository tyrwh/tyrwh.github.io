---
title: "BIGapp Rshiny platform"
excerpt: "A demo page to launch a service on Google Cloud Run."
---

This is a page to launch Breeding Insight's BIGapp (BI Genomics app), an RShiny-based platform to etc etc

For more information about BIGapp, visit its Github [here](https://github.com/Breeding-Insight/BIGapp)

<script>
window.addEventListener('load', () => {
  fetch('https://bigapp-516395572783.us-central1.run.app/')
    .catch(error => console.error('Request failed:', error));
});
</script>