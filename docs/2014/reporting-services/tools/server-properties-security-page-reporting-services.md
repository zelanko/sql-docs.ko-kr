---
title: 서버 속성(보안 페이지) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 95c237945cdb21921f04d16adc782ce0b60b533a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62635037"
---
# <a name="server-properties-security-page---reporting-services"></a>서버 속성(보안 페이지) - Reporting Services
  이 페이지를 사용하여 보고서 서버를 손상시킬 가능성이 있는 기능을 해제할 수 있습니다. 이러한 기능을 해제하면 일부 기능이 제한되지만 특정 위협을 완화하여 보고서 서버의 전체적인 보안을 향상시킬 수 있습니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작하고 보고서 서버 인스턴스에 연결한 다음 보고서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **보안** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>변수  
 **보고서 데이터 원본에 대한 Windows 통합 보안 사용**  
 보고서를 요청한 사용자의 Windows 보안 토큰을 사용하여 보고서 데이터 원본에 연결할 수 있는지 여부를 지정합니다.  
  
 이 기능을 해제하면 보고서 데이터 원본 속성 페이지의 Windows 통합 보안 기능을 사용할 수 없게 됩니다. 보고서 데이터 원본이 Windows 통합 보안으로 구성된 상태에서 이 기능을 해제하면 보고서 서버는 모든 데이터 원본 연결 속성을 즉시 업데이트하여 자격 증명을 확인하도록 합니다.  
  
 **임시 보고 사용**  
 사용자가 관심 있는 데이터를 클릭할 때 자동으로 새 보고서가 생성되는 보고서 작성기 보고서에서 사용자가 임시 쿼리를 수행할 수 있는지 여부를 지정합니다.  
  
 이 옵션 설정에 따라 보고서 서버의 `EnableLoadReportDefinition` 속성이 `True` 또는 `False`로 지정됩니다. 이 옵션의 선택을 취소하면 속성은 `False`로 설정되며 보고서 서버는 데이터 탐색 중 작성된 클릭 광고 보고서를 생성하지 않습니다. `LoadReportDefinition` 메서드에 대한 모든 호출은 차단됩니다.  
  
 이 옵션을 끄면 악의적인 사용자가 `LoadReportDefinition` 요청으로 보고서 서버에 오버로드를 가하여 서비스 거부 공격을 실행할 수 있는 위협이 완화됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](connect-to-a-report-server-in-management-studio.md)   
 [자격 증명 및 보고서 데이터 원본에 대 한 연결 정보 지정] (.. /report-data/specify-credential-and-connection-information-for-report-data-sources.md [Management Studio F1 도움말의 보고서 서버](report-server-in-management-studio-f1-help.md)  
  
  
