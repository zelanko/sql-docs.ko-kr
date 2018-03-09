---
title: "Reporting Services 예외 처리에 관한 모범 사례 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e6ae230c7d3e21ad4b5ac19ab791f63db8d51c50
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Reporting Services 예외 처리를 위한 최상의 방법
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 응용 프로그램을 개발할 때 예외 발생을 없애거나 줄이기 위해 사용할 수 있는 방법이 다수 있습니다. 예외가 발생하면 사용자에게 간단 명료한 오류 메시지를 제공하고 적절한 예외 처리를 추가하여 응용 프로그램이 갑자기 종료되지 않도록 합니다.  
  
 보고서 서버 웹 서비스에 요청을 보내는 응용 프로그램은 다음 기능을 수행해야 합니다.  
  
-   잘못된 요청을 최대한 방지하여 예외 발생을 막습니다.  
  
-   예외를 catch하고 가능한 경우 항상 특정 오류 처리 코드를 제공합니다.  
  
-   예외를 throw하지 않는 오류 사례를 처리합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[잘못된 요청 방지](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|잘못된 요청이 보고서 서버에 전송되지 않도록 하기 위한 기술에 대해 설명합니다.|  
|[Try 및 Catch 블록 사용](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|try/catch 블록으로 응용 프로그램의 안정성을 향상시킬 수 있는 방법을 설명합니다.|  
|[예외를 발생하지 않는 경고 및 사례 처리](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 예외가 throw되지 않는 오류를 처리하는 방법을 설명합니다.|  
|[Detail 속성을 사용하여 특정 오류 처리](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|**SoapException** 개체의 **Detail** 속성을 사용하여 특정 오류를 프로그래밍 방식으로 처리하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Detail 속성](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
