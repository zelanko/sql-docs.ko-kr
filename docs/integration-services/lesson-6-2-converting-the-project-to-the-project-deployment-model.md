---
description: '6-2단원: 프로젝트를 프로젝트 배포 모델로 변환'
title: '2단계: 프로젝트를 프로젝트 배포 모델로 변환 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc0e6111542e73ad64a2e82a7f82b3b8bfbf41c4
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88487768"
---
# <a name="lesson-6-2-convert-the-project-to-the-project-deployment-model"></a>6-2단원: 프로젝트를 프로젝트 배포 모델로 변환

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



이 작업에서는 프로젝트를 프로젝트 배포 모델로 변환하기 위해 Integration Services 프로젝트 변환 마법사를 사용합니다.  
  
1.  **프로젝트** 메뉴에서 **프로젝트 배포 모델로 변환** 을 선택합니다.  
  
2.  **Integration Services 프로젝트 전환 마법사** **소개** 페이지에서 단계를 검토하고 **다음** 을 선택합니다.  
  
3.  **패키지 선택** 페이지의 **패키지** 목록에서 **Lesson 6.dtsx** 를 제외한 모든 확인란의 선택을 취소한 다음, **다음** 을 선택합니다.  
  
4.  **프로젝트 속성 지정** 페이지에서 **다음** 을 선택합니다.  
  
5.  **실행 패키지 작업 업데이트** 페이지에서 **다음** 을 선택합니다.  
  
6.  **구성 선택** 페이지의 **구성** 목록에서 **Lesson 6.dtsx** 패키지가 선택되었는지 확인한 다음, **다음** 을 선택합니다.  
  
7.  **매개 변수 만들기** 페이지에서 **lesson 6.dtsx** 패키지를 선택해야 합니다.  **범위** 가 **구성 속성** 목록의 **패키지** 인지 확인한 다음, **다음** 을 선택합니다.  
  
8.  **매개 변수 구성** 페이지에서 **이름** 및 **값** 이 변수 및 구성 값에 대한 Lesson 5에서 지정된 이름 및 값과 동일한지 확인한 다음, **다음** 을 선택합니다.  
  
9. **검토** 페이지의 **요악** 창에서 마법사가 변환된 **속성** 을 설정하기 위해 구성 파일의 정보를 사용했습니다.  
  
10. **변환** 을 선택합니다.  
  
    변환이 완료되면 프로젝트를 저장할 때까지 변경 내용이 저장되지 않았다는 경고 메시지가 표시됩니다. **확인** 을 선택하여 경고 대화 상자를 닫습니다.  
  
11. **Integration Services 프로젝트 변환 마법사** 에서 **닫기** 를 선택합니다.  
  
12. **SQL Server Data Tools** 에서 **파일** 메뉴를 클릭한 다음, **저장** 을 선택하여 변환된 패키지를 저장합니다.  
  
13. **매개 변수** 탭을 선택하고 패키지에 **VarFolderName** 의 매개 변수가 포함되어 있는지 확인합니다. 매개 변수 값은 5단원 구성 파일의 **New Sample Data** 폴더에 지정된 동일한 경로입니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[3단계: 6단원 패키지 테스트](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
