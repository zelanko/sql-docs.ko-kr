---
title: "데이터 처리 확장 프로그램에 대 한 Command 클래스 구현 | Microsoft Docs"
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
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: b601aa43ecce5347f7229999455360be761f3bd3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>데이터 처리 확장 프로그램에 대한 Command 클래스 구현
  **명령** 개체는 요청을 생성 하 고 데이터 원본에 전달 합니다. 명령 텍스트는 텍스트 및 XML을 비롯하여 다양한 구문 형식을 취할 수 있습니다. 결과 반환 되는 경우는 **명령** 와 결과 반환 하는 개체는 **DataReader** 개체입니다.  
  
 만들려는 **명령** 클래스를 구현 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>합니다. 구현 된 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 으로 설정 된 결과 반환 하는 메서드는 **DataReader** 개체입니다. <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 방식의 프로그램 **명령** 클래스에 사용 하는 구현이 포함 되어야는 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> 인수로 열거형입니다. 데이터 처리 확장 프로그램을 보고서 디자이너에 배포할 경우 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> 메서드에서 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 사례를 처리하는 구현을 제공합니다. 스키마 전용 구현은 보고서 디자이너에 필드 목록을 제공하는 데 사용됩니다. **DataReader** 에서 반환 된 개체는 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 열을 결과 집합에서 또는 메서드는 필드에 대 한 유형 및 이름 정보가 포함 되어야 합니다.  
  
 필요에 따라 프로그램 **명령** 클래스를 구현할 수 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>합니다. 이 인터페이스를 통해 구현 클래스에서 쿼리를 분석하고 쿼리의 매개 변수 목록을 반환할 수 있습니다. <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 인터페이스의 기능은 보고서 디자이너에서만 사용됩니다. <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>를 구현하면 보고서가 미리 보기 모드에서 실행될 때마다 보고서 디자이너 사용자로 하여금 매개 변수를 결정하도록 할 수 있습니다. 또한 매개 변수를 볼 수 있습니다는 **매개 변수** 탭은 **데이터 집합** 대화 상자.  
  
> [!NOTE]  
>  사용자 지정 데이터 처리 확장 프로그램에서 매개 변수를 지원하지 않는 경우 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>를 구현하면 안 됩니다.  
  
 샘플 **명령** 클래스 구현을 참조 하십시오. [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

