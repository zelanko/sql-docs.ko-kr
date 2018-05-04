---
title: 소스 제어에서 SQL 작업 Studio (미리 보기) | Microsoft Docs
description: SQL 작업 Studio (미리 보기)에서 소스 제어를 구성 하는 방법에 알아봅니다.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58475a1c7bfb27f29c1e040de286c82d9c7a204f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>소스 제어에서 사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 버전/소스 제어에 Git를 지원합니다.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>에 Git 지원 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 하지만 Git 소스 제어 관리자 (SCM)과 함께 제공 되며 계속 해야 [Git 설치 (버전 2.0.0 이상)](https://git-scm.com/download) 전에 이러한 기능을 사용할 수 있습니다. 



## <a name="open-an-existing-git-repository"></a>기존 Git 저장소를 엽니다.

1. 아래는 **파일** 메뉴 선택 **폴더 열기...**
2. Git에서 추적 파일이 있는 폴더를 찾아 클릭 **폴더 선택**합니다. 하위 폴더에 로컬 리포지토리는 여기에서 선택 하려면 허용 합니다.


## <a name="initialize-a-new-git-repository"></a>새 git 리포지토리를 초기화 합니다.

1. 선택 **소스 제어**, git 아이콘을 선택 합니다.

   ![소스 제어에 git 아이콘](media/source-control/source-control.png)

1. Git 리포지토리 및 키를 눌러로 초기화 하려는 폴더의 경로를 입력 **Enter**합니다.

   ![Git 리포지토리를 초기화 합니다.](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Git 리포지토리를 사용

[!INCLUDE[name-sos](../includes/name-sos-short.md)] VS Code에서 Git 구현을 상속 되지만 추가 SCM 공급자 현재 지원 하지 않습니다. Git를 열거나 저장소 초기화 작업에 대 한 세부 정보를 참조 하십시오. [VS Code의 Git 지원](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)합니다.


## <a name="additional-resources"></a>추가 리소스
- [Git 설명서](https://git-scm.com/documentation)
