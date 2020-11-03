---
title: 특정 쿼리 문자열 매개 변수가 있는 모바일 보고서 열기 | Microsoft Docs
description: 매개 변수 및 데이터 원본을 포함하는 Reporting Services 모바일 보고서의 경우, 보고서 URL에 쿼리 매개 변수를 사용하여 지정된 값으로 보고서를 열 수 있습니다.
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: abcdda5a396451508df78610eeb4f7bc417484d5
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907351"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>특정 쿼리 문자열 매개 변수가 있는 모바일 보고서 열기 | Reporting Services
매개 변수가 포함된 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서와 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 데이터 원본이 있는 경우 매개 변수가 지정한 값으로 자동으로 열리도록 보고서 URL에 쿼리 문자열 매개 변수를 포함할 수 있습니다. 
1.  [매개 변수가 포함된 모바일 보고서](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

2. 모바일 보고서 게시자에서 보고서를 열고 데이터 탭을 선택합니다. 

2. 테이블의 맨 아래에 있는 탭에서 데이터 세트의 이름과 원하는 필드 이름을 찾습니다. 
    
    ![모바일 보고서 게시자 매개 변수 데이터 뷰의 스크린샷](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  URL 구문은 데이터 원본에 따라 다릅니다. 

     **SQL Server Analysis Services 데이터 원본** : 쿼리 문자열 매개 변수를 사용하여 다음 형식으로 URL을 빌드합니다.

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    다음은 그 예입니다.
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **SQL Server 데이터 원본** : 쿼리 문자열 매개 변수는 거의 동일하지만 필드 이름 앞에 \@ 기호가 있습니다.

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    다음은 그 예입니다.
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  이 URL에서는 서버에 있는 보고서가 지정한 매개 변수 값으로 자동 필터링되어 열립니다.

    ![화살표가 URL과 ?TimeChartLoD.@category=Clothing 텍스트 주변 상자를 가리키는 모바일 보고서 게시자 매개 변수 웹 포털 보기의 스크린샷](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>참고 항목

[모바일 보고서에 매개 변수 추가](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

