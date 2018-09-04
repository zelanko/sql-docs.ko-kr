---
title: rsServerConfigurationError - Reporting Services 오류 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 509ae9322e4ed8d23875577dfb56abc5a98962c9
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277669"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services 오류
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|rsServerConfiguration|  
|이벤트 원본|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|구성 요소|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|메시지 텍스트|보고서 서버에서 구성 오류가 발생했습니다.|  
  
## <a name="explanation"></a>설명  
 이는 보고서 도구 또는 보고서 제작 도구에 잘못된 구성 설정이 있는 경우에 일반적으로 발생하는 오류로서, 일반적으로 오류의 실제 원인을 나타내는 두 번째 메시지와 함께 표시됩니다.  
  
 가능한 원인은 다음과 같습니다.  
  
-   RSReportServer.config 또는 RSReportDesigner.config 파일을 찾을 수 없거나 읽을 수 없습니다.  
  
-   구성 파일의 XML 요소가 누락되었거나 잘못되었습니다.  
  
-   하나 이상의 XML 요소에 대한 값이 누락되었거나 잘못되었습니다.  
  
-   레지스트리 설정이 잘못되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 구성 파일을 수동으로 편집한 후에 이 오류가 발생하기 시작했다면 변경 내용을 제거하고 이전 값을 입력하거나 백업이 있는 경우 이전 버전을 복원하세요.  
  
 **rsServerConfiguration** 오류와 함께 표시되는 추가 오류 메시지 정보를 확인하려면 \Microsoft SQL Server\MSRS12.\<instancename >\Reporting Services\LogFiles에 있는 보고서 서버 추적 로그 파일을 검토하세요. 자세한 내용은 [Reporting Services 로그 파일 및 소스](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)를 참조하세요.  
  
## <a name="internal-only"></a>내부 전용  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
