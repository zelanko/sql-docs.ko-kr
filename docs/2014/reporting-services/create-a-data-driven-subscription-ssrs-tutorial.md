---
title: 데이터 기반 구독 만들기(SSRS 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f4122aa579766d80cfac6600753d4a8f8a672ae9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017915"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>데이터 기반 구독 만들기(SSRS 자습서)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 데이터 기반 구독을 제공하므로 동적 구독자 데이터를 기반으로 보고서 배포를 사용자 지정할 수 있습니다. 데이터 기반 구독은 다음과 같은 종류의 시나리오에 사용됩니다.  
  
-   배포마다 멤버가 변경될 수 있는 대규모 받는 사람 풀에 보고서 배포. 예를 들면 모든 현재 고객에게 월별 보고서를 배포하는 경우입니다.  
  
-   미리 정의된 조건을 기반으로 특정 받는 사람 그룹에 보고서 배포. 예를 들면 조직의 최고 판매 관리자 10명에게 판매 실적 보고서를 보내는 경우입니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 개념을 설명하는 간단한 예제를 통해 데이터 기반 구독을 사용하는 방법을 보여 줍니다.  
  
 이 자습서는 다음 3개의 단원으로 이루어져 있습니다.  
  
 [1단원: 예제 구독자 데이터베이스 만들기](lesson-1-creating-a-sample-subscriber-database.md)  
 이 단원에서는 구독자 정보가 있는 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스를 만드는 방법을 배웁니다.  
  
 [2단원: 보고서 데이터 원본 속성 수정](lesson-2-modifying-the-report-data-source-properties.md)을 참조하세요.  
 이 단원에서는 보고서가 무인 모드로 실행되도록 보고서 데이터 원본 속성을 수정하는 방법을 배웁니다. 무인 처리를 위해서는 저장된 자격 증명이 필요합니다. 또한 구독자 데이터로 공급되는 매개 변수를 포함하도록 보고서 데이터 세트를 수정합니다.  
  
 [3단원: 데이터 기반 구독 정의](lesson-3-defining-a-data-driven-subscription.md)  
 이 단원에서는 데이터 기반 구독을 정의하는 방법을 배우며 데이터 기반 구독 마법사의 각 페이지를 안내합니다.  
  
## <a name="requirements"></a>요구 사항  
 데이터 기반 구독은 대개 보고서 서버 관리자가 만들고 유지 관리합니다. 데이터 기반 구독을 만들려면 쿼리 작성에 대한 전문 지식, 구독자 데이터가 포함된 데이터 원본에 대한 지식, 보고서 서버에서 승격된 권한이 필요합니다.  
  
 이 자습서는 자습서에서 만든 보고서를 사용 하 여 [기본 테이블 보고서 만들기 &#40;SSRS 자습서&#41; ](create-a-basic-table-report-ssrs-tutorial.md) 및 데이터에서 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 이 자습서를 사용하려면 시스템에 다음 항목이 설치되어야 합니다.  
  
-   데이터 기반 구독을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 버전. 자세한 내용은 [버전 및 SQL Server 2014 구성 요소](../sql-server/editions-and-components-of-sql-server-2016.md)합니다.  
  
-   기본 모드로 보고서 서버가 실행되고 있어야 합니다. 이 자습서에 설명된 사용자 인터페이스는 기본 모드 보고서 서버를 기반으로 합니다. 구독은 SharePoint 모드 보고서 서버에서 지원되지만 사용자 인터페이스는 이 자습서에 설명된 것과 다릅니다.  
  
-   SQL Server 에이전트 서비스가 실행되고 있어야 합니다.  
  
-   매개 변수가 들어 있는 보고서가 필요합니다. 이 자습서에서는 `Sales Orders` 기본 테이블 보고서 만들기&#40;SSRS 자습서&#41; [기본 테이블 보고서 만들기&amp;#40;SSRS 자습서&amp;#41;](create-a-basic-table-report-ssrs-tutorial.md)의 데이터를 사용합니다.  
  
-   예제 보고서에 데이터를 제공하는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 예제 데이터베이스가 필요합니다.  
  
-   예제 보고서에 대한 모든 구독 관리 태스크를 포함하는 역할 할당이 필요합니다. 이 태스크는 데이터 기반 구독 정의에 필요합니다. 컴퓨터 관리자인 경우 로컬 관리자에 대한 기본 역할 할당을 통해 데이터 기반 구독을 만드는 데 필요한 권한을 얻을 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)을 참조하세요.  
  
-   쓰기 권한이 있는 공유 폴더가 필요합니다. 이 공유 폴더는 네트워크 연결을 통해 액세스할 수 있어야 합니다.  
  
 **자습서에 소요되는 예상 시간:** 30분 기본 보고서 자습서를 완료하지 않은 경우 추가 30분이 소요됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
