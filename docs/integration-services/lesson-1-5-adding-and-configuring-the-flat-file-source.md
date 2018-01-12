---
title: "5단계: 플랫 파일 원본 추가 및 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5e4d78be29d3fd124b1a85c12c4a8ec58d3c5dcf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-1-5---adding-and-configuring-the-flat-file-source"></a>1-5단원: 플랫 파일 원본 추가 및 구성
이 태스크에서는 플랫 파일 원본을 패키지에 추가하고 구성하는 방법에 대해 설명합니다. 플랫 파일 원본은 플랫 파일 연결 관리자에서 정의된 메타데이터를 사용하여 변환 프로세스를 통해 플랫 파일에서 추출할 데이터 구조와 형식을 지정하는 데이터 흐름 구성 요소입니다. 플랫 파일 원본은 플랫 파일 연결 관리자에서 제공된 파일 형식 정의를 사용하여 단일 플랫 파일에서 데이터를 추출하도록 구성할 수 있습니다.  
  
이 자습서에서는 이전에 작성한 **Sample Flat File Source Data** 연결 관리자를 사용하도록 플랫 파일 원본을 구성하는 과정을 다룹니다.  
  
### <a name="to-add-a-flat-file-source-component"></a>플랫 파일 원본 구성 요소를 추가하려면  
  
1.  **Extract Sample Currency Data** 데이터 흐름 태스크를 두 번 클릭하거나 **데이터 흐름** 탭을 클릭하여 **데이터 흐름**디자이너를 엽니다.  
  
2.  **SSIS 도구 상자**에서 **기타 원본**을 확장한 다음 **플랫 파일 원본** 을 **데이터 흐름** 탭의 디자인 화면으로 끌어다 놓습니다.  
  
3.  **데이터 흐름** 디자인 화면에서 새로 추가한 **플랫 파일 원본**을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 다음 이름을 **Extract Sample Currency Data**로 변경합니다.  
  
4.  플랫 파일 원본을 두 번 클릭하여 플랫 파일 원본 편집기 대화 상자를 엽니다.  
  
5.  **플랫 파일 연결 관리자** 상자에서 **Sample Flat File Source Data**를 선택합니다.  
  
6.  **열** 을 클릭하고 열 이름이 올바른지 확인합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  플랫 파일 원본을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
9. 속성 창에서 **LocaleID** 속성이 **영어(미국)**로 설정되어 있는지 확인합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[6단계: 조회 변환 추가 및 구성](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>참고 항목  
[플랫 파일 원본](../integration-services/data-flow/flat-file-source.md)  
[플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
  
  
