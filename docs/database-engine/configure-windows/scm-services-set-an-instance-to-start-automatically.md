---
title: SCM 서비스 - 인스턴스 자동 시작 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6850d5b607cd8645ac056ad8c18a2ec6ce07f28e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>SCM 서비스 - 인스턴스 자동 시작 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스가 자동으로 시작되도록 설정하는 방법에 대해 설명합니다. 설치 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 일반적으로 자동으로 시작되도록 구성됩니다. 이렇게 구성되지 않은 경우 언제든지 설정을 변경할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>SQL Server 인스턴스를 자동으로 시작하도록 설정하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 응용 프로그램으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **시작 페이지**에 SQLServerManager13.msc를 입력합니다( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 13을 더 작은 수로 바꿉니다. SQLServerManager13.msc를 클릭하면 구성 관리자가 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄에 고정하려면 SQLServerManager13.msc를 마우스 오른쪽 단추로 클릭한 다음 **파일 위치 열기**를 클릭합니다. Windows 파일 탐색기에서 SQLServerManager13.msc를 마우스 오른쪽 단추로 클릭하고 **시작 화면에 고정** 또는 **작업 표시줄에 고정**을 클릭합니다.  
    > -   **Windows 8**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **검색** 참의 **앱**에 **SQLServerManager\<version>.msc**(예: **SQLServerManager13.msc**)를 입력한 다음 **Enter** 키를 누릅니다.  
  
2.  **SQL Server 구성 관리자**에서 **서비스**를 확장한 다음 **SQL Server**를 클릭합니다.  
  
3.  세부 정보 창에서 자동으로 시작할 인스턴스의 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **SQL Server \<***instancename***> 속성** 대화 상자에서 **시작 모드**를 **자동**으로 설정합니다.  
  
5.  **확인**을 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 인스턴스의 자동 시작 방지&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [다른 컴퓨터에 연결&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [WMI를 구성하여 SQL Server 도구에 서버 상태 표시](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
  
