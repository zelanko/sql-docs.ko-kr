---
title: '1단계: 5단원 패키지 복사 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c4c895e71da13d7de38bf5dfc64f27829206d25
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283120"
---
# <a name="lesson-6-1-copy-the-lesson-5-package"></a>6-1단원: 5단원 패키지 복사

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 작업에서는 5단원의 **Lesson 5.dtsx** 패키지에 대한 복사본을 만듭니다. 5단원을 완료하지 않은 경우에는 자습서에 포함되어 있는 완성된 5단원 패키지를 프로젝트에 추가한 다음, 작업을 수행할 복사본을 만들 수 있습니다. 6단원의 나머지 부분에서 이 새 복사본을 사용합니다. 

> [!IMPORTANT]
> 5단원 패키지를 복사한 후 솔루션에 이전 단원의 패키지가 현재 있는 경우 1-5단원에서 각 패키지를 마우스 오른쪽 단추로 클릭하고, **프로젝트에서 제외**를 선택합니다. 작업이 완료되면 솔루션에 **Lesson 6.dtsx**만 남게 됩니다.   
  
## <a name="create-the-lesson-6-package"></a>6단원 패키지 만들기  
  
완료된 5단원을 복사하는 경우 이 프로시저를 사용하세요.  샘플 5단원을 복사하려면 다음 섹션을 참조하세요.

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools가 아직 열려 있지 않은 경우 **시작** > **모든 프로그램** > **Microsoft SQL Server 2017**을 선택한 다음, **SQL Server Data Tools**를 선택합니다.

2.  **파일** 메뉴에서 **열기** > **프로젝트/솔루션**, **SSIS 자습서** 폴더, **열기**를 차례로 선택한 다음, **SSIS Tutorial.sln**을 두 번 클릭합니다.

3.  **솔루션 탐색기**에서 **Lesson 5.dtsx**를 마우스 오른쪽 단추로 클릭한 다음, **복사**를 선택합니다.

4.  **솔루션 탐색기**에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음, **붙여넣기**를 선택합니다.

    기본적으로 복사된 패키지의 이름은 **Lesson 5.dtsx**입니다.

5.  **솔루션 탐색기**에서 **Lesson 5.dtsx**를 두 번 클릭하여 패키지를 엽니다.

6.  **제어 흐름** 디자인 화면 배경의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.

7.  **속성** 창에서 **Name** 속성을 **6단원**으로 변경합니다.

8.  **ID** 속성 상자를 선택하고 드롭다운 화살표를 선택한 다음, **\<새 ID> 생성**을 선택합니다.

## <a name="add-the-completed-lesson-5-package"></a>완성된 5단원 패키지 추가

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools를 연 다음 SSIS 자습서 프로젝트를 엽니다.

2.  **솔루션 탐색기**에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음, **기존 패키지 추가**를 선택합니다.

3.  **기존 패키지의 복사본 추가** 대화 상자의 **패키지 위치**에서 **파일 시스템**을 선택합니다.

4.  찾아보기 **(...)** 단추를 선택하여 머신의 **Lesson 5.dtsx**로 이동한 다음, **열기**를 선택합니다.

5.  이전 섹션의 3-8단계에서 설명한 대로 5단원 패키지를 복사하여 붙여넣습니다.

## <a name="go-to-next-task"></a>다음 작업으로 이동
[2단계: 프로젝트를 프로젝트 배포 모델로 변환](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
