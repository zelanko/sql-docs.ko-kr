---
description: Force a Target Server to Poll the Master Server
title: Force a Target Server to Poll the Master Server
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 4aaac1b02996efdf950e4a0fecac054b25a9055c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474464"
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Force a Target Server to Poll the Master Server
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 강제로 대상 서버가 마스터 서버를 폴링하도록 하는 방법에 대해 설명합니다. 대상 서버는 마스터 서버에 등록된 서버여야 합니다.  
  
작업은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 수행하도록 지정된 일련의 동작입니다. 다중 서버 작업은 마스터 서버가 하나 이상의 대상 서버에서 실행하는 작업입니다. 각 대상 서버는 같은 작업의 한 인스턴스를 동시에 실행할 수 있습니다. 각 대상 서버는 주기적으로 마스터 서버를 폴링하여 해당 대상 서버에 새로 할당된 작업의 복사본을 다운로드한 다음 연결을 끊습니다. 대상 서버는 로컬에서 작업을 실행한 다음 마스터 서버에 다시 연결하여 작업 결과 상태를 업로드합니다.  
  
> [!NOTE]  
> 대상 서버에서 작업 상태 업로드를 시도할 때 마스터 서버가 액세스 가능하지 않은 경우 작업 상태는 마스터 서버가 액세스 가능해질 때까지 스풀링됩니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Restrictions), [보안](#Security)  
  
-   **대상 서버가 마스터 서버를 폴링하도록 설정하려면** [SQL Server Management Studio](#SSMS)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
대상 서버는 마스터 서버에 등록된 서버여야 합니다. 마스터 서버에서 이 항목에 제공된 지침을 실행해야 합니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) 및 [Choose the Right SQL Server Agent Service Account for Multiserver Environments](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
**대상 서버가 마스터 서버를 폴링하도록 설정하려면**  
  
1.  **개체 탐색기** 에서 마스터 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리** 를 가리킨 다음 **대상 서버 관리** 를 클릭합니다.  
  
3.  대상 서버를 클릭한 다음 **강제 폴링** 을 클릭합니다.  
