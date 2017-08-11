---
title: "보고서 서버 시스템 속성 | Microsoft Docs"
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
- report servers [Reporting Services], properties
- system-specific properties [Reporting Services]
ms.assetid: cd874117-00e5-4ae6-8629-eb9ba9f40478
caps.latest.revision: 55
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: d91c1bb43978ab08857c09ffc235da78f5f0ffea
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="reporting-services-properties---report-server-system-properties"></a>보고 서비스 속성-보고서 서버 시스템 속성
  다음 시스템 속성 이름은 예약되어 있습니다. 동일한 이름의 사용자 정의 속성을 만들 수 없습니다. 이러한 속성 중 상당수는 웹 서비스 메서드를 사용하여 읽거나 수정할 수 있습니다.  
  
## <a name="properties"></a>속성  
  
|속성|Description|  
|--------------|-----------------|  
|SiteName|사용자 인터페이스에 표시되는 보고서 서버 사이트의 이름입니다. 기본값은 **Microsoft 보고서 서버**합니다. 이 속성은 빈 문자열일 수 있습니다. 최대 길이는 8,000자입니다.|  
|SystemSnapshotLimit|하나의 보고서에 대해 저장되는 최대 스냅숏 수입니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 스냅숏 제한이 없습니다.|  
|SystemReportTimeout|보고서 서버 네임스페이스에서 관리되는 모든 보고서에 대한 기본 보고서 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 **1800**입니다.|  
|UseSessionCookies|보고서 서버에서 클라이언트 브라우저와 통신할 때 세션 쿠키를 사용해야 하는지 여부를 나타냅니다. 기본값은 **true**입니다.|  
|SessionTimeout|세션이 활성 상태로 유지되는 시간(초)입니다. 기본값은 **600**입니다.|  
|EnableMyReports|내 보고서 기능이 설정되어 있는지 여부를 나타냅니다. **true** 값은 이 기능이 설정되어 있음을 나타냅니다.|  
|MyReportsRole|사용자의 내 보고서 폴더에서 보안 정책을 만들 때 사용된 역할의 이름입니다. 기본값은 **My Reports Role**입니다.|  
|EnableExecutionLogging|보고서 실행 로깅이 설정되어 있는지 여부를 나타냅니다. 기본값은 **true**입니다.|  
|ExecutionLogDaysKept|실행 로그에 보고서 실행 정보를 보관하는 일 수입니다. 이 속성에 유효한 값은 **0** 부터 **2**,**147**,**483**,**647**까지입니다. 값이 **0** 이면 실행 로그 테이블에서 항목이 삭제되지 않습니다. 기본값은 **60**입니다.|  
|SnapshotCompression|스냅숏의 압축 방식을 정의합니다. 기본값은 **SQL**입니다. 유효한 값은 다음과 같습니다.<br /><br /> **SQL** = 보고서 서버 데이터베이스에 저장 될 때 스냅숏이 압축 됩니다. 이것은 현재 동작입니다.<br /><br /> **None =** 스냅숏이 압축되지 않습니다.<br /><br /> **모든** = 보고서 서버 데이터베이스 또는 파일 시스템을 포함 하는 모든 저장소 옵션에 대해 스냅숏이 압축 됩니다.|  
|EnableClientPrinting|보고서 서버에서 RSClientPrint ActiveX 컨트롤을 다운로드할 수 있는지 여부를 지정합니다. 유효한 값은 **true** 및 **false**입니다. 기본값은 **true**입니다. 이 컨트롤에 필요한 추가 설정에 대한 자세한 내용은 [Reporting Services에 대해 클라이언트 쪽 인쇄 사용 및 사용 안 함](../../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)을 참조하세요.|  
|EnableIntegratedSecurity|보고서 데이터 원본 연결에 통합 보안이 지원되는지 여부를 지정합니다. 기본값은 **True**입니다. 유효한 값은 다음과 같습니다.<br /><br /> **True** = 통합 보안을 사용 합니다.<br /><br /> **False** = 통합 보안이 사용 되지 않습니다. 통합 보안을 사용하도록 구성된 보고서 데이터 원본이 실행되지 않습니다.|  
|EnableRemoteErrors|원격 컴퓨터에서 보고서를 요청하는 사용자에 대해 반환되는 오류 메시지에 외부 오류 정보(예: 보고서 데이터 원본에 대한 오류 정보)를 포함합니다. 유효한 값은 **true** 및 **false**입니다. 기본값은 **false**입니다. 자세한 내용은 [원격 오류 사용&#40;Reporting Services&#41;](../../../reporting-services/report-server/enable-remote-errors-reporting-services.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>   
 <xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>   
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
