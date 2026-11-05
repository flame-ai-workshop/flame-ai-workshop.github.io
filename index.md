---
layout: default
# Header fields (title, dates/venue, Register/Flyer links, banner) are set in
# _config.yml under `defaults` -> path "". Override any of them here if needed.

# Speaker cards rendered by {% include team.html id="speakers" %}.
# image: put photos in /assets/img/ ; url: link for the name (flyer PDF, homepage, ...)
# interest: optional italic line (e.g. talk title) under the affiliation.
speakers: []
#  - name: Jane Doe
#    url: /assets/img/speaker_flyer_doe.pdf
#    aff: Professor <br /> Some University
#    interest: '"Talk title"'
#    image: /assets/img/doe.png
---

**Registration for FLAME AI 2027 is open:** [register here]({{ page.register_url }}).

# Mission
To foster a dynamic forum for exchanging ideas, cutting-edge data, advanced methods, and models related to ML techniques for fluid dynamics, turbulence, and environmental science - applications crucial to the development of sustainable energy solutions, climate resilience, wildfire mitigation, and safety systems.

# Agenda
Details for FLAME AI 2027 are coming soon. Previous editions featured:
1. A multi-week **ML challenge** (1-2 person teams) on predicting spatio-temporal and dynamical processes in physical sciences, environmental flows, and engineering with open-source data.
2. **Invited talks and keynote lectures** on cutting-edge trends by AI/ML experts from Stanford, academia, and industry partners in the Greater Silicon Valley ecosystem.

# Invited Speakers
{% if page.speakers.size > 0 %}
{% include team.html id="speakers" %}
{% else %}
Speaker announcements coming soon. In the meantime, see the [2024](/2024/) and [2023](/2023/) editions.
{% endif %}
