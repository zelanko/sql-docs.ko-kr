---
title: "Reporting Services WMI 공급자 라이브러리 참조 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- Reporting Services WMI Provider Library
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce7657f048154ab0cf68c8e160bf1e5e6d15c210
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Reporting Services WMI 공급자 라이브러리 참조(SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI(Windows Management Instrumentation) 공급자는 보고서 서버 및 보고서 관리자의 설정을 수정하는 스크립트 및 코드를 쓸 수 있도록 WMI 작업을 지원합니다.  
  
 예를 들어, 보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 통합 보안 사용 여부를 변경하려면 MSReportServer_ConfigurationSetting 클래스의 인스턴스를 만들고 보고서 서버 인스턴스의 DatabaseIntegratedSecurity 속성을 사용합니다. 다음 표에 표시된 클래스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소를 나타냅니다. 클래스는 [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] 또는 [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] 네임스페이스에 정의됩니다. 각 클래스는 읽기 및 쓰기 작업을 지원합니다. 만들기 작업은 지원되지 않습니다.  
  
## <a name="classes"></a>클래스  
 [MSReportServer_Instance 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 클라이언트에서 설치된 보고서 서버에 연결하는 데 필요한 기본 정보를 제공합니다.  
  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 보고서 서버 인스턴스의 설치 및 런타임 매개 변수를 나타냅니다. 이러한 매개 변수는 보고서 서버의 구성 파일에 저장됩니다.  
  
 WMI 작업에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK에 포함되어 있는 WMI SDK 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services WMI 공급자 액세스](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [기술 참조&#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
