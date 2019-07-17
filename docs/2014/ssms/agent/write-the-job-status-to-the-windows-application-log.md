---
title: Windows 애플리케이션 로그에 작업 상태 쓰기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 526e95490644b4fddae3e02e9ee73b57c00797c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211271"
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Windows 애플리케이션 로그에 작업 상태 쓰기
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 작업 상태를 Windows 응용 프로그램 이벤트 로그에 기록하도록 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성하는 방법에 대해 설명합니다.  
  
 작업 응답은 데이터베이스 관리자에게 작업 완료 시점과 작업 실행 간격을 알립니다. 일반적인 작업 응답은 다음과 같습니다.  
  
-   전자 메일, 전자 호출 또는 **net send** 메시지 등으로 운영자에게 알림 운영자가 추가 작업 동작을 실행해야 할 경우 이 작업 응답 중 하나를 사용. 예를 들어 백업 작업이 성공적으로 완료될 경우 운영자는 백업 테이프를 빼낸 다음 안전한 곳에 저장하도록 알림을 받아야 합니다.  
  
-   이벤트 메시지를 Windows 애플리케이션 로그에 씀 이 응답은 실패한 작업에만 사용할 수 있습니다.  
  
-   작업을 자동 삭제함 이 작업을 반환할 필요가 없을 경우에는 이 작업 응답을 사용합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **Windows 응용 프로그램 로그에 작업 상태를 쓰려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMS)  
  
     [SQL Server 관리 개체](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>Windows 애플리케이션 로그에 작업 상태를 쓰려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장하고 편집할 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **알림** 페이지를 선택합니다.  
  
4.  **Windows 응용 프로그램 이벤트 로그에 쓰기**를 선택하고 다음 중 하나를 선택합니다.  
  
    -   작업이 성공적으로 완료되었을 때 작업 상태를 기록하려면**작업 성공 시**를 클릭합니다.  
  
    -   작업이 성공적으로 완료되었을 때 작업 상태를 기록하려면**작업 실패 시**를 클릭합니다.  
  
    -   작업이 성공적으로 완료되었을 때 작업 상태를 기록하려면**작업 완료 시** 를 클릭합니다.  
  
##  <a name="SMO"></a> SQL Server 관리 개체를 사용 하 여  
 **Windows 응용 프로그램 로그에 작업 상태를 쓰려면**  
  
 Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 `EventLogLevel` 클래스의 `Job` 속성을 호출합니다.  
  
 다음 코드 예에서는 작업 실행이 끝날 때 운영 체제 이벤트 로그 항목을 생성하도록 작업을 설정합니다.  
  
 **PowerShell**  
  
```  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
  
  
