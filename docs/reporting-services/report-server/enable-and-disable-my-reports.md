---
title: 내 보고서 사용 및 사용 안 함 설정 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6670d1da918ac1bdc6cb1947b265f9d543259814
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577775"
---
# <a name="enable-and-disable-my-reports"></a>내 보고서 설정 및 해제
  내 보고서 기능은 보고서 서버 데이터베이스에 프라이빗 스토리지를 할당하여 해당 사용자가 소유한 보고서를 프라이빗 폴더에 저장할 수 있도록 합니다. 보고서 서버 관리자는 이 기능을 설정 또는 해제하거나 이 작업 영역으로 수행할 수 있는 작업을 제어하는 보안 설정을 수정하여 이 기능의 작동 방식을 변경할 수 있습니다.  
  
 기본적으로 내 보고서 기능은 해제되어 있습니다. 모든 사용자에 대해 이 기능을 설정 또는 해제할 수 있지만 특정 사용자 그룹만 이 기능을 사용하도록 설정할 수는 없습니다. 대부분의 사용자와 조직에서는 이 기능을 유용하게 사용할 수 있습니다. 이 도움말 항목에 설명되어 있는 장단점을 잘 살펴보고 이 기능이 해당 조직에 적합한지를 판단해 보십시오.  
  
## <a name="how-to-enable-and-disable-my-reports"></a>내 보고서를 설정 또는 해제하는 방법  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 내 보고서를 설정하려면 보고서 서버 인스턴스에 연결하고 **서버 속성** 페이지를 엽니다. 그런 다음 **일반** 탭에서 **각 사용자에 대해 내 보고서 폴더 설정** 옵션을 선택합니다.  
  
 내 보고서에 사용되는 역할 정의에 따라 내 보고서 작업 영역에서 지원되는 동작이 결정됩니다. 예를 들어 내 보고서 역할에서 "링크된 보고서 만들기"가 제외된 경우에 사용자는 내 보고서 폴더에서 링크된 보고서를 만들 수 없습니다. 자세한 내용은 [내 보고서 보안 설정](../../reporting-services/security/secure-my-reports.md)을 참조하세요.  
  
 내 보고서를 비활성화하려면 **각 사용자에 대해 내 보고서 폴더 설정**의 선택을 취소하십시오. 내 보고서를 비활성화하면 사용자가 내 보고서 폴더에 대해 볼 수 있는 표시가 모두 제거됩니다. 실제 스토리지를 제공하는 폴더 즉, 사용자 폴더의 하위 폴더는 이 기능을 해제한 후 수동으로 삭제해야 합니다.  
  
### <a name="when-my-reports-is-activated"></a>내 보고서가 활성화된 경우  
 이 기능을 활성화하면 사용자는 루트 폴더인 홈 아래에 있는 내 보고서 폴더를 볼 수 있습니다. 보고서 서버 관리자는 내 보고서 폴더는 물론 각 사용자의 하위 폴더가 있는 "사용자 폴더" 폴더도 볼 수 있습니다.  
  
 이 기능이 활성화되어 있을 때는 사용자 폴더 및 그 하위 폴더를 삭제할 수 없습니다. 그리고 "내 보고서"라는 이름은 루트 노드(홈) 아래에 생성된 폴더에 대한 이름으로 예약됩니다.  
  
 내 보고서를 비활성화했다가 활성화하는 경우 "사용자 폴더" 폴더가 새로 생성됩니다(없는 경우). 사용자 폴더가 있으면 사용자가 해당 내 보고서 폴더에 로그온할 때 새 하위 폴더가 추가됩니다.  
  
### <a name="when-my-reports-is-deactivated"></a>내 보고서가 비활성화된 경우  
 이 기능이 비활성화되면 "내 보고서"라는 이름이 더 이상 예약되지 않습니다. 사용자는 홈 폴더 아래에 내 보고서라는 개인 폴더를 만들 수 있습니다. 또한 내 보고서를 사용자별 내 보고서 하위 폴더로 리디렉션하는 기능은 더 이상 수행되지 않습니다. 마지막으로 URL 주소에 사용자별 내 보고서 폴더를 포함하는 보고서 링크는 더 이상 사용할 수 없습니다.  
  
## <a name="choosing-to-use-my-reports"></a>내 보고서를 사용하도록 선택  
 전용 서버 리소스를 통해 사용자 작업 영역을 지원할지 여부에 따라 내 보고서 사용 여부가 결정됩니다. 내 보고서는 사용자가 작업에 필요한 정보 리소스를 제어할 수 있도록 하는 강력한 기능입니다. 특별한 용도로 만들어진 보고서 작업도 할 수 있습니다. 내 보고서를 사용하는 가장 중요한 이유 중 하나는 보고서를 작성하고 검토해야 하는 사용자를 단위별로 안전하게 관리할 수 있다는 것입니다. 이 기능이 없으면 각 상황에 따라 여러 사용자에 대한 폴더 및 보안 정책을 직접 만들어야 합니다. 따라서 사용자 및 사용자 요구의 변화에 따라 폴더 및 정책 수가 계속 늘어나 시간이 지날수록 관리하기 어려워집니다.  
  
 내 보고서를 활성화하는 경우 내 보고서 링크를 클릭하는 도메인 계정으로 모든 사용자를 위한 내 보고서 폴더가 생성됩니다. 사용자가 원하지 않더라도 내 보고서 폴더는 생성됩니다. 사용되고 있는 폴더를 확인할 체계적인 방식은 없습니다. 폴더에 포함된 내용이 있는지 확인하려면 폴더를 직접 살펴봐야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [내 보고서 보안 설정](../../reporting-services/security/secure-my-reports.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
