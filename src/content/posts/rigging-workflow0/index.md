---
title: rigging-workflow0
date: 2025-11-22
description: rigging workflow 에 대한 생각.
tags:
  - rigging-workflow
  - rigging-system
image:
imageAlt:
imageOG: false
hideCoverImage: false
hideTOC: false
targetKeyword: ""
draft: false
---
[https://bindpose.com/rigging-systems-reusability-modularity-extensibility/](https://bindpose.com/rigging-systems-reusability-modularity-extensibility/)

위 글은 입사하고 얼마 지나지 않은 1년, 2년 정도에 보게 된 글이다. 그 당시에 나는 작업 보다 R&D를 주로 하는 역할로 팀 내에서 사용할 biped, quadruped rigging system 을 만드는 중 이었다. 그때 만들어야 했던 rigging system 에 대한 검색을 하다가 [위 글](https://bindpose.com/rigging-systems-reusability-modularity-extensibility/)을 보게 되었고, 내가 만들고 있던 것이 guidable(링크된 글의 작성자도 임의로 붙인 이름인 것 같다)이라는 rigging system 의 한 종류라는 것을 알았다. 그 당시에 만들던 rigging system 은 현재 가지고 있지 않지만 [이것](https://www.perryleijten.com/en/works/rigPlacement)과 비슷했다. 

이 당시에 나는 guidable rigging system 를 scripting을 하지 않거나 덜 할 수 있는 장점이 있다고 생각하고 있었다. 하지만 이것은 작업을 거의 하지 않은 내 착각이었고 실제 작업 시에는 script 를 안 쓸 수 없다는 것을 뒤늦게 알았다. asset 마다 요구 사항이 다르고 추가 작업이 필요하다. 하지만 guidable rigging system 은 이런 개별 요구 사항까지 포함하기는 힘들었다.

guidable rigging system 은 실제 작업하는 것은 굉장히 편했으나 그것을 완성하기까지 과정이 너무 힘들고 디버깅이 쉽지 않았다. 잘못된 부분을 확인하는 것도 힘들지만 그것이 반복 적으로 사용 될 때 일괄 수정이 매우 힘들었다. 

이후에는 [글](https://bindpose.com/rigging-systems-reusability-modularity-extensibility/)에 언급된 [mgear](https://www.mgear-framework.com/) 를 찾아보기 시작했다. mgear 는 data centric workflow를 중심으로 하는 철학으로 rigging에 필요한 전체 기능을 제공하는 framework 이다. scene이 아닌 guide를 기반으로 하는 데이터로부터 리그를 생성하는 workflow 는 scene 에 종속되지 않고 이전으로 돌아가 문제를 해결 할 수 있었으며, custom scripts를 사용해서 modular rigging system 에서 지원하는 범위 밖의 `asset 당 자동화`를 달성 할 수 있었다. 

하지만 mgear 역시 불편한 점이 있었는데 rig가 없는 guide 상태에서 작업을 하기 때문에 rig 를 확인하기 위해 build 를 반복해야 한다는 점이었다. 이것은 build가 얼마 걸리지 않을 때는 아무 문제가 되지 않았지만 rig를 build 하는데 10분이 넘어가는 asset을 작업할 때 굉장히 문제가 되었다. 그리고 외부 플러그인을 강제로 쓸 수 밖에 없다는 점. modular rigging system 을 수정하기 위해선 코드를 수정해야 하는데 오픈소스로 개발이 진행 중인 프로젝트라 수정 + 업데이트를 모두 관리해야 한다는 점. custom script 의 버전 관리가 자동으로 되지 않는 점. 

결국 현재는 rigging workflow 를 확립하는데 다음 항목을 고려하게 되었다.
1. asset 당 자동화
2. data centric workflow
3. modular rigging system
4. guidable rigging system 
5. build 속도 향상
6. guide version 이 올라감에 따라 custom scripts, skin data, shape delta 등의 버전 관리
7. 전체 코드 베이스를 모두 관리 할 수 있어야 함.