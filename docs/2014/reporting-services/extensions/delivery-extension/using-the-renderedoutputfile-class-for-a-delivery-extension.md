---
title: 배달 확장 프로그램에 대해 RenderedOutputFile 클래스 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: 33
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 069fd2ec6a57bd082722cd19b0edab51fe9d2d4e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181529"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>배달 확장 프로그램에 대해 RenderedOutputFile 클래스 사용
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스는 데이터 스트림 및 데이터 스트림의 연관 속성에 대한 정보를 나타냅니다. <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스의 **Data** 속성은 렌더링된 보고서 또는 보고서 리소스를 **Stream** 개체로 나타내는 데 사용됩니다.  
  
 **Report** 개체의 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> 메서드는 렌더링된 단일 보고서를 구성하는 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체 배열을 하나 이상 반환합니다. 첫 번째 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체는 렌더링된 보고서입니다. 다른 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체는 보고서 데이터(예: HTML 파일 및 연결된 이미지)와 함께 배달되어야 하는 리소스입니다. 단일 스트림 렌더링 확장 프로그램(IMAGE, PDF, MHTML 및 EXCEL)은 배열에 있는 하나의 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체만 반환합니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스 사용 방법에 대한 예는 [SQL Server Reporting Services 제품 예제](http://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [배달 확장 프로그램 구현](implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  