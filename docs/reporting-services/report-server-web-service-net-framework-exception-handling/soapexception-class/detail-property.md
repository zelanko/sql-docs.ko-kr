---
title: "속성에 자세히 설명 | Microsoft Docs"
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
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f2359ac68758ba2846c4a9065f6cb1c9c96a7e01
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="detail-property"></a>Detail 속성
  **세부** 의 속성은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException** 클래스에 다음 XML 구조:  
  
## <a name="elements"></a>요소  
 **세부 정보**  
 모든 기타 오류 세부 정보 요소를 포함하는 최상위 요소입니다.  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 특정 오류 코드입니다.  
  
 **HttpStatus**  
 HTTP 상태 코드입니다.  
  
 **메시지**  
 보고서 서버에서 할당한 오류 메시지 및 오류 코드입니다.  
  
 **HelpLink**  
 오류에 대한 추가 정보를 찾을 수 있는 웹 사이트에 대한 도움말 링크 URL입니다. 자세한 내용은 참조 [HelpLink 요소](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)합니다.  
  
 **LinkID**  
 링크에 할당된 ID입니다.  
  
 **제품 이름**  
 제품의 이름입니다. 기본값은 **Microsoft SQL Server Reporting Services**합니다.  
  
 **ProductVersion**  
 버전의 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]합니다. 최대 길이는 15자입니다. 버전 번호의 형식은 다음과 같아야: 8.00.0xxx.00 합니다.  
  
 **ProductLocaleId**  
 응용 프로그램 INTL DLL의 로캘 ID 또는 언어 ID입니다(예: 0x41A).  
  
 **운영 체제**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]가 설치된 운영 체제입니다. 유효한 값은 **0** 독립적 이며 운영 체제에 대 한 **1** 에 대 한 [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)], 및 **16** Windows XP에 대 한 합니다.  
  
 **CountryLocaleId**  
 운영 체제의 로캘 ID 또는 언어 ID입니다. 예를 들어 프랑스어 버전 Windows에 대해 이 값은 0x040c입니다.  
  
 **자세한 내용**  
 메서드 실행 중 발생한 중첩된 예외를 포함하는 XML 문자열입니다.  
  
 **원본**  
 자식 요소 **MoreInformation**합니다. 오류의 출처입니다.  
  
 **메시지**  
 자식 요소 **MoreInformation**합니다. 중첩된 예외의 오류 메시지입니다. 이 요소에 대 한 XML 특성을 포함 **ErrorCode** 및 **HelpLink**합니다.  
  
 **경고**  
 보고서 처리에서 반환된 경고를 포함하는 XML 문자열입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail 속성을 사용 하 여 특정 오류 처리](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
