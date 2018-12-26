---
title: 선택적 웹 서비스 개체에 대한 값 생략 | Microsoft Docs
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4d9a155ee59beb30adb14608a3216006739b14f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725821"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>선택적 웹 서비스 개체에 대한 값 생략
  보고서 서버 웹 서비스 복합 유형의 속성은 대부분 Specified 속성으로 알려진 동반 속성을 갖습니다. 속성 이름은 원래 속성 이름에 "Specified"라는 단어를 붙여 만듭니다. 이 속성이 있다면 원래 속성의 값을 가끔씩 생략할 수 있다는 의미입니다. 이는 WSDL(Web Service Description Language)에서 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 프록시 클래스로 변환하는 데 따른 직접적인 결과입니다. 예를 들어, 복합 유형 <xref:ReportService2010.DataSourceDefinition.Enabled%2A>의 웹 서비스 속성 <xref:ReportService2010.DataSourceDefinition>에 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>라는 동반 속성이 있습니다. 애플리케이션을 구축하는 중 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 속성의 값을 설정하지 않으려면 <xref:ReportService2010.DataSourceDefinition.Enabled%2A>의 값을 제공할 필요가 없습니다. 그러면 기본값 **true**가 사용됩니다. 그러나 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>를 **false**로 설정해야 합니다. <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 속성에 값을 제공하려면 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>를 **true**에 해당하는 값으로 설정해야 합니다. 이는 쓰기 가능한 속성의 경우입니다. 읽기 전용 속성의 경우에는 별다른 조치를 하지 않아도 됩니다.  
  
> [!IMPORTANT]  
>  위에 언급한 기술로 속성을 지정하는 데 실패하면 예기치 않은 웹 서비스 동작이 발생할 수 있습니다.  
  
 추가 Specified 속성을 처리하는 데 필요한 데이터 형식은 대개 **Boolean**, **DateTime** 및 **Enumeration**입니다.  
  
 예제는 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 메서드를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
