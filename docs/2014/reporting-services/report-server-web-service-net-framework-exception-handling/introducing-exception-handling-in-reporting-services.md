---
title: Reporting Services의 예외 처리 소개 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 091b1f40d293515617e369b750a5f18dfe12951b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63012320"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Reporting Services의 예외 처리 소개
  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션이 보고서 서버 웹 서비스에서 처리할 수 없는 요청을 보낼 경우 이 서비스는 SOAP 예외를 클라이언트에 반환합니다. 보고서 서버 웹 서비스에서 throw된 예외에 대한 처리는 개발하는 애플리케이션에서 중요한 부분입니다. 이러한 처리를 통해 오류 발생 시 사용자에게 유용한 정보를 반환할 수 있기 때문입니다.  
  
 이 섹션에는 예외 처리, 유효하지 않은 사용자 입력 방지, 사용자에게 의미 있는 오류 정보 반환 등에 대한 정보가 포함되어 있습니다. 예외 처리에 대 한 일반적인 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서의 "예외 처리 및 throw"를 참조 하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[Reporting Services의 예외 처리](handling-exceptions-in-reporting-services.md)|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서의 예외에 대해 개략적으로 설명하고 웹 서비스 반환 오류에서 SOAP의 역할에 대해 설명합니다.|  
|[Reporting Services 예외 처리를 위한 최상의 방법](best-practices/best-practices-for-reporting-services-exception-handling.md)|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 예외를 처리하는 방법에 대한 권장 사항을 제공합니다.|  
|[Reporting Services SoapException 클래스](soapexception-class/reporting-services-soapexception-class.md)|
  **의 **SoapException[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 클래스에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스 및 .NET Framework를 사용하여 애플리케이션 빌드](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
