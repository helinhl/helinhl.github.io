---
layout: page
permalink: /publications/
title: Publications
description: The materials presented below are for academic use only. Copyright and all rights therein are retained by the authors or by the respective copyright holders.<br><sup>#</sup> indicates the corresponding author.
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->


<!-- {% include bib_search.liquid %} -->



[[Books](#books)] [[Conference papers](#conference-papers)] [[Journal & Magazine papers](#journal--magazine-papers)] [[Posters & Demos](#posters--demos)] [[Patents](#patents)]
<br/>

<!-- 仅显示选中标签的区域 -->
<div id="tag-filter-container" class="tag-filter-container" style="margin: 1rem 0; padding: 1rem;">
  <div id="selected-tags" style="display: flex; flex-wrap: wrap; gap: 0.5rem;">
    <!-- 选中的标签会在这里显示 -->
  </div>
</div>

<script>
// 存储当前选中的标签
let selectedTags = new Set();

// 页面加载完成后初始化
document.addEventListener('DOMContentLoaded', function() {
  // 为所有标签添加点击事件
  document.querySelectorAll('.publication-tags .tag').forEach(tag => {
    tag.addEventListener('click', function(e) {
      e.preventDefault();
      const tagText = this.textContent.trim();
      
      // 切换标签选中状态
      if (selectedTags.has(tagText)) {
        selectedTags.delete(tagText);
      } else {
        selectedTags.add(tagText);
      }
      
      // 更新筛选状态和显示
      updateTagFilterUI();
      filterPublications();
    });
    
    // 添加上手提示样式
    tag.style.cursor = 'pointer';
  });
});

// 更新标签筛选UI（仅显示选中标签，无文字提示）
function updateTagFilterUI() {
  const selectedTagsContainer = document.getElementById('selected-tags');
  
  // 清空现有选中标签
  selectedTagsContainer.innerHTML = '';
  
  // 添加选中的标签
  selectedTags.forEach(tag => {
    const tagElement = document.createElement('span');
    tagElement.className = 'tag selected-tag';
    tagElement.style.display = 'flex';
    tagElement.style.alignItems = 'center';
    tagElement.style.gap = '0.3rem';
    
    // 复制原始标签样式
    const sampleTag = Array.from(document.querySelectorAll('.publication-tags .tag'))
      .find(t => t.textContent.trim() === tag);
    
    if (sampleTag) {
      const computedStyle = window.getComputedStyle(sampleTag);
      tagElement.style.backgroundColor = computedStyle.backgroundColor;
      tagElement.style.color = computedStyle.color;
      tagElement.style.padding = computedStyle.padding;
      tagElement.style.borderRadius = computedStyle.borderRadius;
      tagElement.style.fontSize = computedStyle.fontSize;
    }
    
    tagElement.innerHTML = `${tag} <span style="cursor: pointer; font-weight: bold;">×</span>`;
    
    // 为关闭按钮添加事件
    tagElement.querySelector('span').addEventListener('click', function(e) {
      e.stopPropagation();
      selectedTags.delete(tag);
      updateTagFilterUI();
      filterPublications();
    });
    
    selectedTagsContainer.appendChild(tagElement);
  });
}

// 筛选论文并处理类别和年份显示
function filterPublications() {
  // 获取所有分类容器
  const categoryContainers = document.querySelectorAll('.publications');
  
  categoryContainers.forEach(container => {
    // 处理论文条目显示
    const pubsInCategory = container.querySelectorAll('.row');
    let hasVisiblePubInCategory = false;

    pubsInCategory.forEach(pub => {
      const pubTags = new Set();
      pub.querySelectorAll('.publication-tags .tag').forEach(tag => {
        pubTags.add(tag.textContent.trim());
      });

      // 判断是否匹配选中的标签
      const shouldShow = selectedTags.size === 0 || 
        Array.from(selectedTags).every(tag => pubTags.has(tag));

      // 控制论文显示
      pub.style.display = shouldShow ? '' : 'none';
      if (shouldShow) {
        hasVisiblePubInCategory = true;
      }
    });

    // 处理类别标题显示
    const categoryTitle = container.previousElementSibling;
    if (categoryTitle && categoryTitle.tagName === 'H4') {
      categoryTitle.style.display = hasVisiblePubInCategory ? '' : 'none';
    }
    container.style.display = hasVisiblePubInCategory ? '' : 'none';

    // 处理年份显示
    if (hasVisiblePubInCategory) {
      handleYearHeadings(container);
    }
  });
}

// 处理年份标题的显示
function handleYearHeadings(container) {
  const visibleYears = new Set();
  container.querySelectorAll('.row:not([style*="display: none"])').forEach(pub => {
    const periodical = pub.querySelector('.periodical');
    if (periodical) {
      const yearMatch = periodical.textContent.match(/\b20\d{2}\b/);
      if (yearMatch) {
        visibleYears.add(yearMatch[0]);
      }
    }
  });

  const yearHeadings = container.querySelectorAll('h2, .year');
  yearHeadings.forEach(heading => {
    const yearText = heading.textContent.trim().match(/\b20\d{2}\b/)?.[0];
    if (yearText) {
      heading.style.display = visibleYears.has(yearText) ? '' : 'none';
    }
  });
}
</script>

#### Books
<div class="publications">

{% bibliography -f book %}

</div>
<br/>


#### Conference papers
<div class="publications">

{% bibliography -f confs %}

</div>
<br/>


#### Journal & Magazine papers
<div class="publications">

{% bibliography -f journal %}

</div>
<br/>


#### Posters & Demos
<div class="publications">

{% bibliography -f poster %}

</div>
<br/>


#### Patents
<div class="publications">

{% bibliography -f patent %}

</div>
