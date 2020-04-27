---
title: 대상 서버의 폴링 간격 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- interval for polling [SQL Server]
- target servers [SQL Server], polling interval
- polling interval [SQL Server]
ms.assetid: 4ffbbefa-77fb-442e-a77c-cb8c6cab9f3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1578bbefc9ae17baae56799d943e5ae6186628ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63033645"
---
# <a name="set-the-polling-interval-for-target-servers"></a>Set the Polling Interval for Target Servers
  이 항목에서는 에이전트가 마스터에서 대상 서버로 정보 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 새로 고치는 빈도를 설정 하는 방법에 대해 설명 합니다. 작업은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 수행하도록 지정된 일련의 동작입니다. 다중 서버 작업은 마스터 서버가 하나 이상의 대상 서버에서 실행하는 작업입니다.  
  
-   **시작하기 전에:**  [보안](#Security)  
  
-   **다음을 사용하여 대상 서버 폴링 간격 설정**  [SQL Server Management Studio](#SSMS), [Transact-SQL](#TSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
 각 대상 서버는 같은 작업의 한 인스턴스를 동시에 실행할 수 있습니다. 각 대상 서버는 주기적으로 마스터 서버를 폴링하여 해당 대상 서버에 새로 할당된 작업의 복사본을 다운로드한 다음 연결을 끊습니다. 대상 서버는 로컬에서 작업을 실행한 다음 마스터 서버에 다시 연결하여 작업 결과 상태를 업로드합니다.  
  
> [!NOTE]  
>  대상 서버에서 작업 상태 업로드를 시도할 때 마스터 서버가 액세스 가능하지 않은 경우 작업 상태는 마스터 서버가 액세스 가능해질 때까지 스풀링됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) 및 [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)을 참조하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> SQL Server Management Studio 사용  
 **대상 서버의 폴링 간격을 설정하려면**  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음, 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리**를 가리킨 다음 **대상 서버 관리**를 클릭합니다.  
  
3.  **대상 서버 상태** 탭에서 **명령 게시**를 클릭합니다.  
  
4.  **명령 유형** 목록에서 **폴링 간격 설정**을 선택합니다.  
  
5.  **폴링 간격** 상자에 대상 서버가 마스터 서버를 폴링하기 전에 경과해야 하는 시간(초)을 10부터 28,800까지 범위에서 입력합니다.  
  
6.  **받는 사람**에서 다음 중 하나를 수행합니다.  
  
    1.  모든 대상 서버가 같은 폴링 간격을 공유할 경우 **모든 대상 서버** 를 클릭합니다.  
  
    2.  모든 대상 서버가 같은 폴링 간격을 공유하지는 않는 경우 **대상 서버 지정** 을 클릭한 다음 이 폴링 간격을 사용할 대상 서버를 각각 선택합니다.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Transact-SQL 사용  
 **대상 서버의 폴링 간격을 설정하려면**  
  
1.  개체 탐색기에서 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  쿼리 창에서 [sp_post_msx_operation &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql) 시스템 저장 프로시저를 사용 하 여 대상 서버의 폴링 간격을 설정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [dbo. sysdownloadlist &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysdownloadlist-transact-sql)  
  
  
