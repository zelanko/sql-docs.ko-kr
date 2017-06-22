---
title: "데이터 기반 구독 (SSRS 자습서) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
caps.latest.revision: 50
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7ca542c75d289b79284c5affeea5095ac032e1e0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>데이터 기반 구독 만들기(SSRS 자습서)
이 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 자습서에서는 필터링된 보고서 출력을 생성하고 파일 공유에 저장하기 위해 데이터 기반 구독을 만드는 간단한 예제를 단계별로 안내하여 데이터 기반 구독의 개념을 설명합니다. 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 기반 구독을 사용하면 동적 구독자 데이터를 기반으로 하여 보고서 배포를 사용자 지정 및 자동화할 수 있습니다. 데이터 기반 구독은 다음과 같은 종류의 시나리오에 사용됩니다.  
  
-   배포마다 멤버가 변경될 수 있는 대규모 받는 사람 풀에 보고서 배포. 예를 들면 모든 현재 고객에게 월별 보고서를 메일로 보내는 경우입니다.  
  
-   미리 정의된 조건을 기반으로 특정 받는 사람 그룹에 보고서 배포. 예를 들면 조직의 모든 판매 관리자에게 판매 실적 보고서를 보내는 경우입니다.
+ 다양한 형식(예: .xlsx 및 .pdf)의 보고서 생성을 자동화합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서는 다음 3개의 단원으로 이루어져 있습니다.  
 단원 | 설명
 ------- | --------------
 [1단원: 샘플 구독자 데이터베이스 만들기](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | 이 단원에서는 필터링 및 출력 파일 형식에 사용할 주문 번호 정보 등의 구독자 정보가 있는 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 테이블을 만듭니다.
[2단원: 보고서 데이터 원본 속성 구성](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) |이 단원에서는 보고서가 일정에 따라 무인 모드로 실행되도록 보고서 데이터 원본을 구성합니다. 무인 처리를 위해서는 저장된 자격 증명이 필요합니다. 또한 구독자 데이터로 공급되는 매개 변수를 포함하도록 보고서 데이터 집합을 수정합니다. 이 매개 변수는 주문 번호에 따라 보고서 데이터를 필터링하는 데 사용됩니다.
 [3단원: 데이터 기반 구독 정의](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | 이 단원에서는 데이터 기반 구독을 만듭니다. 데이터 기반 구독 마법사의 각 페이지를 안내합니다.

 다음 다이어그램은 자습서의 기본 워크플로를 보여 줍니다.

단계  |Description 
---------|---------
(1)     |  구독 구성에는 원본 보고서, 일정 및 구독자 데이터베이스에 대한 필드 매핑이 표시됩니다.        
(2)     | OrderInfo 테이블에는 필터링에 사용할 4개의 주문 번호(파일당 1개씩)가 포함되어 있습니다. 또한 테이블에는 생성된 보고서의 파일 형식이 있습니다.
(3)     | Adventureworks 데이터베이스의 정보가 필터링되어 보고서에 반환됩니다. 
(4)     | Orderinfo 테이블에 지정된 파일 형식으로 보고서가 생성됩니다.

 
 
   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>요구 사항  
데이터 기반 구독은 대개 보고서 서버 관리자가 만들고 유지 관리합니다. 데이터 기반 구독을 만드는 단계를 수행하려면 쿼리 작성, 구독자 데이터가 포함된 데이터 원본에 대한 지식, 보고서 서버에서 승격된 권한이 필요합니다.  
  
이 자습서에서는 *기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;* 자습서에서 만든 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) 보고서와 샘플 데이터베이스 **AdventureWorks2014**의 데이터를 사용합니다.  
  
이 자습서를 사용하려면 컴퓨터에 다음 항목이 설치되어 있어야 합니다.  
  
-   데이터 기반 구독을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 버전. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../sql-server/editions-and-components-of-sql-server-2016.md)를 참조하세요.  
  
-   기본 모드로 보고서 서버가 실행되고 있어야 합니다. 이 자습서에 설명된 사용자 인터페이스는 기본 모드 보고서 서버를 기반으로 합니다. 구독은 SharePoint 모드 보고서 서버에서 지원되지만 사용자 인터페이스는 이 자습서에 설명된 것과 다릅니다.  
  
-   SQL Server 에이전트 서비스가 실행되고 있어야 합니다.  
  
-   매개 변수가 들어 있는 보고서가 필요합니다. 이 자습서에서는 `Sales Orders` 기본 테이블 보고서 만들기&#40;SSRS 자습서&#41; [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)의 데이터를 사용합니다.  
  
-   샘플 보고서에 데이터를 제공하는 **AdventureWorks2014** 샘플 데이터베이스가 필요합니다.  
  
-   샘플 보고서에 대한 모든 구독 관리 태스크를 포함하는 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 역할 할당이 필요합니다. 이 태스크는 데이터 기반 구독 정의에 필요합니다. 컴퓨터 관리자인 경우 로컬 관리자에 대한 기본 역할 할당을 통해 데이터 기반 구독을 만드는 데 필요한 권한을 얻을 수 있습니다. 자세한 내용은 [Granting Permissions on a Native Mode Report Server](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)을 참조하세요.  
  
-   쓰기 권한이 있는 공유 폴더가 필요합니다. 이 공유 폴더는 네트워크 연결을 통해 액세스할 수 있어야 합니다.  
  
**자습서에 소요되는 예상 시간:** 30분 기본 보고서 자습서를 완료하지 않은 경우 추가 30분이 소요됩니다.  
  
## <a name="see-also"></a>참고 항목  
[Data-Driven Subscriptions](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 


