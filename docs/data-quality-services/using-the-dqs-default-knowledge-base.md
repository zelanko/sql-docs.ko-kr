---
title: "DQS 기본 기술 자료 사용 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7ae8a2dfc3d36da671ff848eb8ab0d5a7f2a7bf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="using-the-dqs-default-knowledge-base"></a>DQS 기본 기술 자료 사용
  이 항목에서는 DQS( **)와 함께 설치되는 기본 기술 자료인**DQS 데이터 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 에 대해 설명합니다. DQS 데이터는 다음과 같은 도메인이 포함된 미리 작성된 기본 기술 자료입니다.  
  
-   **국가/지역**: 각 위치에 대해 규칙에 따른 긴 이름(국가/지역에 따라 지정되는 공식 이름)과 짧은 이름(목록, 지도 등에 사용되는 일반 이름), 2자 약어, 3자 약어 및 3자리 코드를 포함합니다.  선행 값은 긴 국가 이름으로 설정됩니다.  
  
-   **국가/지역(선행 3자)**: 각 위치에 대해 규칙에 따른 긴 이름(국가/지역에 따라 지정되는 공식 이름)과 짧은 이름(목록, 지도 등에 사용되는 일반 이름), 2자 약어, 3자 약어 및 3자리 코드를 포함합니다.  선행 값은 국가의 3자 약어로 설정됩니다.  
  
-   **국가/지역(선행 2자)**: 각 위치에 대해 규칙에 따른 긴 이름(국가/지역에 따라 지정되는 공식 이름)과 짧은 이름(목록, 지도 등에 사용되는 일반 이름), 2자 약어, 3자 약어 및 3자리 코드를 포함합니다.  선행 값은 국가의 2자 약어로 설정됩니다.  
  
-   **미국 - 지방**: 미국의 지방 목록을 포함합니다.  
  
-   **미국 - 성**: 2000년 인구 조사에서 100번 이상 나타난 성의 목록을 포함합니다.  
  
-   **미국 - 위치**: 2010년 인구 조사에서 추출된 50개 주, 콜롬비아 특별구 및 푸에르토리코의 위치 목록을 포함합니다.  
  
-   **미국 - 주**: 미국의 각 주에 대해 규칙에 따른 긴 이름(공식 이름)과 2자 약어를 포함합니다. 선행 값은 규칙에 따른 주 이름으로 설정됩니다.  
  
-   **미국 - 주(선행 2자)**:미국의 각 주에 대해 규칙에 따른 긴 이름(공식 이름)과 2자 약어를 포함합니다. 선행 값은 주 이름의 2자 약어로 설정됩니다.  
  
## <a name="using-the-default-knowledge-base"></a>기본 기술 자료 사용  
 다음과 같은 방법으로 기본 DQS 기술 자료인 DQS 데이터를 사용할 수 있습니다.  
  
-   먼저 DQS에서 새 기술 자료를 만들 필요 없이 기본 기술 자료를 사용하여 정리 데이터 품질 프로젝트를 빠르게 시작하고 실행합니다.  
  
-   기본 기술 자료에서 도메인 관리, 기술 자료 검색 또는 일치 정책 작업을 실행합니다. 이렇게 하려면 **Data Quality Client Home Screen** 에서 [기술 자료 열기](../data-quality-services/data-quality-client-home-screen.md)를 클릭하고 **기술 자료 열기** 화면에서 **DQS 데이터** 기술 자료를 선택한 다음 **작업 선택** 영역에서 필요한 작업을 선택합니다. 계속 진행하려면 **다음** 을 클릭합니다.  
  
-   기본 기술 자료를 사용하여 새 기술 자료를 만듭니다. 기존 기술 자료를 토대로 기술 자료를 만들려면 [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md)를 참조하십시오.  
  
-   [Integration Services의 DQS 정리 구성 요소](http://go.microsoft.com/fwlink/?LinkId=238830) 및 [Excel용 Master Data Services 추가 기능](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)에서 기술 자료를 사용합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DQS 기술 자료 및 도메인](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
