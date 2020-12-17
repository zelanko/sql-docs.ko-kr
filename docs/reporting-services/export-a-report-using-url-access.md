---
title: URL 액세스를 사용하여 보고서 내보내기 | Microsoft Docs
description: rs:Format URL 매개 변수로 보고서를 렌더링할 형식을 지정해 URL 액세스를 사용하여 보고서를 내보내는 방법을 알아봅니다.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d61f509fa07528b71cd7cbb23488bc14f33959ae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472494"
---
# <a name="export-a-report-using-url-access"></a>URL 액세스를 사용하여 보고서 내보내기
  *rs:Format* URL 매개 변수를 사용하여 선택적으로 보고서를 렌더링할 형식을 지정할 수 있습니다.  HTML4.0 및 HTM5 형식(렌더링 확장 프로그램)은 브라우저에서 렌더링하고 다른 형식의 경우 브라우저는 로컬 파일에 보고서 출력을 저장하라는 메시지가 나타납니다.  
  
 예를 들어 기본 모드 보고서 서버에서 직접 보고서 PDF 복사본을 가져오는 경우 다음을 사용합니다.  
  
```  
https://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  

::: moniker range="=sql-server-2016"
  
 또한 SharePoint 통합 모드 보고서 서버에서 가져오는 경우 다음을 사용합니다.  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
 
::: moniker-end
 
 예를 들어 브라우저의 다음 URL 명령은 보고서 서버의 명명된 인스턴스에서 PPTX 보고서를 내보냅니다.  
  
```  
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 이 매개 변수의 유효한 값은 액세스할 보고서 서버에 설치된 보고서 렌더링 확장 프로그램을 기반으로 합니다. 일반적인 확장 프로그램은 HTML4.0, MHTML, IMAGE, EXCELOPENXML(xlsx), WORDOPENXML(docx), CSV, PDF, XML 및 NULL입니다. 지정된 렌더링 확장 프로그램이 보고서 서버에 설치되지 않은 경우 보고서가 렌더링되지 않고 오류가 발생하여 브라우저에 표시됩니다.  
  
 *Format* 매개 변수를 URL의 일부로 포함하지 않으면 보고서 서버가 브라우저를 감지하고 적절한 HTML 형식으로 보고서를 렌더링합니다.  
  
## <a name="see-also"></a>참고 항목  
 [URL 액세스&#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)  
  
  
