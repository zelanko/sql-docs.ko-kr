---
title: 렌더링 확장 프로그램 구현 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 56a8294775ccb51cd216c2cd72c955bd9379c004
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643751"
---
# <a name="implementing-a-rendering-extension"></a>렌더링 확장 프로그램 구현
  렌더링 확장 프로그램은 보고서 데이터 및 레이아웃 정보를 장치별 형식으로 변환하는 보고서 서버의 구성 요소 또는 모듈입니다. SQL Server Reporting Services에는 HTML, Excel, Word, CSV 또는 텍스트, XML, 이미지 및 PDF의 6가지 렌더링 확장 프로그램이 포함되어 있습니다. 추가 렌더링 확장 프로그램을 만들어 다른 형식으로 보고서를 생성할 수 있습니다.  
  
> [!NOTE]  
>  사용 가능한 렌더링 확장 프로그램을 확인하려면 RSReportServer.config 파일에서 설치된 확장 프로그램 목록을 볼 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [렌더링 확장 프로그램 개요](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]용 사용자 지정 렌더링 확장 프로그램을 작성하는 방법을 소개합니다.  
  
 [IRenderingExtension 인터페이스 구현](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 렌더링 확장 프로그램의 특성을 설명합니다.  
  
 [렌더링 확장 프로그램 배포](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 보고서 서버에 렌더링 확장 프로그램을 배포하는 방법을 설명합니다.  
  
 [렌더링 확장 프로그램 제거](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 보고서 서버에서 렌더링 확장 프로그램을 제거하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
