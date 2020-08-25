---
title: 바로 가기 키 만들기 및 사용자 지정
description: Visual Studio Code의 기능을 기반으로 Azure Data Studio에서 바로 가기 키를 보고 편집하고 만드는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: e8f5e60d0a8f5c578e27dfb283459882d58a0195
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746123"
---
# <a name="keyboard-shortcuts-in-azure-data-studio"></a>Azure Data Studio에서의 바로 가기 키

이 문서에서는 Azure Data Studio에서 바로 가기 키를 빠르게 살펴보고 편집하고 만드는 단계를 제공합니다.

Azure Data Studio는 Visual Studio Code에서 키 바인딩 기능을 상속 받으므로 고급 사용자 지정, 다양한 키보드 레이아웃 사용 등에 대한 자세한 내용은 [Visual Studio Code의 키 바인딩](https://code.visualstudio.com/docs/getstarted/keybindings) 문서를 참조하세요. 일부 키 바인딩 기능은 사용하지 못할 수도 있습니다. 예를 들어 키맵 확장은 Azure Data Studio에서 지원되지 않습니다.

## <a name="open-the-keyboard-shortcuts-editor"></a>바로 가기 키 편집기 열기

현재 정의된 바로 가기 키를 모두 보려면 다음을 수행합니다.

**파일** 메뉴에서 **바로 가기 키** 편집기를 엽니다. **파일** > **기본 설정** > **바로 가기 키**(Mac에서는 **Azure Data Studio** > **기본 설정** > **바로 가기 키**)를 선택하면 됩니다.

**바로 가기 키** 편집기에는 현재 키 바인딩뿐만 아니라 바로 가기 키가 정의되지 않은 사용 가능한 명령도 표시됩니다. **바로 가기 키** 편집기를 사용하여 키 바인딩을 쉽게 변경, 제거, 다시 설정 및 새로 정의할 수 있습니다.  

## <a name="edit-existing-keyboard-shortcuts"></a>기존 바로 가기 키 편집

기존 바로 가기 키의 키 바인딩을 변경하려면 다음을 수행합니다.

1. 검색 상자를 사용하거나 목록을 스크롤하여 변경할 바로 가기 키를 찾습니다.
   > [!TIP]
   > 관련된 바로 가기 키를 모두 반환하려면 키, 명령, 원본 등으로 검색합니다.

2. 원하는 항목을 마우스 오른쪽 단추로 클릭하고 **키 바인딩 변경**을 선택합니다.

   ![바로 가기 키 편집](media/keyboard-shortcuts/change-keybinding.png)

3. 원하는 키 조합을 누르고 **Enter** 키를 눌러 저장합니다. 

   ![바로 가기 키 저장](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>새 바로 가기 키 만들기

새 바로 가기 키를 만들려면 다음을 수행합니다.

1. 키 바인딩이 없는 명령을 마우스 오른쪽 단추로 클릭하고 **키 바인딩 추가**를 선택합니다.

   ![바로 가기 키 만들기](media/keyboard-shortcuts/add-keybinding.png)

2. 원하는 키 조합을 누르고 **Enter** 키를 눌러 저장합니다.