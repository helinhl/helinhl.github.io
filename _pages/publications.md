---
layout: page
permalink: /publications/
title: Publications
description: 
conf-years: [2023, 2022, 2021, 2020, 2019, 2017]
jrnl-years: [2023, 2022, 2021, 2018, 2015]
pat-years: [2021, 2020, 2016, 2015]
nav: true
---
Copy Right Notice: The materials presented below are for academic use only. Copyright and all rights therein are retained by the authors or by the respective copyright holders.

[[Conference papers](#conference-papers)] | [[Journal & Magazine papers](#journal--magazine-papers)] | [[Patents](#patents)]


#### Conference papers
<sup>#</sup> indicates the corresponding author.
<div class="publications">

{% for y in page.conf-years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f confs -q @*[year={{y}}]* %}
{% endfor %}

</div>

<br/>

#### Journal & Magazine papers
<sup>#</sup> indicates the corresponding author.
<div class="publications">

{% for y in page.jrnl-years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f journal -q @*[year={{y}}]* %}
{% endfor %}

</div>

<br/>

#### Patents
<div class="publications">

{% for y in page.pat-years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f patent -q @*[year={{y}}]* %}
{% endfor %}

</div>

