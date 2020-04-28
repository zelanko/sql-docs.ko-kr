---
title: 암호 재설정
description: 암호 재설정 페이지에서 분석 플랫폼 시스템에 사용 되는 관리자 계정의 암호를 변경할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400901"
---
# <a name="password-reset---analytics-platform-system"></a>암호 재설정-분석 플랫폼 시스템
**암호 재설정** 페이지에서 분석 플랫폼 시스템에 사용 되는 관리자 계정의 암호를 변경할 수 있습니다.  
  
> [!WARNING]  
> 항상 **Configuration Manager** 를 사용 하 여 어플라이언스 도메인 관리자 암호를 업데이트 합니다. 다른 방법으로는 분석 플랫폼 시스템의 모든 구성 요소를 업데이트할 수 없으며 어플라이언스 액세스 문제가 발생할 수 있습니다.  
  
기기가 제공 될 때 분석 플랫폼 시스템 암호가 제공 됩니다. 어플라이언스를 담당 하는 경우 항상 암호를 새 값으로 변경 합니다. 3 개의 암호를 업데이트할 수 있습니다. 암호는 서로 같을 필요가 없습니다.  
  
**F<*xxxx*> \administrator**  
어플라이언스 도메인의 **관리자** 입니다.  
  
**.\Administrator**  
가상 컴퓨터를 호스트 하는 컴퓨터의 로컬 **관리자** 계정입니다.  
  
> [!IMPORTANT]  
> 어플라이언스 업데이트 1의 경우 **Configuration Manager** 는 PDW VM 전체에서 로컬 관리자 계정의 암호를 올바르게 변경 하지 않습니다. 필요한 경우 추가 지침은 CSS에 문의 하세요.  
  
**sa**  
SQL Server의 **sa** 로그인입니다. **sa** 는 **sysadmin** 고정 서버 역할의 멤버 이며 SQL Server 관리자입니다. **ALTER login** 문을 사용 하 여 **sa** 로그인의 암호를 변경할 수도 있습니다.  
  
## <a name="password-requirements"></a>암호 요구 사항  
도메인 관리자 자격 증명과 시스템 관리자 자격 증명은 각 자격 증명 형식에 대 한 암호 수준 정책을 준수 합니다. 도메인 관리자 자격 증명을 변경 하는 경우 새 암호는 SQL Server PDW 전체에 필요한 도메인으로 업데이트 됩니다.  
  
> [!IMPORTANT]  
> SQL Server PDW은 도메인 관리자 또는 로컬 관리자 암호에서**$** 달러 기호 문자 ()를 지원 하지 않습니다. 문자 **^% &** 은 (는) 암호로 허용 되지만 PowerShell에서 특수 문자로 간주 됩니다. 이러한 문자 중 하나를 시스템 관리자 또는 SQL Server**sa** 계정 (설치 하는 동안 **Adminpassword** 및 **pdwsapassword** 매개 변수)의 암호에 사용 하는 경우 설치, 업그레이드, REPLACENODE 및 패치 적용을 포함 한 설치는 실패 합니다. 현재 암호에 지원 되지 않는 문자가 포함 되어 있을 때 업그레이드를 성공적으로 수행 하려면 업그레이드를 실행 하기 전에 이러한 문자가 포함 되지 않도록 암호를 변경 합니다. 업그레이드가 완료 되 면 이러한 암호를 원래 값으로 다시 설정할 수 있습니다. 암호 요구 사항에 대 한 자세한 내용은 [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)을 참조 하세요.  
  
## <a name="to-reset-a-password"></a>암호를 다시 설정하려면  
  
1.  컨트롤 노드에 연결 하 고 **Configuration Manager** (**dwconfig .exe**)를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작 ](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  **Configuration Manager**의 왼쪽 창에서 **암호 재설정**을 클릭 합니다.  
  
3.  **계정** 드롭다운 메뉴에서 관리자 유형을 선택 하 고 **암호** 및 **암호 확인** 상자에 새 암호를 입력 합니다. 클릭 **적용** 변경 내용을 저장 합니다.  
  
    이러한 계정에 대 한 변경 내용은 현재 활성화 된 세션에는 영향을 주지 않지만 각 사용자에 대해 다음 번에 로그온 할 때 적용 됩니다.  
  
    ![SQL Server DWConfig 암호](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>참고 항목  
[디렉터리 서비스 복원 모드에서 AD 노드에 로그온 하기 위한 관리자 암호를 설정 &#40;DSRM&#41; &#40;분석 플랫폼 시스템&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Configuration Manager &#40;Analytics Platform System을 시작&#41;](launch-the-configuration-manager.md)  
  
