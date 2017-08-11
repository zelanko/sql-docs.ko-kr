---
title: "기본 테이블 보고서 (SSRS 자습서) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
caps.latest.revision: 67
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7cd0ab1950eeaf54da67e7f8dd5bb2da89a26307
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="create-a-basic-table-report-ssrs-tutorial"></a>기본 테이블 보고서 만들기(SSRS 자습서)

이 자습서에서는 보고서 디자이너를 사용 하면 SQL Server Data Tools에서 만드는 기본 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서로 테이블을 기반으로  **[!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]**  데이터베이스입니다. 만들 수도 있습니다 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서 작성기는 보고서입니다. 

이 자습서를 진행 보고서 프로젝트, 연결 정보를 설정, 쿼리를 정의 테이블 데이터 영역을 추가, 그룹화 및 총 일부 필드를 만들고 보고서를 미리 봅니다.  
  
## <a name="requirements"></a>요구 사항  
이 자습서를 사용하려면 시스템에 다음 항목이 설치되어야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)]SQL Server 데이터베이스 엔진입니다.  
  
-   [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] .  
  
-   [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 데이터베이스.  자세한 내용은 [Adventure Works 2014 샘플 데이터베이스](https://msftdbprodsamples.codeplex.com/releases/view/125550)를 참조하세요.  
  
 -   보고서 디자이너를 사용할 수 있도록 "SQL Server Reporting Services" 구성 요소가 설치된[SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) .    
  
또한 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 데이터베이스에서 데이터를 검색하려면 읽기 전용 권한이 있어야 합니다.

**자습서에 소요되는 예상 시간:** 30분
  
## <a name="tasks"></a>태스크  
[1단원: 보고서 서버 프로젝트 만들기&#40;Reporting Services&#41;](../reporting-services/lesson-1-creating-a-report-server-project-reporting-services.md)  
  
[2단원: 연결 정보 지정&#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md)  
  
[3단원: 테이블 보고서에 대한 데이터 집합 정의&#40;Reporting Services&#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)  
  
[4단원: 보고서에 테이블 추가&#40;Reporting Services&#41;](../reporting-services/lesson-4-adding-a-table-to-the-report-reporting-services.md)  
  
[5단원: 보고서 서식 지정&#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md)  
  
[6단원: 그룹화 및 합계 추가&#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)  

## <a name="next-steps"></a>다음 단계

[Reporting Services 자습서](../reporting-services/reporting-services-tutorials-ssrs.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
