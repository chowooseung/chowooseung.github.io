---
title: rigging-workflow1
date: 2025-11-25
description: rigging workflow 에 대한 생각.
tags:
  - rigging-system
  - rigging-workflow
  - rigging
  - data-centric
  - 자동화
  - guidable-rigging-system
  - modular-rigging-system
image: ""
imageAlt: ""
imageOG: false
hideCoverImage: false
hideTOC: false
targetKeyword: ""
draft: false
---
[이전에](posts/rigging-workflow0/index.md) 정리한 항목 중에 다음 두 가지에 대해서 살펴보려 한다.

* asset 단위의 자동화를 달성하려면 무엇이 필요할까?
먼저 여기서 자동화는 rigging 을 원 클릭으로 해주는 마법을 이야기 하지 않는다. 작업한 asset을 언제든지 처음부터 다시 생성할수있는것을 이야기한다. 이것이 중요한 이유는 model이 업데이트 되면 rig 가 변경 사항이 없어도 업데이트 해야 하기 때문이다[^1]. 자동화는 이 업데이트의 시간적 부담을 줄여주고 작업의 일관성을 보장한다. 
자동화를 하는 방법은 간단하게도 모든 것을 스크립트로 작성하면 된다. model을 불러오고, rig를 생성하고, skin을 바인딩하고, PSD를 다시 적용하는 스크립트를 작성해 놓으면 model 업데이트로 낭비되는 시간을 줄일 수 있다. 하지만 이 모든 것을 아무런 도구 없이 작성하려면 asset 하나에 몇 만 줄의 코드가 필요 할 수 있다. 따라서 이 코드를 간단하게 만들어줄 api가 필요하다. 

* data centric workflow 를 달성하기 위한 도구를 만들려면 어떻게 해야 할까? 
Maya 는 scene을 바탕으로 작업을 이어 나간다. 모든 data 는 scene 에 합쳐져 있고 이것은 Maya의 기본적인 작업 흐름이다. data 중심의 작업 방식을 구현하려면 이것을 굳이 굳이 분리 해야 한다. 분리하기 위한 데이터는 Rigging 하는 과정에 따라 조금씩 다를 것이다. 
개인적인 경험 일 수 있지만 보편적으로 Rigging 과정은 Rig - Skin - PSD 순서로 진행된다. 이 외에 좀 더 특별한 작업이 추가 될 수 있지만 그것은 custom scripts 형태로 관리가 가능하다고 생각한다. 이러한 script 또한 data 이다. 따라서 Rig를 생성하기 위한 Guide data, Skin data, PSD(joint, blendshape) data 만 in, out 이 가능하다면 기본적인 rigging workflow 를 감당할 수 있는 도구를 만들 수 있을 것이다.

---
[^1]: 해외는 model 이 업데이트 되면 자동으로 rig 를 붙여서 재 publish 되는 파이프 라인이 있다고 듣긴 했지만 경험해 본 적은 없다. 이러한 파이프 라인도 모든 데이터와 그 관계가 정해져 있기 때문에 가능하다고 추측하고 있다. 
