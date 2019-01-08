---
title: 시작 하려면 SQL Server의 인스턴스를 자동으로 설정 (SQL Server 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 300b539e132b9bda9bc6540c0aadcac6ab9f11a1
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640315"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>SQL Server 인스턴스를 자동으로 시작하도록 설정(SQL Server 구성 관리자)
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스가 자동으로 시작되도록 설정하는 방법에 대해 설명합니다. 설치 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 일반적으로 자동으로 시작되도록 구성됩니다. 이렇게 구성되지 않은 경우 언제든지 설정을 변경할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>SQL Server 인스턴스를 자동으로 시작하도록 설정하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 애플리케이션으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          열려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에는 **시작 페이지**, sqlservermanager12.msc (에 대 한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 12를 더 작은 수로 바꿉니다. SQLServerManager12.msc를 클릭 하면 Configuration Manager 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄을 고정 하려면 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **파일 위치 열기**합니다. Windows 파일 탐색기에서 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 화면에 고정** 하거나 **작업 표시줄에 고정**합니다.  
    > -   **Windows 8**:  
    >          열려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에서의 **검색** 참의 **앱**, 형식 **SQLServerManager\<버전 >.msc** 등`SQLServerManager12.msc`를 누릅니다 **Enter**합니다.  
  
2.  **SQL Server 구성 관리자**에서 **서비스**를 확장한 다음 **SQL Server**를 클릭합니다.  
  
3.  세부 정보 창에서 자동으로 시작할 인스턴스의 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **SQL Server \<***instancename***> 속성** 대화 상자에서 **시작 모드**를 **자동**으로 설정합니다.  
  
5.  **확인**을 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 인스턴스의 자동 시작 방지&#40;SQL Server 구성 관리자&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [다른 컴퓨터에 연결&#40;SQL Server 구성 관리자&#41;](scm-services-connect-to-another-computer.md)   
 [WMI를 구성하여 SQL Server 도구에 서버 상태 표시](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
