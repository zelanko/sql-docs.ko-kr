---
title: Detail 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 383e356a85597a6b6564584fc375e83f258241b9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019364"
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
 오류에 대한 추가 정보를 찾을 수 있는 웹 사이트에 대한 도움말 링크 URL입니다. 자세한 내용은 [HelpLink 요소](helplink-element.md)를 참조하세요.  
  
 **LinkID**  
 링크에 할당된 ID입니다.  
  
 **ProductName**  
 제품의 이름입니다. 기본값은 **Microsoft SQL Server Reporting Services**입니다.  
  
 **ProductVersion**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 버전입니다. 최대 길이는 15자입니다. 버전 번호의 형식은 다음과 같아야 합니다. 8.00.0xxx.00.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services의 예외 처리 소개](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](reporting-services-soapexception-class.md)   
 [Detail 속성을 사용하여 특정 오류 처리](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
