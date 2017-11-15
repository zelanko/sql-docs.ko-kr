---
title: "서버 속성(보안 페이지) - Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
caps.latest.revision: "11"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 29d302f7f04d2d4058d73d9a24b61bbc0235f440
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="server-properties-security-page---reporting-services"></a>서버 속성(보안 페이지) - Reporting Services
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 에서 이 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 페이지를 사용하여 보고서 서버를 손상시킬 가능성이 있는 기능을 해제할 수 있습니다. 이러한 기능을 해제하면 일부 기능이 제한되지만 특정 위협을 완화하여 보고서 서버의 전체적인 보안을 향상시킬 수 있습니다.  
  
 이 페이지를 열려면
 1) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다.
 2) 보고서 서버 인스턴스에 연결합니다.
 3) 보고서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다. 
 4) **보안** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>옵션  
 **보고서 데이터 원본에 대한 Windows 통합 보안 사용**  
 보고서를 요청한 사용자의 Windows 보안 토큰을 사용하여 보고서 데이터 원본에 연결할 수 있는지 여부를 지정합니다.  
  
 이 기능을 해제하면 보고서 데이터 원본 속성 페이지의 Windows 통합 보안 기능을 사용할 수 없게 됩니다. 보고서 데이터 원본이 Windows 통합 보안으로 구성된 상태에서 이 기능을 해제하면 보고서 서버는 모든 데이터 원본 연결 속성을 즉시 업데이트하여 자격 증명을 확인하도록 합니다.  
  
 **임시 보고 사용**  
 사용자가 관심 있는 데이터를 클릭할 때 자동으로 새 보고서가 생성되는 보고서 작성기 보고서에서 사용자가 임시 쿼리를 수행할 수 있는지 여부를 지정합니다.  
  
 이 옵션 설정에 따라 보고서 서버의 **EnableLoadReportDefinition** 속성이 **True** 또는 **False**로 지정됩니다. 이 옵션의 선택을 취소하면 속성은 **False** 로 설정되며 보고서 서버는 데이터 탐색 중 작성된 클릭 광고 보고서를 생성하지 않습니다. **LoadReportDefinition** 메서드에 대한 모든 호출은 차단됩니다.  
  
 이 옵션을 끄면 악의적인 사용자가 **LoadReportDefinition** 요청으로 보고서 서버에 오버로드를 가하여 서비스 거부 공격을 실행할 수 있는 위협이 완화됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
