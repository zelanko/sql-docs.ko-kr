---
title: "RenderedOutputFile 클래스를 사용 하 여 배달 확장 프로그램에 대 한 | Microsoft Docs"
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
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5ebd5ea1a5a96727a77ea78aa1ee9cbc74e6dd81
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>배달 확장 프로그램에 대해 RenderedOutputFile 클래스 사용
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스는 데이터 스트림 및 데이터 스트림의 연관 속성에 대한 정보를 나타냅니다. **데이터** 속성은 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스 렌더링 된 보고서 또는 보고서 리소스를 나타내는 데 사용 되는 **스트림** 개체입니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> 의 메서드는 **보고서** 하나 이상의의 배열을 반환 하는 개체 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 렌더링 된 단일 보고서를 구성 하는 개체입니다. 첫 번째 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체는 렌더링된 보고서입니다. 다른 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체는 보고서 데이터(예: HTML 파일 및 연결된 이미지)와 함께 배달되어야 하는 리소스입니다. 단일 스트림 렌더링 확장 프로그램(IMAGE, PDF, MHTML 및 EXCEL)은 배열에 있는 하나의 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체만 반환합니다.  
  
 사용 하는 방법의 예는 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스를 참조 하십시오. [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
