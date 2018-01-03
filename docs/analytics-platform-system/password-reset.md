---
title: "암호 재설정 (분석 플랫폼 시스템)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0f808fc-e120-430b-b6c9-11f2b1c90bf3
caps.latest.revision: "26"
ms.openlocfilehash: 5b342aca4498816e59e0fafcb882c5c039fed501
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="password-reset"></a>암호 다시 설정
**암호 재설정** 페이지 분석 플랫폼 시스템에서 사용 하는 관리자 계정에 대 한 암호를 변경할 수 있습니다.  
  
> [!WARNING]  
> 항상 사용 하는 **Configuration Manager** 기기 도메인 관리자 암호를 업데이트 합니다. 다른 메서드 분석 플랫폼 시스템의 모든 구성 요소를 업데이트할 수 있습니다 및 어플라이언스에 액세스 문제를 일으킬 수 있습니다.  
  
분석 플랫폼 시스템 암호 어플라이언스에 배달 될 때 제공 됩니다. 항상 장치에 대 한 책임을 져야 때 암호를을 새 값으로 변경 합니다. 업데이트 하려면 세 개의 암호 있습니다. 암호는 서로와 동일할 필요가 없습니다.  
  
**F <*xxxx*> \Administrator**  
**관리자** 기기 도메인의 합니다.  
  
**. \Administrator**  
로컬 **관리자** 가상 컴퓨터를 호스팅하는 컴퓨터에는 계정입니다.  
  
> [!IMPORTANT]  
> 어플라이언스 업데이트 1, **Configuration Manager** 되지 않았습니다. 변경 않습니다 PDW VM의 전체에서 로컬 관리자 계정의 암호입니다. 필요한 경우 추가 지침에 대 한 CSS에 문의 합니다.  
  
**sa**  
**sa** SQL Server의 로그인 합니다. **sa** 의 구성원은 **sysadmin** 고정 서버 역할 및 SQL Server 관리자입니다. 암호는 **sa** 를 사용 하 여 로그인을 변경할 수도 있습니다는 **ALTER LOGIN** 문.  
  
## <a name="password-requirements"></a>암호 요구 사항  
도메인 관리자 자격 증명 및 시스템 관리자 자격 증명은 모두 자격 증명의 각 형식에 대 한 암호 강도 정책을 준수합니다. 도메인에 새 암호를 업데이트할 도메인 관리자 자격 증명을 변경할 경우 전체 SQL Server PDW에서 필요한 부분입니다.  
  
> [!IMPORTANT]  
> SQL Server PDW 달러 기호 문자를 지원 하지 않습니다 (**$**)에서 도메인 관리자 또는 로컬 관리자 암호입니다. 하지만 문자 **^ % &** 는 PowerShell이 방법으로 특수 문자를 인식 암호에 사용할 수 있습니다. 이러한 문자가 사용 되는 경우 암호에는 시스템 관리자 또는 SQL Server에 대 한**sa** 계정 (의 **AdminPassword** 및 **PdwSAPassword** 하는 동안 매개 변수 설치 프로그램) 한 다음 설치 프로그램을 설치, 업그레이드, REPLACENODE, 및 패치 적용을 포함 하 여 실패 합니다. 현재 암호는 지원 되지 않는 문자를 포함 하는 경우 업그레이드를 성공적으로 되도록 이러한 암호 변경 하 여 업그레이드를 실행 하기 전에 이러한 문자는 포함 하지 않습니다. 업그레이드가 완료 된 후에 원래 값으로 다시 이러한 암호를 설정할 수 있습니다. 암호 요구 사항에 대 한 자세한 내용은 참조 [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)합니다.  
  
## <a name="to-reset-a-password"></a>암호를 재설정 하려면  
  
1.  시작 및 제어 노드가에 연결 된 **Configuration Manager** (**dwconfig.exe**). 자세한 내용은 참조 [구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41; ](launch-the-configuration-manager.md).  
  
2.  왼쪽된 창에는 **Configuration Manager**, 클릭 **암호 재설정**합니다.  
  
3.  관리자 유형을 선택는 **계정** 드롭 다운 메뉴에서 다음에 새 암호를 입력 하 고는 **암호** 및 **암호 확인** 상자입니다. 클릭 **적용** 변경 내용을 저장 합니다.  
  
    이러한 계정을 변경 하면 모든 현재 활성 세션에 영향을 주지 않습니다 되지만 각 사용자에 대 한 다음 로그온 할 때 적용 됩니다.  
  
    ![SQL Server DWConfig 암호](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>관련 항목:  
[디렉터리 서비스에 노드가 AD에 로그인 하기 위해 관리자 암호 설정 복원 모드 &#40; DSRM &#41; &#40; 분석 플랫폼 시스템 &#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41;](launch-the-configuration-manager.md)  
  
