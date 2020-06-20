---
title: SQL Server (SQL Server 구성 관리자)에서 사용 하는 계정의 암호 변경 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1454e29835c0087fb75c93a1680f452dfe0f2c05
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935088"
---
# <a name="change-the-password-of-the-accounts-used-by-sql-server-sql-server-configuration-manager"></a>SQL Server에서 사용하는 계정의 암호 변경(SQL Server 구성 관리자)
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에이전트에 사용되는 계정의 암호를 변경하는 방법에 대해 설명합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 설치 중에 처음 제공된 자격 증명을 사용하여 컴퓨터에서 서비스로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 도메인 계정으로 실행되고 있으며 해당 계정의 암호가 변경된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용하는 암호를 새 암호로 업데이트해야 합니다. 암호를 업데이트하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 일부 도메인 리소스에 액세스하지 못할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 중지되면 암호를 업데이트할 때까지 서비스가 다시 시작되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 암호를 변경하려면 [암호 만료](../password-expired.md)를 참조하세요.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 설정을 변경하도록 디자인 되고 권한이 부여된 도구입니다. Windows 서비스 제어 관리자( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services.msc **) 애플리케이션을 사용하여**서비스를 변경하면 일부 필수 설정은 변경되지 않으며 서비스가 제대로 작동하지 않을 수 있습니다. 그러나 클러스터형 환경에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 액티브 노드의 암호를 변경한 후에는 서비스 제어 관리자를 사용하여 패시브 노드의 암호를 변경해야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 서비스에 사용되는 암호를 변경하려면 컴퓨터의 관리자여야 합니다.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>SQL Server(데이터베이스 엔진) 서비스에 사용되는 암호를 변경하려면  
  
1.  **시작** 단추를 클릭하고 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 애플리케이션으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          Configuration Manager를 열려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **시작 페이지**에서 sqlservermanager12.msc (의 경우)를 입력 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 12를 더 작은 수로 바꿉니다. SQLServerManager12.msc를 클릭하면 구성 관리자가 열립니다. Configuration Manager를 시작 페이지나 작업 표시줄에 고정 하려면 Sqlservermanager12.msc를 마우스 오른쪽 단추로 클릭 한 다음 **파일 위치 열기**를 클릭 합니다. Windows 파일 탐색기에서 Sqlservermanager12.msc를 마우스 오른쪽 단추로 클릭 한 다음 **시작 화면에 고정** 또는 **작업 표시줄에 고정**을 클릭 합니다.  
    > -   **Windows 8**:  
    >          Configuration Manager를 열려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **검색** 참의 **앱**아래에 **SQLServerManager \<version> ** 를 입력 한 `SQLServerManager12.msc` 다음 **enter**키를 누릅니다.  
  
2.  SQL Server 구성 관리자에서 **SQL Server 서비스**를 클릭합니다.  
  
3.  세부 정보 창에서 **SQL Server (**)를 마우스 오른쪽 단추로 클릭 한 \<instancename> **)** 다음 **속성**을 클릭 합니다.  
  
4.  **SQL Server (** \<instancename> **) 속성** 대화 상자의 로그온 탭에서 **계정 이름** 상자에 나열 된 계정에 대해 **암호** 및 **암호 확인** 상자에 새 암호를 입력 한 다음 **확인**을 클릭 합니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하지 않아도 암호가 즉시 적용됩니다.  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>SQL Server 에이전트 서비스에 사용되는 암호를 변경하려면  
  
1.  **시작** 단추를 클릭하고 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  SQL Server 구성 관리자에서 **SQL Server 서비스**를 클릭합니다.  
  
3.  세부 정보 창에서 **SQL Server 에이전트 (**)를 마우스 오른쪽 단추로 클릭 한 \<instancename> **)** 다음 **속성**을 클릭 합니다.  
  
4.  **SQL Server 에이전트 (** \<instancename> **) 속성** 대화 상자의 로그온 탭에서 **계정 이름** 상자에 나열 된 계정에 대해 **암호** 및 **암호 확인** 상자에 새 암호를 입력 한 다음 **확인**을 클릭 합니다.  
  
     독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하지 않아도 암호가 즉시 적용됩니다. 클러스터형 인스턴스에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스를 오프라인 상태로 만들 수 있으므로 다시 시작해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서비스 관리 방법 도움말 항목&#40;SQL Server 구성 관리자&#41;](../managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
  
