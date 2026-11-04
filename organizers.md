---
layout: default

# TODO(2027): placeholder copied from the 2024 committee — update names/affiliations.
speakers:
  - name: Prof. Matthias Ihme
    url: https://web.stanford.edu/group/ihmegroup/cgi-bin/MatthiasIhme/people/matthias-ihme/
    aff: Stanford University, SLAC
    image: /assets/img/ihme.png
  - name: Bassem Akoush
    url: https://www.linkedin.com/in/bassem-akoush/
    aff: Stanford University
    image: /assets/img/akoush.png
  - name: Jen Zen Ho
    url: https://au.linkedin.com/in/jen-zen-ho/
    aff: Stanford University
    image: /assets/img/jenzen.png
  - name: Wai Tong Chung
    url: https://waitong94.github.io/
    aff: Stanford University
    image: /assets/img/chung.png
  - name: Walter Reade
    url: https://www.linkedin.com/in/reade/
    aff: Kaggle
    image: /assets/img/reade.png
  - name: Adib Bazgir
    url: https://www.linkedin.com/in/adib-bazgir-698534138
    aff: University of Missouri
    image: /assets/img/bazgir.png

# Office hour hosts: section below appears only when this list is non-empty.
oh_hosts: []
---

## Organizing Committee
{% include team.html id="speakers" %}

{% if page.oh_hosts.size > 0 %}
## Office Hour Hosts
{% include team.html id="oh_hosts" %}
{% endif %}
