---
title: "선택적 웹 서비스 개체에 대 한 값을 생략 하는 것입니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 3532a470bd036e0128a8df21ca391210cf7209a2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="omitting-values-for-optional-web-service-objects"></a>선택적 웹 서비스 개체에 대한 값 생략
  여러 보고서 서버 웹 서비스 복합 유형의 속성에 표시 된 속성으로 알려진 동반 속성이 있으며 속성 이름은 원래 속성 이름에 "Specified"라는 단어를 붙여 만듭니다. 이 속성이 있다면 원래 속성의 값을 가끔씩 생략할 수 있다는 의미입니다. 이는 WSDL(Web Service Description Language)에서 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 프록시 클래스로 변환하는 데 따른 직접적인 결과입니다. 예를 들어, 복합 유형 <xref:ReportService2010.DataSourceDefinition.Enabled%2A>의 웹 서비스 속성 <xref:ReportService2010.DataSourceDefinition>에 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>라는 동반 속성이 있습니다. 응용 프로그램을 작성 하는 값을 설정 하지 않을 경우는 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 속성을 않아도 대 한 값을 제공 하지 <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; 기본값인 **true** 사용 됩니다. 그러나 여전히 설정 해야 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 를 **false**합니다. 에 대 한 값을 제공 하는 경우는 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 속성을 설정 해야 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 같음 **true**합니다. 이는 쓰기 가능한 속성의 경우입니다. 읽기 전용 속성의 경우에는 별다른 조치를 하지 않아도 됩니다.  
  
> [!IMPORTANT]  
>  위에 언급한 기술로 속성을 지정하는 데 실패하면 예기치 않은 웹 서비스 동작이 발생할 수 있습니다.  
  
 일반적으로 추가 된 속성을 처리 해야 하는 경우 데이터 형식이 **부울**, **DateTime**, 및 **열거형**합니다.  
  
 예제는 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 메서드를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
