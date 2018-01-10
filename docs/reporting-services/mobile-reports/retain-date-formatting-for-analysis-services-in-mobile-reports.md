---
title: "모바일 보고서에서 Analysis Services에 대한 날짜 형식 지정 유지 | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
caps.latest.revision: "3"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a20327b51bd4fa05baa140bd8958dd9ff5486291
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>모바일 보고서에서 Analysis Services에 대한 날짜 형식 지정 유지
보고서 작성기의 공유 데이터 집합에 측정값을 추가하므로 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 데이터 원본의 날짜가 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]의 데이터 형식을 유지합니다.

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 쿼리에 대한 기본 반환 형식은 문자열입니다.  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 작성기에 대한 데이터 집합을 만들 때 문자열 형식이 적용되고 서버에 저장됩니다. 

그러나 JSON 테이블 렌더러가 데이터 집합을 처리할 때 열의 값을 문자열로 읽고 문자열을 렌더링합니다.  [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 에서 테이블을 가져올 때도 문자열만 보입니다.

이에 대한 해결 방법은 보고서 작성기에서 공유 데이터 집합을 만들 때 계산 멤버를 추가하는 것입니다. [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 다차원 모델 및 테이블 형식 모델 모두에 대해 작동합니다.

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>측정값을 만들어 날짜 필드 데이터 형식 유지

1. 측정값을 만들어 요청한 날짜 필드 값을 유지하고, 수식 필드에서 날짜의 계층/수준을 선택하고 **.CurrentMember.MemberValue**를 추가합니다. 예를 들어 다음과 같이 사용할 수 있습니다.
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![ssas-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. 이제 왼쪽 아래의 계산 멤버 목록에서 끌어 오른쪽의 열 표에 놓는 방법으로 열 집합에 이 계산 멤버를 추가할 수 있습니다.  

   ![ssas-query-designer-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>관련 항목:

-  [Data for Reporting Services mobile reports](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [Reporting Services 모바일 보고서에 대한 데이터 준비](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
