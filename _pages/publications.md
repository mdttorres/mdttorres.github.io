---
layout: page
permalink: /publications/
title: publications
description: >
  Peer-reviewed articles, book chapters, and editorials, newest first.
  Name in <strong>bold</strong>; <u>underline</u> = first / co-first authorship; * = co-corresponding.
nav: true
nav_order: 2
---

<style>
.mdt-filterbar{display:flex;flex-wrap:wrap;gap:8px;align-items:center;margin:.5rem 0 .3rem;padding:14px 0;
  position:sticky;top:64px;z-index:20;background:var(--global-bg-color);border-bottom:1px solid var(--global-divider-color);}
.mdt-fbtn{font-size:.82rem;font-weight:500;padding:6px 13px;border-radius:999px;cursor:pointer;
  border:1px solid var(--global-divider-color);color:var(--global-text-color);background:transparent;transition:all .15s ease;}
.mdt-fbtn:hover{border-color:var(--global-theme-color);}
.mdt-fbtn.on{background:var(--global-theme-color);border-color:var(--global-theme-color);color:#fff;font-weight:600;}
.mdt-search{margin-left:auto;}
.mdt-search input{background:transparent;border:1px solid var(--global-divider-color);color:var(--global-text-color);
  padding:7px 13px;border-radius:999px;font-size:.85rem;min-width:190px;outline:none;}
.mdt-search input:focus{border-color:var(--global-theme-color);}
.mdt-count{opacity:.6;font-size:.82rem;margin:12px 0 4px;}
</style>

<div id="mdt-filter" class="mdt-filterbar">
  <button class="mdt-fbtn on" data-f="all">All</button>
  <button class="mdt-fbtn" data-f="ai">AI & deep learning</button>
  <button class="mdt-fbtn" data-f="amp">AMP design & SAR</button>
  <button class="mdt-fbtn" data-f="chem">Peptide chemical modification</button>
  <button class="mdt-fbtn" data-f="sensor">Biosensors & diagnostics</button>
  <button class="mdt-fbtn" data-f="malaria">Antimalarial peptide-hormones</button>
  <button class="mdt-fbtn" data-f="nano">Nanomaterials & delivery</button>
  <span class="mdt-search"><input id="mdt-search" type="search" placeholder="Search title / author…"></span>
</div>
<div class="mdt-count" id="mdt-count"></div>

<div class="publications">

{% bibliography %}

</div>

<script>
(function(){
  var KEYS={"torres2026deep":"ai amp","deb2026computat":"ai amp chem","yagati2026colorime":"sensor","torres2026generati":"ai","kalimuthu2026design":"amp","gaglione2026discover":"ai","maus2025covering":"ai","jones2025dataset":"ai","beckmaniv2025molecula":"amp","levya2025key":"amp","bosso2025explorin":"ai amp","torres2025generati":"ai","torres2025discover":"ai","guan2025venomics":"ai","amponnawarat2025syntheti":"amp","wan2025accelera":"ai","ageitos2025frog":"amp","torres2024encrypte":"ai amp","torres2024human":"ai amp","deb2024computat":"ai amp chem","santosjunior2024computat":"ai","wan2024molecula":"ai","delossantos2024polyprol":"amp","reffuveille2024antibiof":"amp","araujo2024low":"sensor","silva2024syntheti":"malaria","nazarianfiro2023recombin":"amp chem","chiloeches2023synergis":"amp nano","cesaro2023deep":"ai","maasch2023molecula":"ai amp","averbeck2023stabilit":"nano","pedron2023molecula":"chem","boaro2023rational":"amp","lima2023rapid":"sensor","ageitos2022biologic":"amp","torres2022molecula":"amp","cardoso2022asparagi":"amp","daniell2022debulkin":"sensor nano","arque2022autonomo":"amp nano","torres2022detectio":"sensor","cesaro2022syntheti":"ai","torres2022mining":"ai amp","lopes2021color":"sensor","oliveira2021syntheti":"amp","lima2021minute":"sensor","meurer2021antimicr":"amp","torres2021low":"sensor","palmer2021molecula":"amp","torres2021syntheti":"amp","silveira2021anti":"amp","pedron2021net":"amp malaria","torres2021ionic":"nano","boaro2020light":"amp","ahmed2020syntheti":"amp","silva2020repurpos":"amp","pedron2020arg":"amp malaria","echeverria2020physical":"nano","mercer2020antimicr":"amp","freire2020wasp":"amp malaria","torres2020wasp":"amp malaria","silva2020simple":"sensor","cruz2020photoche":"amp nano","torres2019reprogra":"amp","yehl2019engineer":"amp","agbale2019antimicr":"amp","oshiro2019computer":"amp","pedron2019effect":"amp","pedron2019repurpos":"amp","cndido2019short":"amp","fensterseife2019selectiv":"amp","torres2019toward":"amp","torres2019peptide":"amp","torres2018structur":"amp","cardoso2018computat":"ai amp","boase2018polynitr":"amp","pane2018identifi":"ai amp","porto2018silico":"ai amp chem","pizzo2018novel":"amp","torres2018natural":"amp","torres2018peptide":"amp malaria","cao2018yeast":"amp","pedron2018anticanc":"amp","delafuentenu2018magnetic":"amp nano","pedron2017novel":"amp","torres2017decorali":"amp","delafuentenu2017next":"amp","silva2017angioten":"chem malaria","torres2017antimicr":"amp","torres2016evidence":"malaria","torres2015angioten":"malaria","torres2015highly":"malaria","silva2015effects":"malaria","silva2015new":"malaria","silva2015anti":"malaria","silva2014antiplas":"malaria","torres2014importan":"malaria","ferreira2014effects":"malaria","chamlian2013study":"malaria","cesaro2022methods":"amp","silva2016pept":"amp","torres2016antimicr":"amp","torres2014intera":"amp","lopez2022special":"amp","torres2021special":"amp"};
  function ready(fn){document.readyState!='loading'?fn():document.addEventListener('DOMContentLoaded',fn);}
  ready(function(){
    var pub=document.querySelector('.publications'); if(!pub) return;
    var lis=pub.querySelectorAll('ol.bibliography > li');
    lis.forEach(function(li){var idEl=li.querySelector('[id]');li.setAttribute('data-topics',(idEl&&KEYS[idEl.id])?KEYS[idEl.id]:'');});
    var bar=document.getElementById('mdt-filter'),search=document.getElementById('mdt-search'),current='all';
    function apply(){
      var q=(search&&search.value||'').toLowerCase().trim(),shown=0;
      lis.forEach(function(li){
        var t=' '+(li.getAttribute('data-topics')||'')+' ';
        var okT=current==='all'||t.indexOf(' '+current+' ')>=0;
        var okQ=!q||li.textContent.toLowerCase().indexOf(q)>=0;
        var vis=okT&&okQ; li.style.display=vis?'':'none'; if(vis)shown++;
      });
      pub.querySelectorAll('h2.bibliography').forEach(function(h){
        var ol=h.nextElementSibling,visible=false;
        if(ol&&ol.tagName==='OL'){ol.querySelectorAll(':scope > li').forEach(function(li){if(li.style.display!=='none')visible=true;});}
        h.style.display=visible?'':'none'; if(ol&&ol.tagName==='OL')ol.style.display=visible?'':'none';
      });
      var c=document.getElementById('mdt-count'); if(c)c.textContent=shown+' publication'+(shown===1?'':'s')+' shown';
    }
    if(bar)bar.addEventListener('click',function(e){var b=e.target.closest('.mdt-fbtn');if(!b)return;current=b.getAttribute('data-f');bar.querySelectorAll('.mdt-fbtn').forEach(function(x){x.classList.toggle('on',x===b);});apply();});
    if(search)search.addEventListener('input',apply);
    apply();
  });
})();
</script>
