---
layout: landing
title: Årsmöten
nav-menu: true
nav-order: 6
show_tile: true
description: Handlingar och protokoll från föreningens årsmöten.
image: assets/images/pic09.jpg
---

<div class="spotlights">
{% for meeting in site.data.annual_meetings %}
  <section>
    <div class="content">
      <div class="inner">
        <h3>{{ meeting.year }}</h3>
        <ul style="list-style: none; padding: 0; margin: 0;">
          {% assign docs = meeting.documents %}
          
          {% if docs.invitation %}
            <li style="margin: 8px 0;">
              {% if docs.invitation == "pending" %}
                <span style="opacity: 0.5;"><i class="fa fa-envelope" style="margin-right: 8px; width: 16px;"></i>Kallelse</span>
              {% else %}
                <a href="{{ docs.invitation | relative_url }}" target="_blank" style="color: inherit; text-decoration: none;">
                  <strong><i class="fa fa-envelope" style="margin-right: 8px; width: 16px;"></i>Kallelse</strong>
                </a>
              {% endif %}
            </li>
          {% endif %}
          
          {% if docs.activity_report %}
            <li style="margin: 8px 0;">
              {% if docs.activity_report == "pending" %}
                <span style="opacity: 0.5;"><i class="fa fa-file-text" style="margin-right: 8px; width: 16px;"></i>Verksamhetsberättelse</span>
              {% else %}
                <a href="{{ docs.activity_report | relative_url }}" target="_blank" style="color: inherit; text-decoration: none;">
                  <strong><i class="fa fa-file-text" style="margin-right: 8px; width: 16px;"></i>Verksamhetsberättelse</strong>
                </a>
              {% endif %}
            </li>
          {% endif %}
          
          {% if docs.business_plan %}
            <li style="margin: 8px 0;">
              {% if docs.business_plan == "pending" %}
                <span style="opacity: 0.5;"><i class="fa fa-file-text" style="margin-right: 8px; width: 16px;"></i>Verksamhetsplan</span>
              {% else %}
                <a href="{{ docs.business_plan | relative_url }}" target="_blank" style="color: inherit; text-decoration: none;">
                  <strong><i class="fa fa-file-text" style="margin-right: 8px; width: 16px;"></i>Verksamhetsplan</strong>
                </a>
              {% endif %}
            </li>
          {% endif %}
          
          {% if docs.selection_committee %}
            <li style="margin: 8px 0;">
              {% if docs.selection_committee == "pending" %}
                <span style="opacity: 0.5;"><i class="fa fa-users" style="margin-right: 8px; width: 16px;"></i>Valberedningens förslag</span>
              {% else %}
                <a href="{{ docs.selection_committee | relative_url }}" target="_blank" style="color: inherit; text-decoration: none;">
                  <strong><i class="fa fa-users" style="margin-right: 8px; width: 16px;"></i>Valberedningens förslag</strong>
                </a>
              {% endif %}
            </li>
          {% endif %}
          
          {% if docs.protocol %}
            <li style="margin: 8px 0;">
              {% if docs.protocol == "pending" %}
                <span style="opacity: 0.5;"><i class="fa fa-check-circle" style="margin-right: 8px; width: 16px;"></i>Mötesprotokoll</span>
              {% else %}
                <a href="{{ docs.protocol | relative_url }}" target="_blank" style="color: inherit; text-decoration: none;">
                  <strong><i class="fa fa-check-circle" style="margin-right: 8px; width: 16px;"></i>Mötesprotokoll</strong>
                </a>
              {% endif %}
            </li>
          {% endif %}
        </ul>
      </div>
    </div>
  </section>
{% endfor %}
</div>
