---
title: "보고서 뷰어 웹 파트는 SharePoint 사이트에서 | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a37ed5efe7c365c601deb95d9fe761d227e7021e
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>보고서 뷰어 웹 파트는 SharePoint 사이트에서

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

보고서 뷰어 웹 파트는 사용자 지정 웹 파트입니다. 웹 파트를 사용 하 여 탐색 하며 인쇄를 SharePoint 사이트 내에서 보고서 서버에서 보고서를 내보낼 수 있습니다. 보고서 뷰어 웹 파트를 보고서 정의 파일 (.rdl)는 Microsoft SQL Server Reporting Services 보고서 서버에서 처리 하는 연관 되어 있습니다. 

최신 보고서 뷰어 웹 파트는 Power BI 보고서 서버에 배포 된 서비스 페이지를 매긴 보고서를 수도 있습니다. Power BI 보고서와 함께 웹 파트를 작동 하지 않습니다.

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>이유는 보고서 뷰어 웹 파트는 다시 도입

보고서 뷰어 웹 파트를 사용할 수 있는 SharePoint 제품용 Reporting Services add-in의 일환으로 합니다. 웹 파트를 SharePoint 통합된 모드로 보고서 서버에 대 한 특정 했습니다. SharePoint 통합된 모드는 SQL Server 2016 후 사용 되지 않았습니다.

Reporting Services에 대 한 하나의 설치 모드는 SQL Server 2017 부터는: **기본 모드**합니다. 사용 하 여 페이지 뷰어 웹 파트를 사용 하 여 모든 보고서 형식을 포함할 수는 *rs: 포함 = true* URL 매개 변수입니다. SharePoint 페이지에 보고서 포함 고객 및 업데이트 된 보고서 뷰어 웹 파트에서 요청 하는 통합 스토리 페이지가 매겨진된 보고서에 대 한 이러한 시나리오가 지원입니다.

페이지 뷰어 웹 파트 페이지 매긴된 보고서를 SharePoint 페이지에 포함 하려면 접미사에 업데이트 된 보고서 뷰어 웹 파트는 추가 기능을 제공 합니다.

* 특정 도구 모음 단추 표시/숨기기
* 보고서 매개 변수 값을 재정의 합니다.
* 보고서 매개 변수를 필터 웹 파트를 연결 합니다.

## <a name="download-the-report-viewer-web-part-solution-package"></a>보고서 뷰어 웹 파트 솔루션 패키지를 다운로드 합니다.

보고서 뷰어 웹 파트를 Microsoft 다운로드 센터에서 사용할 수 있습니다.

[보고서 뷰어 웹 파트 솔루션 패키지를 다운로드 합니다.](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>고려 사항 및 제한 사항

나열 된 항목은 업데이트 된 보고서 뷰어 웹 파트 관련이 있습니다.

* 웹 파트에서 사용할 수 있습니다 *클래식* SharePoint 페이지입니다.
* 보고서 뷰어 웹 파트에 포함 하기 위한 페이지 매긴된 (RDL) 보고서에만 사용할 수 있습니다. Power BI 보고서 또는 모바일 보고서를 포함 하려면 원하는 경우 사용할 수 있습니다는 *rs: 포함 = true* URL 매개 변수입니다.

## <a name="next-steps"></a>다음 단계

업데이트 된 보고서 뷰어 웹 파트와 시작 하려면 참조 [SharePoint 사이트에서 보고서 뷰어 웹 파트 배포](deploy-report-viewer-web-part.md)합니다.

