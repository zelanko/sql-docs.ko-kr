---
title: "보안 웹 서비스 메서드를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
caps.latest.revision: 36
author: sabotta
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 802070f070222fba573b52bf1f53b2c6eb8ba8b6
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="using-secure-web-service-methods"></a>보안 웹 서비스 메서드 사용
  특정 보고서 서버 웹 서비스 메서드를 호출할 때 보안 연결이 필요할 수 있습니다. 보안 연결을 필요로 하는 메서드에 의해 결정 됩니다는 **SecureConnectionLevel** RSReportServer.config 파일에 설정 합니다. 이 설정의 값은 0 이상의 유효 범위를 가진 정수 값입니다. 다음 표에서는 이러한 값에 대해 설명합니다.  
  
|Level|Description|  
|-----------|-----------------|  
|**0**|안전하지 않습니다. Reporting Services SOAP API에 대해 이루어지는 호출에 보안 연결이 필요하지 않습니다.|  
|보다 큰 **0**|보안. Reporting Services SOAP API에 대해 이루어지는 모든 호출에 보안 연결이 필요합니다.|  
  
 웹 서비스의 <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> 메서드를 사용하여 보고서 서버의 현재 구성에 따라 보안 연결이 필요한 웹 서비스 메서드 목록을 반환할 수 있습니다. SSL 시나리오에서는 <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>를 통해 반환된 메서드 목록을 평가하고 웹 서비스 URI의 스키마 이름을 호출되는 메서드에 따라 "https" 또는 "http"로 변경해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
