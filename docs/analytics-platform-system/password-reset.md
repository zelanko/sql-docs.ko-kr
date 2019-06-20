---
title: 암호 재설정-Analytics Platform System | Microsoft Docs
description: 암호 재설정 페이지를 사용 하면 분석 플랫폼 시스템에서 사용 하는 관리자 계정에 대 한 암호를 변경할 수 있습니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 63fbb097bf1ca926223ce7c0114c8da5d10cd969
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639942"
---
# <a name="password-reset---analytics-platform-system"></a>암호 재설정-Analytics Platform System
합니다 **암호 재설정** 페이지를 사용 하면 분석 플랫폼 시스템에서 사용 하는 관리자 계정에 대 한 암호를 변경할 수 있습니다.  
  
> [!WARNING]  
> 항상 사용 합니다 **Configuration Manager** 어플라이언스 도메인 관리자 암호를 업데이트 합니다. 다른 메서드는 Analytics Platform System의 모든 구성 요소를 업데이트할 수 있습니다 및 어플라이언스 액세스 문제가 발생할 수 있습니다.  
  
Analytics Platform System 암호 어플라이언스 전달 될 때 제공 됩니다. 항상 어플라이언스에 대 한 책임을 가져올 때 새 값으로 암호를 변경 합니다. 세 가지 암호 업데이트 있습니다. 암호는 서로 같이 필요가 없습니다.  
  
**F<*xxxx*>\Administrator**  
합니다 **관리자** 어플라이언스 도메인입니다.  
  
**.\Administrator**  
로컬 **관리자** 가상 컴퓨터를 호스트 하는 컴퓨터 계정입니다.  
  
> [!IMPORTANT]  
> 어플라이언스에 대 한 업데이트 1 **Configuration Manager** 에 제대로 변경 PDW VM의 전체 로컬 관리자 계정의 암호입니다. 필요한 경우 추가 지침은 CSS에 문의 합니다.  
  
**sa**  
합니다 **sa** SQL Server에 로그인 합니다. **sa** 의 멤버인 합니다 **sysadmin** 고정 서버 역할 및 SQL Server 관리자입니다. 암호를 **sa** 사용 하 여 로그인을 변경할 수도 있습니다는 **ALTER LOGIN** 문입니다.  
  
## <a name="password-requirements"></a>암호 요구 사항  
도메인 관리자 자격 증명 및 시스템 관리자 자격 증명을 자격 증명의 각 형식에 대 한 암호 보안 수준 정책을 준수합니다. 도메인에 새 암호를 업데이트는 도메인 관리자 자격 증명을 변경 하는 경우 전체 SQL Server PDW에서 필요한 경우.  
  
> [!IMPORTANT]  
> SQL Server PDW 달러 기호 문자를 지원 하지 않습니다 ( **$** ) 도메인 관리자 또는 로컬 관리자 암호입니다. 하지만 문자 **^ % &** PowerShell 이러한 특수 문자를 인식 암호에 허용 됩니다. 시스템 관리자 또는 SQL Server 암호에 사용 되는 이러한 문자가**sa** 계정 (합니다 **AdminPassword** 및 **PdwSAPassword** 중 매개 변수 설치 프로그램)을 설정 하 고 설치, 업그레이드, REPLACENODE, 및 패치를 포함 하 여 실패 합니다. 현재 암호는 지원 되지 않는 문자를 포함 하는 경우 성공적인 업그레이드를 위해 업그레이드를 실행 하기 전에 이러한 문자가 포함 되지 않도록 이러한 암호를 변경 합니다. 업그레이드가 완료 된 후에 원래 값으로 다시이 암호를 설정할 수 있습니다. 암호 요구 사항에 대 한 자세한 내용은 참조 하세요. [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)합니다.  
  
## <a name="to-reset-a-password"></a>암호를 재설정 하려면  
  
1.  제어 노드 및 시작에 연결 합니다 **Configuration Manager** (**dwconfig.exe**). 자세한 내용은 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.  
  
2.  왼쪽된 창에는 **Configuration Manager**, 클릭 **암호 재설정**합니다.  
  
3.  관리자 유형을 선택 합니다 **계정** 드롭 다운 메뉴에서에서 새 암호를 입력 합니다 **암호** 및 **암호 확인** 상자. 클릭 **적용** 변경 내용을 저장 합니다.  
  
    이러한 계정에 변경한 모든 현재 활성 세션에 영향을 주지 않습니다 하지만 각 사용자에 대 한 다음 로그온 시 적용 됩니다.  
  
    ![SQL Server DWConfig 암호](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>관련 항목  
[디렉터리 서비스 복원 모드에서 AD 노드에 로그온에 대 한 관리자 암호 설정 &#40;DSRM&#41; &#40;분석 플랫폼 시스템&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Configuration Manager 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
