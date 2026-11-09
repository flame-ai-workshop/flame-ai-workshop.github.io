---
layout: default

speakers:
  - name: Prof. Matthias Ihme
    url: https://www.linkedin.com/in/matthias-ihme-47ba974/
    aff: Stanford University, SLAC
    image: /assets/img/ihme.png
  - name: Karl Toepperwien
    url: https://www.linkedin.com/in/karl-toepperwien-14a623252/
    aff: Stanford University
    image: /assets/img/toepperwien.png
  - name: Ben Krisna
    url: https://www.linkedin.com/in/benyamin-krisna-822ab9141/
    aff: Stanford University
    image: /assets/img/krisna.png
  - name: Blake Andersen
    url: https://www.linkedin.com/in/blake-c-andersen
    aff: Stanford University
    image: /assets/img/andersen.png

# Office hour hosts: section below appears only when this list is non-empty.
oh_hosts: []
---

## Organizing Committee
{% include team.html id="speakers" columns=2 %}

{% if page.oh_hosts.size > 0 %}
## Office Hour Hosts
{% include team.html id="oh_hosts" %}
{% endif %}
