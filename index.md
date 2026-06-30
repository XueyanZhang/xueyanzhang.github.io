---
layout: default
---

<div class="profile-section" markdown="1">
<div class="profile-image">
<img src="{{ '/assets/images/profile-photo.jpeg' | relative_url }}" alt="Xueyan Zhang">
</div>
<div class="profile-text" markdown="1">

I am **XYZ**.  
I worked in AI compiler for 3+ yrs.  
I focus on smarter & faster models.

<pre class="stack-tree">
Application
└── Model
    └── Infra
        └── Hardware
            └── Resources
</pre>

<div class="social-icons">
<a href="mailto:xueyanzhang27+githubpages@gmail.com" title="Email"><i class="fas fa-envelope"></i></a>
<a href="https://scholar.google.ca/citations?user=9ZlGB5EAAAAJ&hl=en" title="Google Scholar"><i class="fas fa-graduation-cap"></i></a>
<a href="https://github.com/xueyanzhang" title="GitHub"><i class="fab fa-github"></i></a>
<a href="https://www.linkedin.com/in/xueyanzhang27/" title="LinkedIn"><i class="fab fa-linkedin"></i></a>
<a href="https://x.com/xyz_xueyanz" title="X (Twitter)"><i class="fab fa-twitter"></i></a>
</div>

</div>
</div>

---

<div class="quote-carousel" id="quote-carousel" data-quotes='{{ site.data.quotes | jsonify }}'>
  <blockquote id="quote-text"></blockquote>
</div>

<script>
(function () {
  var el = document.getElementById('quote-carousel');
  var quotes = JSON.parse(el.getAttribute('data-quotes'));
  var textEl = document.getElementById('quote-text');
  var idx = Math.floor(Math.random() * quotes.length);

  function show(i) {
    textEl.style.opacity = 0;
    setTimeout(function () {
      textEl.textContent = quotes[i];
      textEl.style.opacity = 1;
    }, 300);
  }

  show(idx);

  if (quotes.length > 1) {
    setInterval(function () {
      idx = (idx + 1) % quotes.length;
      show(idx);
    }, 6000);
  }
})();
</script>

---

## Publications &nbsp;<span class="pub-toggle">(<a href="javascript:void(0)" id="pub-toggle-selected" onclick="showPubs(0)">show selected</a> / <a href="javascript:void(0)" id="pub-toggle-all" onclick="showPubs(1)">show all</a>)</span>

<div id="pubs-selected" class="pub-list">
{% for pub in site.data.publications %}{% if pub.selected %}<div class="pub-entry">
  <img class="pub-thumb" src="{{ pub.thumb | relative_url }}" alt="paper thumbnail">
  <div class="pub-text">
    <p class="pub-title">{{ pub.title }}</p>
    {% if pub.authors %}<p class="pub-authors">{{ pub.authors }}</p>{% endif %}
    <p class="pub-venue"><em>{{ pub.venue }}</em></p>
    {% if pub.links.size > 0 %}<p class="pub-links">{% for link in pub.links %}{% unless forloop.first %} | {% endunless %}<a href="{{ link.url }}">{{ link.label }}</a>{% endfor %}</p>{% endif %}
  </div>
</div>
{% endif %}{% endfor %}
</div>

<div id="pubs-all" class="pub-list hidden">
{% for pub in site.data.publications %}<div class="pub-entry">
  <img class="pub-thumb" src="{{ pub.thumb | relative_url }}" alt="paper thumbnail">
  <div class="pub-text">
    <p class="pub-title">{{ pub.title }}</p>
    {% if pub.authors %}<p class="pub-authors">{{ pub.authors }}</p>{% endif %}
    <p class="pub-venue"><em>{{ pub.venue }}</em></p>
    {% if pub.links.size > 0 %}<p class="pub-links">{% for link in pub.links %}{% unless forloop.first %} | {% endunless %}<a href="{{ link.url }}">{{ link.label }}</a>{% endfor %}</p>{% endif %}
  </div>
</div>
{% endfor %}
</div>

<script>
function showPubs(id) {
  var selectedList = document.getElementById('pubs-selected');
  var allList = document.getElementById('pubs-all');
  var selectedLink = document.getElementById('pub-toggle-selected');
  var allLink = document.getElementById('pub-toggle-all');
  if (id === 0) {
    selectedList.classList.remove('hidden');
    allList.classList.add('hidden');
    selectedLink.classList.add('active');
    allLink.classList.remove('active');
  } else {
    selectedList.classList.add('hidden');
    allList.classList.remove('hidden');
    allLink.classList.add('active');
    selectedLink.classList.remove('active');
  }
}
showPubs(0);
</script>

---

## Projects

<div class="proj-list">
{% for proj in site.data.projects %}<div class="proj-entry">
  {% if proj.thumb_split %}<div class="proj-thumb proj-thumb-split">
  <img src="{{ proj.thumb_split[0] | relative_url }}" alt="{{ proj.title }} before">
  <img src="{{ proj.thumb_split[1] | relative_url }}" alt="{{ proj.title }} after">
  </div>
  {% elsif proj.carousel %}<div class="proj-thumb proj-thumb-carousel" data-images='{{ proj.carousel | jsonify }}'>
  <img src="{{ proj.carousel[0] | relative_url }}" alt="{{ proj.title }} screenshot">
  </div>
  {% else %}<img class="proj-thumb" src="{{ proj.thumb | relative_url }}" alt="project thumbnail">
  {% endif %}
  <div class="proj-text">
    <p class="proj-title">{% if proj.url and proj.url != "" %}<a href="{{ proj.url }}"><strong>{{ proj.title }}</strong></a>{% else %}<strong>{{ proj.title }}</strong>{% endif %}</p>
    <p class="proj-tagline"><em>{{ proj.tagline }}</em></p>
    {% for line in proj.lines %}<p class="proj-line">{{ line }}</p>{% endfor %}
  </div>
</div>
{% endfor %}
</div>

<script>
(function () {
  var carousels = document.querySelectorAll('.proj-thumb-carousel');
  carousels.forEach(function (el) {
    var images = JSON.parse(el.getAttribute('data-images'));
    var img = el.querySelector('img');
    var idx = 0;
    if (images.length > 1) {
      setInterval(function () {
        idx = (idx + 1) % images.length;
        img.src = images[idx];
      }, 2200);
    }
  });
})();
</script>
