---
title: 특정 쿼리 문자열 매개 변수가 있는 모바일 보고서 열기 | Microsoft Docs
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7204574d10b674c7cea4e08fb570c3550fe33e03
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52393646"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>특정 쿼리 문자열 매개 변수가 있는 모바일 보고서 열기 | Reporting Services
매개 변수가 포함된 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서와 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 데이터 원본이 있는 경우 매개 변수가 지정한 값으로 자동으로 열리도록 보고서 URL에 쿼리 문자열 매개 변수를 포함할 수 있습니다. 
1.  [매개 변수가 포함된 모바일 보고서](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

2. 모바일 보고서 게시자에서 보고서를 열고 데이터 탭을 선택합니다. 

2. 테이블의 맨 아래에 있는 탭에서 데이터 세트의 이름과 원하는 필드 이름을 찾습니다. 
    
    ![mobile-report-publisher-parameter-data-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  URL 구문은 데이터 원본에 따라 다릅니다. 

     **SQL Server Analysis Services 데이터 원본**: 쿼리 문자열 매개 변수를 사용하여 다음 형식으로 URL을 빌드합니다.

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    예를 들어 다음과 같이 사용할 수 있습니다.
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **SQL Server 데이터 원본**: 쿼리 문자열 매개 변수는 거의 동일하지만 필드 이름 앞에 \@ 기호가 있습니다.

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    예를 들어 다음과 같이 사용할 수 있습니다.
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  이 URL에서는 서버에 있는 보고서가 지정한 매개 변수 값으로 자동 필터링되어 열립니다.

    ![mobile-report-publisher-parameter-web-portal-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>관련 항목:

[모바일 보고서에 매개 변수 추가](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

