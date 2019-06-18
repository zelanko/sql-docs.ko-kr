---
title: Reporting Services 배달 확장 프로그램 설정 | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b801fc7ada9e370d12388ba341259f1c13c7a0f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128846"
---
# <a name="reporting-services-delivery-extension-settings"></a>Reporting Services 배달 확장 프로그램 설정
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에는 메일 배달 확장 프로그램 및 파일 공유 배달 확장 프로그램이 포함되어 있습니다. 전자 메일 배달 확장 프로그램은 보고서를 개별 사용자 또는 그룹에 전자 메일로 보낼 수 있는 방법을 제공합니다. 파일 공유 배달 확장 프로그램의 경우 렌더링된 보고서를 네트워크의 공유 위치로 자동으로 보낼 수 있습니다. 표준 구독 또는 데이터 기반 구독에서 지원되는 배달 확장 프로그램 중 하나를 사용할 수 있습니다. <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>,<xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>,<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 및 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 메서드를 호출할 때마다 배달 확장 프로그램 유형에 대한 특정 배달 설정을 전달합니다. 배달 설정 목록을 프로그래밍 방식으로 검색하려면 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 메서드를 사용합니다.  
  
> [!NOTE]  
>  배달 확장 프로그램 설정은 대소문자를 구분합니다.  
  
## <a name="e-mail-delivery-settings"></a>전자 메일 배달 설정  
 다음 표는 보고서 서버 전자 메일을 사용하는 구독을 위한 전자 메일 배달 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**TO**|전자 메일 메시지의 **To** 줄에 표시되는 전자 메일 주소입니다. 여러 개의 전자 메일 주소는 세미콜론으로 구분됩니다. 필수 사항입니다.|  
|**CC**|전자 메일 메시지의 **Cc** 줄에 표시되는 전자 메일 주소입니다. 여러 개의 전자 메일 주소는 세미콜론으로 구분됩니다. (선택 사항)|  
|**BCC**|전자 메일 메시지의 **Bcc** 줄에 표시되는 전자 메일 주소입니다. 여러 개의 전자 메일 주소는 세미콜론으로 구분됩니다. (선택 사항)|  
|**ReplyTo**|전자 메일 메시지의 **Reply-To** 머리글에 표시되는 전자 메일 주소입니다. 값은 단일 전자 메일 주소여야 합니다. (선택 사항)|  
|**IncludeReport**|전자 메일 배달에 보고서를 포함시킬지 여부를 나타내는 값입니다. **true** 값은 보고서가 전자 메일 메시지의 본문으로 배달됨을 나타냅니다.|  
|**RenderFormat**|렌더링된 보고서를 생성하는 데 사용할 렌더링 확장 프로그램의 이름입니다. 이름은 보고서 서버에 설치되었으며 표시되는 렌더링 확장 프로그램의 이름과 일치해야 합니다. 이 값은 **IncludeReport** 설정이 **true** 값으로 설정된 경우에 필요합니다.|  
|**Priority**|전자 메일 메시지를 전송하는 우선 순위입니다. 유효한 값은 **LOW**, **NORMAL** 및 **HIGH**입니다. 기본값은 **NORMAL**입니다.|  
|**Subject**|전자 메일 메시지의 제목 줄 텍스트입니다.|  
|**설명**|전자 메일 메시지의 본문에 포함된 텍스트입니다.|  
|**IncludeLink**|전자 메일 본문에 보고서에 대한 링크를 포함시킬지 여부를 나타내는 값입니다.|  
  
## <a name="file-share-delivery-settings"></a>파일 공유 배달 설정  
 다음 표는 구독을 위한 파일 공유 배달 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**FILENAME**|디스크에 저장되는 파일의 이름입니다.|  
|**FILEEXTN**|렌더링된 보고서에 대한 파일 확장명을 포함시킬지 여부를 나타냅니다. 값은 **true** 또는 **false**입니다.|  
|**PATH**|보고서를 저장할 폴더 경로 또는 UNC 파일 공유 경로입니다.|  
|**RENDER_FORMAT**|디스크에 저장되는 보고서의 형식입니다.|  
|**USERNAME**|네트워크 리소스 또는 디스크에 액세스하는 데 필요한 사용자 이름입니다.|  
|**PASSWORD**|네트워크 리소스 또는 디스크에 액세스하는 데 필요한 암호입니다.|  
|**WRITEMODE**|디스크에 액세스할 때 사용할 쓰기 모드입니다. 유효한 값은 **None**, **Overwrite** 및 **AutoIncrement**입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [웹 서비스 및 .NET Framework를 사용하여 애플리케이션 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
