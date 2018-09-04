---
title: 기본 테이블 보고서 만들기(SSRS 자습서) | Microsoft Docs
ms.date: 11/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c282753708c368326530c84c08a51b8fa484d72e
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43271135"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>기본 테이블 보고서 만들기(SSRS 자습서)

이 자습서에서는 SQL Server Data Tools에서 보고서 디자이너를 사용하여 **[!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]** 데이터베이스 기반의 테이블이 있는, 기본 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 페이지 매긴 보고서를 만듭니다. 보고서 작성기로 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 페이지 매긴 보고서를 만들 수도 있습니다. 

이 자습서를 진행하면서 보고서 프로젝트를 만들고, 연결 정보를 설정하고, 쿼리를 정의하고, 테이블 데이터 영역을 추가하고, 필드를 그룹화하거나 필드 합계를 구하고, 보고서를 미리 보는 방법을 배웁니다.  
  
## <a name="requirements"></a>요구 사항  
이 자습서를 사용하려면 시스템에 다음 항목이 설치되어야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] SQL Server 데이터베이스 엔진.  
  
-   [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] .  
  
-   [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 데이터베이스.  자세한 내용은 [Adventure Works 2014 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 참조하세요.  
  
 -   보고서 디자이너를 사용할 수 있도록 "SQL Server Reporting Services" 구성 요소가 설치된 [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md).    
  
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

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
