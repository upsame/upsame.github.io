---
layout: page
title: FPGA系列文章
titlebar: FPGA
subtitle: <span class="mega-octicon octicon-clippy"></span>&nbsp;&nbsp; 专业分站 <a href ="http://bc2.net/" target="_blank" ><font color="#EB9439">FPGA博客网</font></a>
menu: fpga
css: ['blog-page.css']
permalink: /fpga
---

<div class="row">

    <div class="col-md-12">

        <ul id="posts-list">
            {% for post in site.posts %}
                {% if post.category=='FPGA' or post.keywords contains 'FPGA' %}
                <li class="posts-list-item">
                    <div class="posts-content">
                        <span class="posts-list-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
                        <a class="posts-list-name bubble-float-left" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
                        <span class='circle'></span>
                    </div>
                </li>
                {% endif %}
            {% endfor %}
        </ul> 

        <!-- Pagination -->
        {% include pagination.html %}

        <!-- Comments -->
       <div class="comment">
         {% include comments.html %}
       </div>
    </div>

</div>
<script>
    $(document).ready(function(){

        // Enable bootstrap tooltip
        $("body").tooltip({ selector: '[data-toggle=tooltip]' });

    });
</script>