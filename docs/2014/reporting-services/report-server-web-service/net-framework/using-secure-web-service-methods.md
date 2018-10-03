---
title: 보안 웹 서비스 메서드 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 84dd6a3dcf6ca60a2f0af92064777ae5e204c31d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074457"
---
# <a name="using-secure-web-service-methods"></a>보안 웹 서비스 메서드 사용
  특정 보고서 서버 웹 서비스 메서드를 호출할 때 보안 연결이 필요할 수 있습니다. 보안 연결이 필요한 메서드는 RSReportServer.config 파일의 `SecureConnectionLevel` 설정에서 결정됩니다. 이 설정의 값은 0 이상의 유효 범위를 가진 정수 값입니다. 다음 표에서는 이러한 값에 대해 설명합니다.  
  
|Level|Description|  
|-----------|-----------------|  
|**0**|안전하지 않습니다. Reporting Services SOAP API에 대해 이루어지는 호출에 보안 연결이 필요하지 않습니다.|  
|**0**보다 큼|보안. Reporting Services SOAP API에 대해 이루어지는 모든 호출에 보안 연결이 필요합니다.|  
  
 웹 서비스의 <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> 메서드를 사용하여 보고서 서버의 현재 구성에 따라 보안 연결이 필요한 웹 서비스 메서드 목록을 반환할 수 있습니다. SSL 시나리오에서는 <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>를 통해 반환된 메서드 목록을 평가하고 웹 서비스 URI의 스키마 이름을 호출되는 메서드에 따라 "https" 또는 "http"로 변경해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../report-server-web-service.md)  
  
  
