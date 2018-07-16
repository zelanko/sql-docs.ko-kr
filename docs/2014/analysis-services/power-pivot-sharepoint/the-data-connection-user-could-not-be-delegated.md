---
title: '데이터 연결은 Windows 인증을 사용하지만 사용자 자격 증명을 위임할 수 없습니다. 다음 연결을 새로 고치지 못했습니다: PowerPivot 데이터 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9cdc773ef42536be619d8d8c0edac1d6d1dcb92
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319383"
---
# <a name="the-data-connection-uses-windows-authentication-and-user-credentials-could-not-be-delegated-the-following-connections-failed-to-refresh-powerpivot-data"></a>데이터 연결은 Windows 인증을 사용하지만 사용자 자격 증명을 위임할 수 없습니다. PowerPivot 데이터 연결을 새로 고치지 못했습니다.
  Excel 서비스는 SharePoint의 PowerPivot 서버 인스턴스에 연결할 수 없는 경우 PowerPivot 데이터를 포함하는 Excel 통합 문서에 대해 이 오류를 반환합니다.  
  
## <a name="details"></a>설명  
  
|||  
|-|-|  
|적용 대상|SharePoint용 PowerPivot|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|PowerPoint 데이터 공급자 사용을 시도할 때 연결하지 못했습니다.|  
|메시지 텍스트|데이터 연결은 Windows 인증을 사용하지만 사용자 자격 증명을 위임할 수 없습니다. PowerPivot 데이터 연결을 새로 고치지 못했습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류 메시지는 여러 가지 원인으로 인해 표시됩니다. 이러한 모든 원인에 공통적으로 적용되는 요인은 Excel 서비스가 SharePoint의 클레임 토큰에서 유효한 Windows 사용자 ID를 가져올 수 없다는 것입니다. PowerPivot 데이터가 포함된 Excel 통합 문서의 경우 이 오류는 다음 조건 중 하나라도 해당하는 경우 발생합니다.  
  
-   Windows 토큰 서비스에 대한 클레임이 실행 중이지 않은 경우. SharePoint 로그 파일을 통해 이 오류의 원인을 확인할 수 있습니다. SharePoint 로그에 "파이프 끝점 'net.pipe://localhost/s4u/022694f3-9fbd-422b-b4b2-312e25dae2a2'을(를) 로컬 컴퓨터에서 찾을 수 없습니다." 메시지가 포함되어 있으면 Windows 토큰 서비스에 대한 클레임이 실행 중이지 않은 것입니다. 클레임을 시작하려면 중앙 관리를 통해 서비스 콘솔 응용 프로그램에서 서비스가 실행 중인지 확인합니다.  
  
-   도메인 컨트롤러로 사용자 ID의 유효성을 검사할 수 없는 경우. Windows 토큰 서비스에 대한 클레임은 캐시된 자격 증명을 사용하지 않으며, 각 연결에 대해 사용자 ID 유효성을 검사합니다. SharePoint 로그 파일을 통해 이 오류의 원인을 확인할 수 있습니다. SharePoint 로그에 "IClaimsIdentity에서 WindowsIdentity을(를) 가져오지 못했습니다." 메시지가 포함되어 있으면 사용자 ID를 인증할 수 없는 것입니다.  
  
-   컴퓨터가 같은 도메인 또는 양방향 신뢰 관계가 있는 도메인의 멤버여야 하는 경우  
  
-   Windows 도메인 사용자 계정을 사용해야 하는 경우. 계정의 이름은 UPN(Universal Principal Name)이어야 합니다.  
  
-   Excel 서비스의 서비스 계정에 개체 쿼리를 위한 Active Directory 사용 권한이 있어야 하는 경우  
  
## <a name="user-action"></a>사용자 동작  
 다음 지침에 따라 Windows 토큰 서비스에 대한 클레임 상태를 확인합니다.  
  
 다른 모든 시나리오의 경우에는 네트워크 관리자에게 문의하십시오.  
  
#### <a name="enable-claims-to-windows-token-service"></a>Windows 토큰 서비스에 대한 클레임 설정  
  
1.  중앙 관리의 시스템 설정에서 **서버의 서비스 관리**를 클릭합니다.  
  
2.  **Windows 토큰 서비스에 대한 클레임**을 선택하고 **시작**을 클릭합니다.  
  
3.  서비스가 서비스 콘솔에서도 실행되고 있는지 확인합니다.  
  
    1.  관리 도구에서 서비스를 클릭합니다.  
  
    2.  Windows 토큰 서비스에 대한 클레임이 실행 중이지 않으면 시작합니다.  
  
## <a name="see-also"></a>관련 항목  
 [PowerPivot 서비스 계정 구성](configure-power-pivot-service-accounts.md)  
  
  
