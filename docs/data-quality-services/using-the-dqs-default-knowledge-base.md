---
title: "DQS 기본 기술 자료 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# DQS 기본 기술 자료 사용
  이 항목에서는 기본 기술 자료 문서에서 설명 **DQS 데이터**, 를 함께 설치 되는 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). DQS 데이터는 다음과 같은 도메인이 포함된 미리 작성된 기본 기술 자료입니다.  
  
-   **국가/지역**: 규칙에 따른 긴 (국가/지역으로 지정 된 공식 이름) 및 짧은 이름 (목록, 맵, 등에서 사용 되는 일반 이름), 2 자 약어, 3 자 약어 및 각 위치에 대해 3 자리 코드를 포함 합니다.  선행 값은 긴 국가 이름으로 설정됩니다.  
  
-   **국가/지역 (3 자 선행)**: 규칙에 따른 긴 (국가/지역으로 지정 된 공식 이름) 및 짧은 이름 (목록, 맵, 등에 사용 되는 일반 이름), 2 자 약어, 3 자 약어 및 각 위치에 대해 3 자리 코드를 포함 합니다.  선행 값은 국가의 3자 약어로 설정됩니다.  
  
-   **국가/지역 (2 자 선행)**: 규칙에 따른 긴 (국가/지역으로 지정 된 공식 이름) 및 짧은 이름 (목록, 맵, 등에서 사용 되는 일반 이름), 2 자 약어, 3 자 약어 및 각 위치에 대해 3 자리 코드를 포함 합니다.  선행 값은 국가의 2자 약어로 설정됩니다.  
  
-   **미국-군**: 미국의 군 목록을 포함 합니다.  
  
-   **미국-성**: 성 (성) 100 발생 또는 한 번에 2000 년 인구 조사 목록을 포함 합니다.  
  
-   **미국-배치**: 50 개 주, 콜롬비아 특별구 및 푸에르토리코 2010 년 인구 조사에서에서 추출에 대 한 위치 목록을 포함 합니다.  
  
-   **미국-상태**: 포함 (공식) 규칙에 따른 긴 이름 및 미국의 각 주에에서 대 한 약어 두 자를 합니다. 선행 값은 규칙에 따른 주 이름으로 설정됩니다.  
  
-   **미국 – 상태 (2 못 머리글)**: 포함 (공식) 규칙에 따른 긴 이름 및 미국의 각 주에에서 대 한 약어 두 자를. 선행 값은 주 이름의 2자 약어로 설정됩니다.  
  
## 기본 기술 자료 사용  
 다음과 같은 방법으로 기본 DQS 기술 자료인 DQS 데이터를 사용할 수 있습니다.  
  
-   먼저 DQS에서 새 기술 자료를 만들 필요 없이 기본 기술 자료를 사용하여 정리 데이터 품질 프로젝트를 빠르게 시작하고 실행합니다.  
  
-   기본 기술 자료에서 도메인 관리, 기술 자료 검색 또는 일치 정책 작업을 실행합니다. 이렇게 하려면 **Data Quality Client Home Screen** 에서 [기술 자료 열기](../data-quality-services/data-quality-client-home-screen.md)를 클릭하고 **기술 자료 열기** 화면에서 **DQS 데이터** 기술 자료를 선택한 다음 **작업 선택** 영역에서 필요한 작업을 선택합니다. 계속 진행하려면 **다음** 을 클릭합니다.  
  
-   기본 기술 자료를 사용하여 새 기술 자료를 만듭니다. 기존 기술 자료를 토대로 기술 자료를 만들려면 [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md)를 참조하십시오.  
  
-   사용 된 [Integration Services의 DQS 정리 구성 요소](http://go.microsoft.com/fwlink/?LinkId=238830) 및 [Master Data Services 추가 기능 Excel 용](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)합니다.  
  
## 참고 항목  
 [DQS 기술 자료 및 도메인](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  