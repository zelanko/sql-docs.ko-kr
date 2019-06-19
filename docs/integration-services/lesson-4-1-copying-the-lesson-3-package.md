---
title: '1단계: 3단원 패키지 복사 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7b686a585b037a9377926198278a3a34f6fd4881
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721663"
---
# <a name="lesson-4-1-copy-the-lesson-3-package"></a>4-1단원: 3단원 패키지 복사

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 태스크에서는 3단원에서 Lesson 3.dtsx 패키지의 복사본을 만듭니다. 3단원을 완료하지 않은 경우에는 자습서에 포함되어 있는 완성된 3단원 패키지를 프로젝트에 추가한 다음, 작업을 수행할 복사본을 만들 수 있습니다. 4단원의 나머지 부분에서 이 새 복사본을 사용합니다.  
  
## <a name="create-the-lesson-4-package"></a>4단원 패키지 만들기  
  
완료된 3단원을 복사하는 경우 이 절차를 따릅니다.  샘플 3단원을 복사하려면 다음 섹션을 참조하세요.

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools가 아직 열려 있지 않은 경우 **시작** > **모든 프로그램** > **Microsoft SQL Server 2017**을 선택한 다음, **SQL Server Data Tools**를 선택합니다.

2.  **파일** 메뉴에서 **열기** > **프로젝트/솔루션**, **SSIS 자습서** 폴더, **열기**를 차례로 선택한 다음, **SSIS Tutorial.sln**을 두 번 클릭합니다.

3.  **솔루션 탐색기**에서 **Lesson 3.dtsx**를 마우스 오른쪽 단추로 클릭한 다음, **복사**를 선택합니다.

4.  **솔루션 탐색기**에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음, **붙여넣기**를 선택합니다.

    기본적으로 복사된 패키지의 이름은 **Lesson 4.dtsx**입니다.

5.  **솔루션 탐색기**에서 **Lesson 4.dtsx**를 두 번 클릭하여 패키지를 엽니다.

6.  **제어 흐름** 디자인 화면 배경의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.

7.  **속성** 창에서 **Name** 속성을 **4단원**으로 변경합니다.

8.  **ID** 속성 상자를 선택하고 드롭다운 화살표를 선택한 다음, **\<새 ID> 생성**을 선택합니다.

## <a name="add-the-completed-lesson-3-package"></a>완성된 3단원 패키지 추가

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools를 연 다음 SSIS 자습서 프로젝트를 엽니다.

2.  **솔루션 탐색기**에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음, **기존 패키지 추가**를 선택합니다.

3.  **기존 패키지의 복사본 추가** 대화 상자의 **패키지 위치**에서 **파일 시스템**을 선택합니다.

4.  찾아보기 **(...)** 단추를 선택하여 머신의 **Lesson 3.dtsx**로 이동한 다음, **열기**를 선택합니다.

5.  이전 섹션의 3-8단계에서 설명한 대로 3단원 패키지를 복사하여 붙여넣습니다.

  
## <a name="go-to-next-task"></a>다음 작업으로 이동  
[2단계: 손상된 파일 만들기](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
