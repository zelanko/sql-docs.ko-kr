---
title: 기본 테이블 보고서 만들기(SSRS 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
caps.latest.revision: 61
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a5c3560a7aafd3fcf53f9b10d606e1f999bbf063
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196813"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>기본 테이블 보고서 만들기(SSRS 자습서)
  이 자습서에 따라 기본 테이블 보고서를 만드는 데는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 보고서 디자이너를 사용 하 여 데이터베이스입니다. 또한 보고서 작성기나 보고서 마법사를 사용하여 보고서를 만들 수 있습니다. 이 자습서에서는 보고서 프로젝트를 만들고, 연결 정보를 설정하고, 쿼리를 정의하고, 테이블 데이터 영역을 추가하고, 필드를 그룹화하거나 필드 합계를 구하고, 보고서를 미리 보는 방법을 배웁니다.  
  
> [!NOTE]  
>  이 자습서를 완료하려면 기본 모드로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]가 실행되고 있어야 합니다. SharePoint 통합 모드로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 실행하는 경우 보고서 서버 URL을 사용하는 단계가 작동하지 않습니다. 에 대 한 자세한 내용은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 모드를 참조 하세요 [Reporting Services 보고서 서버](reporting-services-report-server.md)합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서를 사용하려면 시스템에 다음 항목이 설치되어야 합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 기본 모드의 데이터베이스 엔진  
  
-   [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스.  자세한 내용은 [(SQL Server 2012 용 Adventure Works) SQL Server 2012 용 Adventure Works](http://go.microsoft.com/fwlink/?LinkId=245471) (http://go.microsoft.com/fwlink/?LinkId=245471).합니다. 지원에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 예제 데이터베이스 및 샘플 코드 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]를 참조 하세요 [데이터베이스 및 예제 개요](http://go.microsoft.com/fwlink/?LinkId=110391) CodePlex 웹 사이트에서.  
  
-   [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]입니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNote64Samp](../includes/ssnote64samp-md.md)]  
  
 데이터를 검색 하는 읽기 전용 권한이 있어야 합니다 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
## <a name="tasks"></a>태스크  
 [1 단원: 보고서 서버 프로젝트 만들기 &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)  
  
 [2 단원: 연결 정보 지정 &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)  
  
 [3 단원: 테이블 보고서에 대 한 데이터 집합 정의 &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)  
  
 [4 단원: 보고서에 테이블 추가 &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)  
  
 [5 단원: 보고서 서식 지정 &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)  
  
 [6 단원: 그룹화 및 합계 추가 &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)  
  
> [!NOTE]  
>  자습서를 검토할 때 추가 하는 것이 좋습니다 **다음** 하 고 **이전** 문서 뷰어 도구 모음 단추입니다. 자세한 내용은 다음을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services&#40;SSRS&#41; 자습서](reporting-services-tutorials-ssrs.md)  
  
  
