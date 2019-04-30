---
title: URL 액세스를 사용하여 보고서 내보내기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 80238e8edb5b84bc353eca63d63491a8ee74c8ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164005"
---
# <a name="export-a-report-using-url-access"></a>URL 액세스를 사용하여 보고서 내보내기
  사용 하 여 보고서를 렌더링할 형식을 지정할 수도 있습니다는 *rs: Format* 매개 변수입니다. 예를 들어 기본 모드 보고서 서버에서 직접 보고서 PDF 복사본을 가져오는 경우 다음을 사용합니다.  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 또한 SharePoint 통합 모드 보고서 서버에서 가져오는 경우 다음을 사용합니다.  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 이 매개 변수의 유효한 값은 액세스할 보고서 서버에 설치된 보고서 렌더링 확장 프로그램을 기반으로 합니다. 일반적인 확장 프로그램은 HTML4.0, MHTML, IMAGE, EXCEL, WORD, CSV, PDF, XML 및 NULL입니다. 지정된 렌더링 확장 프로그램이 보고서 서버에 설치되지 않은 경우 보고서가 렌더링되지 않고 오류가 발생하여 브라우저에 표시됩니다.  
  
 *Format* 매개 변수를 URL의 일부로 포함하지 않으면 보고서 서버가 브라우저를 감지하고 적절한 HTML 형식으로 보고서를 렌더링합니다.  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
