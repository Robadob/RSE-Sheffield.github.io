---
title: Active Projects
permalink: /service/projects/active
type: text
---

<style>
    .active {
        padding: 10px;
        border: 1px solid gray;
        margin: 10px;
        }   
    .completed {
        color: #656565;
        background-color: WhiteSmoke;
        padding: 10px;
        border: 1px solid gray;
        margin: 10px;
    }    
</style>

Some projects we are currently working on (not a comprehensive list):

{% assign levels = site.data.projects | where: 'show',1 | group_by: 'level' | sort: 'name' %}
{% assign project_descriptions = site.project_descriptions %}
{% assign today_date = 'now' | date: '%s' %}

<div class="current-project-list">
    {% for level in levels %}
        {% assign projects = level.items | sort:'title' %}
        {% for project in projects %}
        {% assign project_end_date = project.end | date: '%s' %}
        {% if project_end_date >= today_date or project.end == undefined %}
            <div class="{% if current %}active{% else %}completed{% endif %}">
                <b>{{project.long_title}} </b>
                    (Active project)
                <hr/>
                {{project.start}} - {{project.end}}
                <br/>
                Collaborating with: <em>{{project.department}}</em>
                <br/>
                Technology and methods: <em>{{project.tech_methods}}</em>
                <br/>
                RSEs involved: <em>{{project.rses}}</em>
                <hr/>
                {% for project_description in project_descriptions %}
                    {% if project_description.key == project.key %}                    
                        <br/>
                        {{project_description.content}}
                    {% endif %}
                {% endfor %}            
            </div>
        {% endif %}
        {% endfor %}
        <hr/>
    {% endfor %}
</div>

