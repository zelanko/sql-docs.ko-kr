---
title: "Reporting Services 배달 확장 프로그램 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
- XML Web service [Reporting Services], delivery extension settings
- Report Server Web service, delivery extension settings
- delivery [Reporting Services]
- network share delivery [Reporting Services]
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- mailing reports [Reporting Services]
- sharing reports
- extensions [Reporting Services], delivery
- mail [Reporting Services]
- Web service [Reporting Services], delivery extension settings
ms.assetid: 68c31a85-261c-4ec4-b8df-1f9842b46f8a
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 668c3d31af5f287d7d254c2dc666e20a5f6328fa
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-delivery-extension-settings"></a>Reporting Services 배달 확장 프로그램 설정
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]전자 메일 배달 확장 프로그램과 파일 공유 배달 확장 프로그램이 포함 되어 있습니다. 전자 메일 배달 확장 프로그램은 보고서를 개별 사용자 또는 그룹에 전자 메일로 보낼 수 있는 방법을 제공합니다. 파일 공유 배달 확장 프로그램의 경우 렌더링된 보고서를 네트워크의 공유 위치로 자동으로 보낼 수 있습니다. 표준 구독 또는 데이터 기반 구독에서 지원되는 배달 확장 프로그램 중 하나를 사용할 수 있습니다. <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>,<xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>,<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 및 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 메서드를 호출할 때마다 배달 확장 프로그램 유형에 대한 특정 배달 설정을 전달합니다. 배달 설정 목록을 프로그래밍 방식으로 검색하려면 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 메서드를 사용합니다.  
  
> [!NOTE]  
>  배달 확장 프로그램 설정은 대소문자를 구분합니다.  
  
## <a name="e-mail-delivery-settings"></a>전자 메일 배달 설정  
 다음 표는 보고서 서버 전자 메일을 사용하는 구독을 위한 전자 메일 배달 설정을 나열합니다.  
  
|설정|Value|  
|-------------|-----------|  
|**받는 사람**|에 표시 되는 전자 메일 주소는 **를** 전자 메일 메시지의 줄입니다. 여러 개의 전자 메일 주소는 세미콜론으로 구분됩니다. 필수 사항입니다.|  
|**참조**|에 표시 되는 전자 메일 주소는 **Cc** 전자 메일 메시지의 줄입니다. 여러 개의 전자 메일 주소는 세미콜론으로 구분됩니다. (선택 사항)|  
|**숨은 참조**|에 표시 되는 전자 메일 주소는 **숨은 참조** 전자 메일 메시지의 줄입니다. 여러 개의 전자 메일 주소는 세미콜론으로 구분됩니다. (선택 사항)|  
|**ReplyTo**|에 표시 되는 전자 메일 주소는 **회신** 전자 메일 메시지의 헤더입니다. 값은 단일 전자 메일 주소여야 합니다. (선택 사항)|  
|**보고서**|전자 메일 배달에 보고서를 포함시킬지 여부를 나타내는 값입니다. 값이 **true** 전자 메일 메시지의 본문에 보고서가 배달 나타냅니다.|  
|**RenderFormat**|렌더링된 보고서를 생성하는 데 사용할 렌더링 확장 프로그램의 이름입니다. 이름은 보고서 서버에 설치되었으며 표시되는 렌더링 확장 프로그램의 이름과 일치해야 합니다. 이 값은 필요는 **보고서** 의 값으로 설정 되어 **true**합니다.|  
|**Priority**|전자 메일 메시지를 전송하는 우선 순위입니다. 유효한 값은 **낮은**, **보통**, 및 **높은**합니다. 기본값은 **보통**합니다.|  
|**Subject**|전자 메일 메시지의 제목 줄 텍스트입니다.|  
|**설명**|전자 메일 메시지의 본문에 포함된 텍스트입니다.|  
|**IncludeLink**|전자 메일 본문에 보고서에 대한 링크를 포함시킬지 여부를 나타내는 값입니다.|  
  
## <a name="file-share-delivery-settings"></a>파일 공유 배달 설정  
 다음 표는 구독을 위한 파일 공유 배달 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**파일 이름**|디스크에 저장되는 파일의 이름입니다.|  
|**FILEEXTN**|렌더링된 보고서에 대한 파일 확장명을 포함시킬지 여부를 나타냅니다. 값은 **true** 또는 **false**합니다.|  
|**경로**|보고서를 저장할 폴더 경로 또는 UNC 파일 공유 경로입니다.|  
|**RENDER_FORMAT**|디스크에 저장되는 보고서의 형식입니다.|  
|**사용자 이름**|네트워크 리소스 또는 디스크에 액세스하는 데 필요한 사용자 이름입니다.|  
|**암호**|네트워크 리소스 또는 디스크에 액세스하는 데 필요한 암호입니다.|  
|**WRITEMODE**|디스크에 액세스할 때 사용할 쓰기 모드입니다. 유효한 값은 **None**, **덮어쓰기**, 및 **AutoIncrement**합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
