---
layout: page
title: EQM Global
subtitle: The global egalitarian economy campaign.
css:
  - "/assets/css/eqm-campaign.css"
---

<span class="eqm-eyebrow">Global premiere · 11/11</span>

<p class="eqm-lead">The premiere is global. It hits the U.S. at 11:11am EST on Wednesday, 11/11.</p>

<!-- PLACEHOLDER: short intro to the campaign, in Lelio's words. -->

<div class="eqm-panel eqm-country-picker">
  <label for="eqm-country-select">Find your country</label>
  <select id="eqm-country-select">
    <option value="">Choose a country</option>
    {% for c in site.data.global_countries %}
    <option value="{{ c.slug }}">{{ c.name }}</option>
    {% endfor %}
  </select>

  <div id="eqm-country-list">
    {% for c in site.data.global_countries %}
    <section class="eqm-country" id="{{ c.slug }}" data-country="{{ c.slug }}">
      <h3>{{ c.name }}</h3>
      {% if c.language and c.language != "" %}<p><b>Language:</b> {{ c.language }}</p>{% endif %}
      {% if c.channel and c.channel != "" %}
      <p><a class="eqm-button" href="{{ c.channel }}" target="_blank" rel="noopener">Watch in {{ c.name }}</a></p>
      {% else %}
      <p class="eqm-soon">Channel coming soon.</p>
      {% endif %}
    </section>
    {% endfor %}
  </div>
</div>

<p>Don't see your country? More are on the way. Email <a href="mailto:build@eqm.systems">build@eqm.systems</a> or call or text (929) 481-0340.</p>

<p><a href="/stewards">Join the team</a></p>

<script>
(function () {
  var select = document.getElementById("eqm-country-select");
  var items = document.querySelectorAll("#eqm-country-list .eqm-country");
  if (!select || !items.length) return;
  function show(slug) {
    items.forEach(function (el) { el.hidden = !slug || el.dataset.country !== slug; });
    select.value = slug || "";
  }
  select.addEventListener("change", function () {
    show(select.value);
    try { history.replaceState(null, "", select.value ? "#" + select.value : location.pathname); } catch (e) {}
  });
  window.addEventListener("hashchange", function () { show(location.hash.slice(1)); });
  show(location.hash.slice(1));
})();
</script>
