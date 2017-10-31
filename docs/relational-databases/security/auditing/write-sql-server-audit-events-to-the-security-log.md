---
title: "보안 로그에 SQL Server Audit 이벤트 쓰기 | Microsoft 문서"
ms.custom: 
ms.date: 09/21/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f684f0168e57c5cd727af6488b2460eeaead100c
ms.openlocfilehash: 990b47afdf34cc16f15a658f5a69f840d44a27fe
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---  

# <a name="write-sql-server-audit-events-to-the-security-log"></a>보안 로그에 SQL Server Audit 이벤트 쓰기  
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]  

보안 수준이 높은 환경에서는 Windows 보안 로그에 개체 액세스를 기록하는 이벤트를 쓰는 것이 좋습니다. 다른 감사 위치도 지원되지만 변조될 가능성이 높습니다.  
  
 Windows 보안 로그에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버 감사를 쓰려면 두 가지 주요 요구 사항을 충족해야 합니다.  
  
-   감사 개체 액세스 설정이 이벤트를 캡처하도록 구성되어야 합니다. 이 감사 정책 도구(`auditpol.exe`)는 **감사 개체 액세스** 범주의 여러 하위 정책 설정을 제공합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 개체 액세스를 감사하도록 허용하려면 **응용 프로그램에서 생성된** 설정을 구성합니다.  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 실행 중인 계정이 Windows 보안 로그에 쓰려면 **보안 감사 생성** 권한이 있어야 합니다. 기본적으로 LOCAL SERVICE 및 NETWORK SERVICE 계정에는 이 권한이 포함됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 이러한 계정 중 하나로 실행 중인 경우에는 이 단계가 필요하지 않습니다.  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정에 대한 모든 권한을 레지스트리 하이브 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Security`에 제공합니다.  

  > [!IMPORTANT]  
  > [!INCLUDE[ssnoteregistry-md](../../../includes/ssnoteregistry-md.md)]   
  
Windows 감사 정책은 Windows 보안 로그에 기록하도록 구성된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 감사에 영향을 줄 수 있으며 감사 정책이 잘못 구성된 경우 이벤트가 손실될 가능성이 있습니다. 일반적으로 Windows 보안 로그는 이전 이벤트를 덮어쓰도록 설정됩니다. 이렇게 하면 가장 최신 이벤트를 유지할 수 있습니다. 하지만 Windows 보안 로그가 이전 이벤트를 덮어쓰도록 설정되지 않으면 보안 로그가 꽉 찰 경우 시스템에서 Windows 이벤트 1104(로그가 꽉 참)가 발생합니다. 그러면 다음과 같이 됩니다.  
-   보안 이벤트가 더 이상 기록되지 않습니다.  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 시스템이 보안 로그에 이벤트를 기록할 수 없다는 것을 감지하지 못하고 따라서 감사 이벤트가 손실될 수 있습니다.  
-   시스템 관리자가 보안 로그를 수정하면 로깅 동작이 정상으로 돌아옵니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터 관리자는 도메인 정책이 보안 로그에 대한 로컬 설정을 덮어쓸 수 있다는 점을 유의해야 합니다. 이 경우에 도메인 정책은 하위 범주 설정을 덮어쓸 수 있습니다(**auditpol /get /subcategory:"application generated"**). 이는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 감사하려는 이벤트가 기록되지 않는다는 점을 감지할 필요 없이 이벤트를 로깅할 수 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 기능에 영향을 미칠 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 이러한 설정을 구성하려면 Windows 관리자여야 합니다.  
  
##  <a name="auditpolAccess"></a> Windows에서 auditpol을 사용하여 감사 개체 액세스 설정을 구성하려면  
  
1.  관리자 권한으로 명령 프롬프트를 엽니다.  
  
    1.  **시작** 메뉴에서 **모든 프로그램**, **보조프로그램**을 차례로 가리키고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
    2.  **사용자 계정 컨트롤** 대화 상자가 열리면 **계속**을 클릭합니다.  
  
2.  다음 문을 실행하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 감사를 사용하도록 설정합니다.  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  명령 프롬프트 창을 닫습니다.  
  
##  <a name="secpolAccess"></a> secpol을 사용하여 계정에 보안 감사 생성 권한을 부여하려면  
  
1.  Windows 운영 체제의 **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  **secpol.msc** 를 입력한 다음 **확인**을 클릭합니다. **사용자 액세스 제어** 대화 상자가 열리면 **계속**을 클릭합니다.  
  
3.  로컬 보안 정책 도구에서 **보안 설정**, **로컬 정책**을 차례로 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
4.  결과 창에서 **보안 감사 생성**을 두 번 클릭합니다.  
  
5.  **로컬 보안 설정** 탭에서 **사용자 또는 그룹 추가**를 클릭합니다.  
  
6.  **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 **domain1\user1** 과 같은 사용자 계정의 이름을 입력한 다음 **확인**을 클릭하거나 **고급** 을 클릭하여 계정을 검색합니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  보안 정책 도구를 닫습니다.  
  
9. 이 설정을 사용하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 다시 시작합니다.  
  
##  <a name="secpolPermission"></a> Windows에서 secpol을 사용하여 감사 개체 액세스 설정을 구성하려면  
  
1.  운영 체제가 [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] 또는 Windows Server 2008 이전 버전인 경우 **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  **secpol.msc** 를 입력한 다음 **확인**을 클릭합니다. **사용자 액세스 제어** 대화 상자가 열리면 **계속**을 클릭합니다.  
  
3.  로컬 보안 정책 도구에서 **보안 설정**, **로컬 정책**을 차례로 확장한 다음 **감사 정책**을 클릭합니다.  
  
4.  결과 창에서 **개체 액세스 감사**를 두 번 클릭합니다.  
  
5.  **로컬 보안 설정** 탭의 **다음 시도 감사** 영역에서 **성공** 및 **실패**를 모두 선택합니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  보안 정책 도구를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  

