---
title: '1단계: 5단원 패키지 복사 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ede34999b9ca7a18a2bb5ec997c4a93735b82be2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62890759"
---
# <a name="step-1-copying-the-lesson-5-package"></a>1단계: 5단원 패키지 복사
  이 태스크에서는 5단원에서 만든 Lesson 5.dtsx 패키지의 복사본을 만듭니다. 또는 자습서에 포함되어 있는 완성된 5단원 패키지를 프로젝트에 추가한 다음 복사할 수도 있습니다. 6단원의 나머지 부분에서 이 새 복사본을 사용합니다.  
  
### <a name="to-copy-the-lesson-5-package"></a>5단원 패키지를 복사하려면  
  
1.  SQL Server Data Tools를 아직 열지 않은 경우 시작을 클릭하고 모든 프로그램, Microsoft SQL Server 2012를 차례로 가리킨 다음 SQL Server Data Tools를 클릭합니다.  
  
2.  파일 메뉴에서 열기, 프로젝트/솔루션을 차례로 클릭하고 SSIS Tutorial을 선택하고 열기를 클릭한 후 SSIS Tutorial.sln을 두 번 클릭합니다.  
  
3.  솔루션 탐색기에서 Lesson 5.dtsx를 마우스 오른쪽 단추로 클릭한 후 복사를 클릭합니다.  
  
4.  솔루션 탐색기에서 SSIS 패키지를 마우스 오른쪽 단추로 클릭한 후 붙여넣기를 클릭합니다.  
  
     기본적으로 복사된 패키지의 이름은 Lesson 6.dtsx가 됩니다.  
  
5.  솔루션 탐색기에서 Lesson 6.dtsx를 두 번 클릭하여 패키지를 엽니다.  
  
6.  제어 흐름 탭 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 다음 속성을 클릭합니다.  
  
7.  속성 창에서 Name 속성을 Lesson 6으로 업데이트합니다.  
  
8.  ID 속성 상자를 클릭 한 다음 드롭다운 화살표를 클릭 하 고 새 ID> 생성 \<을 클릭 합니다.  
  
### <a name="to-add-the-completed-lesson-5-package"></a>완성된 5단원 패키지를 추가하려면  
  
1.  SQL Server Data Tools를 연 다음 SSIS 자습서 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 SSIS 패키지를 마우스 오른쪽 단추로 클릭한 다음 기존 패키지 추가를 클릭합니다.  
  
3.  기존 패키지의 복사본 추가 대화 상자의 패키지 위치에서 파일 시스템을 선택합니다.  
  
4.  찾아보기(…) 단추를 클릭하여 머신의 Lesson 5.dtsx로 이동한 다음, **열기**를 클릭합니다.  
  
     이 자습서에 대한 모든 단원 패키지를 다운로드하려면 다음을 수행합니다.  
  
    1.  [Integration Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=275027)로 이동합니다.  
  
    2.  **다운로드** 탭을 클릭 합니다.  
  
    3.  SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 파일을 클릭합니다.  
  
5.  이전 절차의 3-8단계에서 설명한 대로 5단원 패키지를 복사하여 붙여 넣습니다.  
  
     5단원 패키지를 복사한 후 솔루션에 이전 단원의 패키지가 현재 있는 경우 1-5단원에서 각 패키지를 마우스 오른쪽 단추로 클릭하고 프로젝트에서 제외를 클릭합니다. 작업이 완료되면 솔루션에 Lesson 6.dtsx만 있습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [2단계: 프로젝트를 프로젝트 배포 모델로 변환](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
  
