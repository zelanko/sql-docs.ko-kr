---
title: rsServerConfigurationError - Reporting Services 오류 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a0017be7f7ac6117c1512cbaf3e46b662f0a06f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021685"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services 오류
    
## <a name="details"></a>설명  
  
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
  
 와 함께 제공 되는 추가 오류 메시지 정보를 검토 하는 `rsServerConfiguration` 오류 \Microsoft SQL Server\MSRS12에 있는 보고서 서버 추적 로그 파일을 검토 합니다.\< n a m e > services\logfiles입니다. 자세한 내용은 [Reporting Services 로그 파일 및 소스](../report-server/reporting-services-log-files-and-sources.md)를 참조하세요.  
  
## <a name="internal-only"></a>내부 전용  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 파일](../report-server/reporting-services-configuration-files.md)   
 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
