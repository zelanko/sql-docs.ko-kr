---
title: URL에 장치 정보 설정 지정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: dacc371522447f3af056fcde3a48b6d4fca886c9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186009"
---
# <a name="specify-device-information-settings-in-a-url"></a>URL에 장치 정보 설정 지정
  장치 정보 설정은 렌더링 확장 프로그램에 전달되는 매개 변수입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 보고서 서버 웹 서비스의 메서드를 사용하여 보고서를 렌더링하는 경우 `DeviceInfo` XML 요소가  입력 매개 변수로 전달됩니다. 자식 요소는 `DeviceInfo` 요소 다른 렌더링 확장 프로그램의 장치 정보 설정에 따라 다릅니다. *rc:tag=value* 매개 변수 문자열을 사용하여 URL에 장치 정보 설정을 포함시킬 수 있습니다. 여기서 *tag* 는 액세스되는 장치 정보 설정 요소의 이름입니다. 장치 정보 설정에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], 참조 [장치 정보 설정을 렌더링 확장 프로그램에 전달](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 이미지 렌더링 확장 프로그램의 *OutputFormat* 장치 정보 설정을 사용하여 지정된 보고서의 형식을 JPEG으로 설정합니다(읽기 쉽도록 줄 바꿈 추가됨).  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  