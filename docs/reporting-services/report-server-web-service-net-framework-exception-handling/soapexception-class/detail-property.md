---
title: Detail 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 737dd12eb9cf2f2000c058ffb1af2b3fb98bcae0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="detail-property"></a>Detail 속성
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException**클래스의 **Detail** 속성은 다음 XML 구조를 가집니다.  
  
## <a name="elements"></a>요소  
 **Detail**  
 모든 기타 오류 세부 정보 요소를 포함하는 최상위 요소입니다.  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 특정 오류 코드입니다.  
  
 **HttpStatus**  
 HTTP 상태 코드입니다.  
  
 **메시지**  
 보고서 서버에서 할당한 오류 메시지 및 오류 코드입니다.  
  
 **HelpLink**  
 오류에 대한 추가 정보를 찾을 수 있는 웹 사이트에 대한 도움말 링크 URL입니다. 자세한 내용은 [HelpLink 요소](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)를 참조하세요.  
  
 **LinkID**  
 링크에 할당된 ID입니다.  
  
 **ProductName**  
 제품의 이름입니다. 기본값은 **Microsoft SQL Server Reporting Services**입니다.  
  
 **ProductVersion**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 버전입니다. 최대 길이는 15자입니다. 버전 번호의 형식은 8.00.0xxx.00과 같아야 합니다.  
  
 **ProductLocaleId**  
 응용 프로그램 INTL DLL의 로캘 ID 또는 언어 ID입니다(예: 0x41A).  
  
 **OperatingSystem**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]가 설치된 운영 체제입니다. 유효한 값은 운영 체제에 대해 독립적인 경우 **0**, [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)]의 경우 **1**, Windows XP의 경우 **16**입니다.  
  
 **CountryLocaleId**  
 운영 체제의 로캘 ID 또는 언어 ID입니다. 예를 들어 프랑스어 버전 Windows에 대해 이 값은 0x040c입니다.  
  
 **MoreInformation**  
 메서드 실행 중 발생한 중첩된 예외를 포함하는 XML 문자열입니다.  
  
 **원본**  
 **MoreInformation**의 자식 요소입니다. 오류의 출처입니다.  
  
 **메시지**  
 **MoreInformation**의 자식 요소입니다. 중첩된 예외의 오류 메시지입니다. 이 요소에는 **ErrorCode** 및 **HelpLink**에 대한 XML 요소가 포함됩니다.  
  
 **경고**  
 보고서 처리에서 반환된 경고를 포함하는 XML 문자열입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail 속성을 사용하여 특정 오류 처리](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
