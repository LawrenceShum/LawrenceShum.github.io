---
title: 'Home'
date: 2023-10-24
type: landing
sections:
  - block: resume-biography
    content:
      # The user's folder name in content/authors/
      username: admin
    design:
      spacing:
        padding: [0, 0, 0, 0]
      biography:
        style: 'text-align: justify; font-size: 0.8em;'
  - block: Experience
    id: experience
    content:
      title: Experience
      filters:
        folders:
          - experience
  - block: collection
    id: papers
    content:
      title: Publications
      filters:
        folders:
          - publication
    design:
      view: citation
---
