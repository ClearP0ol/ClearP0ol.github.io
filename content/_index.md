---
# Leave the homepage title empty to use the site title
title: ''
summary: ''
type: landing

sections:
  - block: resume-biography-3
    content:
      # Choose the profile stored in data/authors/<username>.yaml
      username: me
      text: ''
      # Show a call-to-action button under your biography? (optional)
      button:
        text: Download CV
        url: uploads/cv.pdf
      headings:
        about: ''
        education: ''
        interests: ''
    design:
      show_status: false # Hide the status icon at the bottom-right of the avatar
      css_class: profile-first-screen
      spacing:
        # The biography block manages its spacing within the first screen.
        padding: ['0', '0', '0', '0']
      # Use the new Gradient Mesh which automatically adapts to the selected theme colors
      background:
        gradient_mesh:
          enable: true

      # Name heading sizing to accommodate long or short names
      name:
        size: md # Options: xs, sm, md, lg (default), xl

      # Avatar customization
      avatar:
        size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
        shape: circle # Options: circle (default), square, rounded
        width: 300 # Display width in pixels; overrides the size preset
        height: 300 # Display height in pixels; square framing for a circular avatar
        position_x: 80 # Horizontal photo alignment: 0=left, 50=center, 100=right
        position_y: 40 # Vertical crop position: 0=top, 50=center, 100=bottom; overrides anchor
        zoom: 0.85 # Scale the photo inside its frame: 1=original, 0.85=15% smaller
  - block: markdown
    content:
      title: '📚 My Research'
      subtitle: ''
      text: |-
        Wating to explore...
    design:
      columns: '1'
      css_class: compact-research
      spacing:
        padding: ['32px', '0', '24px', '0']
  - block: collection
    id: papers
    content:
      title: Featured Publications
      # Remove this placeholder when adding your own featured publications.
      text: 'No publications yet.'
      filters:
        folders:
          - publications
        featured_only: true
    design:
      view: article-grid
      columns: 2
      spacing:
        padding: ['32px', '0', '24px', '0']
  - block: dated-list
    id: news
    content:
      title: Recent News
      # News entries are shared with /news/ through data/news.yaml.
      data_file: news
    design:
      spacing:
        padding: ['0', '0', '24px', '0']
  - block: dated-list
    id: honors
    content:
      title: Honors & Awards
      # Add awards here in reverse chronological order.
      items:
        - date: '2025-12'
          text: 'First-Class University Scholarship (**Top 5%**).'
        - date: '2024-11'
          text: >-
            **Bronze Medal(1st place)**, 49th International Collegiate Programming Contest (ICPC)
            Asia Regional Contest, Shanghai Site.
        - date: '2024-10'
          text: >-
            **Silver Medal (7th place)**, 2024 China Collegiate Programming Contest (CCPC),
            Jinan Site.
        - date: '2017–2022'
          text: >-
            Multiple **Provincial First Prizes** in both NOIP (Senior Division) and CSP-S.
    design:
      spacing:
        padding: ['48px', '0', '64px', '0']
---
