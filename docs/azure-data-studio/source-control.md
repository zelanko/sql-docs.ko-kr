---
title: 원본 제어
description: Azure Data Studio는 SCM(소스 제어 관리)용 Git를 지원합니다. 기존 Git 리포지토리를 여는 방법 및 새 Git 리포지토리를 초기화하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2019
ms.openlocfilehash: 7f032d870952cdadbde79dbf56f4c63ae351d6e9
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081572"
---
# <a name="source-control-in-azure-data-studio"></a>Azure Data Studio의 소스 제어

Azure Data Studio는 버전/소스 제어를 위해 Git를 지원합니다.

## <a name="git-support-in-azure-data-studio"></a>Azure Data Studio에서 Git 지원

Azure Data Studio는 Git SCM(소스 제어 관리자)과 함께 제공되지만, 먼저 [Git(버전 2.0.0 이상)을 설치](https://git-scm.com/download)해야 이러한 기능을 사용할 수 있습니다.

## <a name="open-an-existing-git-repository"></a>기존 Git 리포지토리 열기

1. **파일** 메뉴에서 **폴더 열기...** 를 선택합니다.
2. git에서 추적한 파일이 포함된 폴더로 이동한 다음, **폴더 선택**을 선택합니다. 여기서 로컬 리포지토리의 하위 폴더를 선택해도 됩니다.

## <a name="initialize-a-new-git-repository"></a>새로운 git 리포지토리 초기화

1. **원본 제어**를 선택한 다음, git 아이콘을 선택합니다.

   ![원본 제어 git 아이콘](media/source-control/source-control.png)

1. Git 리포지토리로 초기화하려는 폴더의 경로를 입력하고 **Enter** 키를 누릅니다.

   ![Git 리포지토리 초기화](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Git 리포지토리 작업

Azure Data Studio는 VS Code에서 Git 구현을 상속받지만, 현재 추가 SCM 공급자를 지원하지 않습니다. 리포지토리를 열거나 초기화한 후의 Git 작업에 대한 자세한 내용은 [VS Code의 Git 지원](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)을 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Git 설명서](https://git-scm.com/documentation)
