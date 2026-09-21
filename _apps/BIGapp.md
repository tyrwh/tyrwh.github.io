---
title: "BIGapp Rshiny platform"
excerpt: "Analyze genomic data across different species ploidy without needing to use command-line tools."
---

This is a page to launch Breeding Insight's BIGapp (BI Genomics app), an RShiny-based platform to do genomics and such.

For more information about BIGapp, visit its Github [here](https://github.com/Breeding-Insight/BIGapp).

<script>
window.addEventListener('load', () => {
  fetch('https://bigapp-516395572783.us-central1.run.app/')
    .catch(error => console.error('Request failed:', error));
});
</script>