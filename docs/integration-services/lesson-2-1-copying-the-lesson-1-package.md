---
title: '1단계: 1단원 패키지 복사 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e73ea716252368e15dcba56242e803d6c1bf93d9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283723"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>2-1단원: 1단원 패키지 복사

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 태스크에서는 **Lesson 1.dtsx** 패키지의 복사본을 만듭니다. 1단원을 완료하지 경우, 이 자습서에 포함되어 있는 완료된 1단원 패키지를 사용할 수 있습니다. 2단원의 나머지 부분에서 새 복사본을 사용합니다.  
  
## <a name="create-the-lesson-2-package"></a>2단원 패키지 만들기  

완료된 1단원을 복사하는 경우 이 절차를 따릅니다.  샘플 1단원을 복사하려면 다음 섹션을 참조하세요.
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools가 아직 열려 있지 않은 경우 **시작** > **모든 프로그램** > **Microsoft SQL Server 2017**을 선택한 다음, **SQL Server Data Tools**를 선택합니다.  
  
2.  **파일** 메뉴에서 **열기** > **프로젝트/솔루션**, **SSIS 자습서** 폴더, **열기**를 차례로 선택한 다음, **SSIS Tutorial.sln**을 두 번 클릭합니다.  
  
3.  **솔루션 탐색기**에서 **Lesson 1.dtsx**를 마우스 오른쪽 단추로 클릭한 다음, **복사**를 선택합니다.  
  
4.  **솔루션 탐색기**에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음, **붙여넣기**를 선택합니다.  
  
    기본적으로 복사된 패키지의 이름은 **Lesson 2.dtsx**가 됩니다.  
  
5.  **솔루션 탐색기**에서 **Lesson 2.dtsx**를 두 번 클릭하여 패키지를 엽니다.  
  
6.  **제어 흐름** 디자인 화면 배경의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  
  
7.  **속성** 창에서 **Name** 속성을 **Lesson 2**으로 변경합니다.  
  
8.  **ID** 속성 상자를 선택하고 드롭다운 화살표를 선택한 다음, **\<새 ID> 생성**을 선택합니다.  
  
## <a name="use-the-sample-lesson-1-package"></a>샘플 1단원 패키지 사용  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools를 연 다음 SSIS 자습서 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음, **기존 패키지 추가**를 선택합니다.  
  
3.  **기존 패키지의 복사본 추가** 대화 상자의 **패키지 위치**에서 **파일 시스템**을 선택합니다.  
  
4.  찾아보기 **(...)** 단추를 선택하여 컴퓨터의 **Lesson 1.dtsx**로 이동한 다음, **열기**를 선택합니다.  
  
5.  이전 섹션의 3-8단계에서 설명한 대로 1단원 패키지를 복사하여 붙여넣습니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동

[2단계: Foreach 루프 컨테이너 추가 및 구성](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
