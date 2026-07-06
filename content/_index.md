---
title: '함명인 간사 홈페이지'
date: 2026-07-02
type: landing

sections:
  - block: hero
    id: top
    content:
      title: "하나님의 자녀로, 영혼 구원의 사명을 따라 헌신하는 함명인 간사입니다."
      text: "영혼을 천하보다 귀하게 여기시는 주님의 마음으로, 뉴저지 땅에서 낙심하고 길 잃은 이들의 신실한 동역자가 되겠습니다."
      primary_action:
        text: "사역 및 돌봄 문의하기"
        url: "#contact"
        icon: hero/paper-airplane
        style: gradient
    design:
      spacing:
        padding: ["6rem", 0, "6rem", 0]
      background:
        color: "#f5f2eb" /* Warm beige background */
        gradient:
          type: radial
          start: "rgba(90, 115, 86, 0.15)" /* Sage green glow */
          end: "transparent"
          position: "50% -10%"
          shape: ellipse
          size: "80% 80%"

  - block: cta-image-paragraph
    id: about
    content:
      items:
        - title: '"땅끝까지 이르러 증인되리라" (사도행전 1:8)'
          text: |
            예수 그리스도의 사랑을 품고 뉴저지 땅에서 한 영혼, 한 영혼을 돌보는 함명인 간사입니다.
            
            신학적 소양을 바탕으로 교회의 일반 사역을 신실하게 감당하며, 낙심하고 길 잃은 이들에게 복음의 기쁜 소식을 전하고 있습니다.
            
            '땅끝까지 이르러 증인되리라'는 말씀을 삶으로 증명해 내는 신실한 동역자가 되기를 소망합니다.
          image: "about-profile.jpg"
    design:
      spacing:
        padding: ["5rem", 0, "5rem", 0]
      css_class: "bg-white"

  - block: features
    id: strengths
    content:
      title: "사역적 강점 및 은사"
      subtitle: "주님께서 주신 아름다운 달란트"
      items:
        - name: "경청과 공감"
          icon: hero/chat-bubble-left-right
          description: "영혼들의 아픔과 이야기에 진심으로 귀를 기울이는 마음"
        - name: "신실한 기도"
          icon: hero/hand-raised
          description: "성도님들과 소외된 이웃들을 향한 끊임없는 중보기도"
        - name: "따뜻한 환대"
          icon: hero/heart
          description: "교회에 처음 발걸음을 한 이들을 조건 없이 품어주는 사랑"
    design:
      columns: 3
      spacing:
        padding: ["5rem", 0, "5rem", 0]
      css_class: "bg-gray-50/50"

  - block: features
    id: ministry
    content:
      title: "사역 (Ministry)"
      subtitle: "한 영혼을 천하보다 귀하게 여기는 현장"
      items:
        - name: "잃어버린 영혼을 위한 '전도 사역'"
          icon: hero/share
          description: "뉴저지 지역 사회 속에서 복음을 듣지 못한 이들을 찾아가 예수 그리스도의 사랑과 기쁜 소식을 전합니다."
        - name: "한 영혼을 천하보다 귀하게 여기는 '돌봄/심방 사역'"
          icon: hero/user-group
          description: "낙심하고 위로가 필요한 교우들과 이웃들을 세심하게 살피며, 예수님의 마음으로 귀를 기울이고 함께 기도합니다."
    design:
      columns: 2
      spacing:
        padding: ["5rem", 0, "5rem", 0]
      css_class: "bg-white"

  - block: steps
    id: timeline
    content:
      title: "사역 이력"
      subtitle: "복음의 증인으로 걸어온 발자취"
      items:
        - title: "현재"
          text: "미국 뉴저지 아이하나 교회 사역 간사 (전도 및 돌봄 사역 담당)"
          icon: hero/briefcase
        - title: "이전"
          text: "신학교 졸업 및 교회의 일반 사역 (잃어버린 영혼의 구원을 위한 헌신)"
          icon: hero/academic-cap
    design:
      layout: horizontal
      spacing:
        padding: ["5rem", 0, "5rem", 0]
      css_class: "bg-gray-50/50"

  - block: collection
    id: blog
    content:
      title: "사역 묵상 / 글 (Blog)"
      subtitle: "사역 현장의 생생한 동행과 은혜의 기록"
      text: "함명인 간사의 신앙 고백과 말씀 묵상, 사역 일지를 나눕니다."
      query:
        collection: blog
        count: 4
    design:
      view: card
      columns: 2
      spacing:
        padding: ["5rem", 0, "5rem", 0]
      css_class: "bg-white"

  - block: contact
    id: contact
    content:
      title: "연락처 / 문의"
      subtitle: "함께 동역하고 기도하겠습니다"
      text: |
        사역 현장을 향한 동역, 돌봄과 위로가 필요한 영혼들의 발걸음을 기다립니다.
        
        나누고 싶은 말씀이나 함께 기도하고 싶은 제목이 있다면 편하게 남겨주세요.
    design:
      spacing:
        padding: ["5rem", 0, "5rem", 0]
      css_class: "bg-gray-50/50"
---
