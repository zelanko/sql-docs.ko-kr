---
title: 렌더링 확장 프로그램 개요 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fd9604fb38d20e03f33623bacb606d1a9d114ae9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092489"
---
# <a name="rendering-extensions-overview"></a>렌더링 확장 프로그램 개요
  렌더링 확장 프로그램은 보고서 데이터 및 레이아웃 정보를 장치별 형식으로 변환하는 보고서 서버의 구성 요소 또는 모듈입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에는 HTML, Excel, Word, CSV 또는 텍스트, XML, 이미지 및 PDF의 7개 렌더링 확장 프로그램이 포함되어 있습니다. 추가 렌더링 확장 프로그램을 만들어 다른 형식으로 보고서를 생성할 수 있습니다.  
  
> [!NOTE]  
>  사용 가능한 렌더링 확장 프로그램을 확인하려면 RSReportServer.config 파일에서 설치된 확장 프로그램 목록을 볼 수 있습니다.  
  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함된 렌더링 확장 프로그램을 설명합니다.  
  
|Extension Name|Description|  
|--------------------|-----------------|  
|`XML`|보고서를 XML로 렌더링합니다. 보고서가 브라우저에서 열립니다. 이 XML 출력에 적용되는 추가 변환은 고유의 렌더링 확장 프로그램을 개발하지 않아도 되도록 하여 비용 효율적인 방법이 될 수 있습니다.|  
|`CSV`|보고서를 쉼표로 분리된 형식으로 렌더링합니다. 보고서가 CSV 파일 형식과 연결된 보기 도구에서 열립니다.|  
|`IMAGE`|보고서를 페이지 형식으로 렌더링합니다. 이 형식은 보고서 도구 모음의 내보내기 드롭다운에 **TIFF**로 표시됩니다.|  
|`PDF`|보고서를 Adobe Acrobat Reader 형식으로 렌더링합니다. 이 형식은 보고서 도구 모음의 내보내기 드롭다운에 **Acrobat(PDF) 파일**로 표시됩니다.|  
|`EXCEL`|보고서를 [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] 형식으로 표시합니다.|  
|`WORD`|보고서를 [!INCLUDE[ofprword](../../../includes/ofprword-md.md)] 형식으로 표시합니다.|  
|`HTML 4.0`(HTML 렌더링 확장 프로그램의 일부)|HTML은 초기에 보고서를 렌더링하는 데 사용되는 형식입니다. HTML 4.0을 지원하는 브라우저인 경우 이 형식이 사용됩니다. 그렇지 않은 경우 HTML 3.2가 사용됩니다.|  
|`MHTML`(HTML 렌더링 확장 프로그램의 일부)|보고서를 MHTML로 렌더링합니다. 보고서가 Internet Explorer에서 열립니다. 이 형식은 보고서 도구 모음의 내보내기 드롭다운에 **웹 보관 파일**로 표시됩니다.|  
|`NULL`|보고서를 특정 형식으로 렌더링하지 않습니다. 이 렌더링 확장 프로그램은 보고서를 캐시에 두는 데 유용합니다. Null 렌더링은 예약된 실행 또는 배달과 함께 사용되어야 합니다.|  
  
 권장되는 형식 및 용도에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서 구현되고 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함된 각 렌더링 확장 프로그램은 공용 인터페이스 집합을 사용합니다. 이를 통해 각 확장 프로그램에서는 동등한 수준의 기능을 구현하고 보고서 서버의 핵심에 있는 렌더링 코드의 복잡성을 줄입니다.  
  
## <a name="rendering-object-model"></a>렌더링 개체 모델  
 보고서를 처리했을 때 나오는 결과는 ROM(렌더링 개체 모델)이라고 하는 공개적으로 표시되는 개체 모델입니다. 렌더링 개체 모델은 처리된 보고서의 내용, 레이아웃 및 데이터를 정의하는 클래스 모음입니다. ROM은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]용 사용자 지정 렌더링 확장 프로그램을 디자인, 개발 및 배포하려는 개발자가 사용할 수 있습니다. ROM은 보고서 서버에서 사용자 정의 보고서 데이터와 함께 보고서의 XML 정의를 처리할 때 만들어집니다. 처리가 완료되면 렌더링 확장 프로그램에서 공용 개체 모델을 사용하여 보고서의 출력을 정의합니다. ROM의 사용 가능한 공개 클래스는 `Microsoft.ReportingServices.OnDemandReportRendering` 네임스페이스에서 정의됩니다.  
  
## <a name="writing-custom-rendering-extensions"></a>사용자 지정 렌더링 확장 프로그램 작성  
 사용자 지정 렌더링 확장 프로그램을 만들도록 결정하기 전에 더 간단한 다른 방법이 있는지 평가해야 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   기존 확장 프로그램에 대한 장치 정보 설정을 지정하여 렌더링되는 출력을 사용자 지정합니다.  
  
-   XSL 변환(XSLT)과 XML 렌더링 형식 출력을 결합하여 사용자 지정 서식 및 표시 기능을 추가합니다.  
  
 사용자 지정 렌더링 확장 프로그램 작성은 어려운 작업입니다. 렌더링 확장 프로그램은 일반적으로 가능한 모든 보고서 요소 조합을 지원해야 하며 수많은 클래스, 인터페이스, 메서드 및 속성 구현이 필요합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함되지 않은 형식으로 보고서를 렌더링해야 하고 렌더링 확장 프로그램의 고유한 관리 코드 구현을 작성하려는 경우, 렌더링 확장 프로그램 코드는 보고서 서버에서 요구되는 `Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension` 인터페이스를 구현해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 대한 추가 설명서 및 백서는 [Reporting Services 웹 사이트](http://go.microsoft.com/fwlink/?LinkId=19951)에서 최신 기술 리소스를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [렌더링 확장 프로그램 구현](implementing-a-rendering-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
