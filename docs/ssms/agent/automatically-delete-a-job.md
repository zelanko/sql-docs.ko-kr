---
description: Automatically Delete a Job
title: Automatically Delete a Job
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 06/03/2020
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 7da6affa2c92686c681566a929bb16dc688e9698
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466594"
---
# <a name="automatically-delete-a-job"></a>Automatically Delete a Job

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 작업이 성공, 실패 또는 완료될 때 해당 작업을 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성하는 방법에 대해 설명합니다.  
  
작업 응답은 데이터베이스 관리자에게 작업 완료 시점과 작업 실행 간격을 알립니다. 일반적인 작업 응답은 다음과 같습니다.  
  
-   전자 메일, 전자 호출 또는 **net send** 메시지 등으로 운영자에게 알림  
  
    운영자가 추가 작업 동작을 실행해야 할 경우 이 작업 응답 중 하나를 사용. 예를 들어 백업 작업이 성공적으로 완료될 경우 운영자는 백업 테이프를 빼낸 다음 안전한 곳에 저장하도록 알림을 받아야 합니다.  
  
-   이벤트 메시지를 Windows 애플리케이션 로그에 씀  
  
    이 응답은 실패한 작업에만 사용할 수 있습니다.  
  
-   작업을 자동 삭제함  
  
    이 작업을 반환할 필요가 없을 경우에는 이 작업 응답을 사용합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-automatically-delete-a-job"></a>자동으로 작업을 삭제하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업** 을 차례로 확장하고 편집할 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.  
  
3.  **알림** 페이지를 선택합니다.  
  
4.  **자동으로 작업 삭제** 를 선택하고 다음 중 하나를 선택합니다.  
  
    -   작업이 성공적으로 완료되었을 때 작업 상태를 삭제하려면 **작업 성공 시** 를 클릭합니다.  
  
    -   작업이 성공적으로 완료되지 않았을 때 작업을 삭제하려면 **작업 실패 시** 를 클릭합니다.  
  
    -   완료 상태에 관계없이 작업을 삭제하려면 **작업 완료 시** 를 클릭합니다.  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>SQL Server 관리 개체 사용  
**자동으로 작업을 삭제하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **Job** 클래스의 **DeleteLevel** 속성을 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)를 참조하세요.  
