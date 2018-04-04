---
title: 작업 속성 - 새 작업(알림 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47bbd070ce658140270adb6bbfbd63e71c22fc6c
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="job-properties---new-job-notifications-page"></a>작업 속성 - 새 작업(알림 페이지)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 작업이 완료되었을 때 수행할 동작을 설정할 수 있습니다.  
  
## <a name="options"></a>변수  
**전자 메일**  
작업이 완료되었을 때 전자 메일을 보내려면 이 옵션을 선택합니다. 이 옵션을 선택한 후 알릴 운영자와 **작업 성공 시**, **작업 실패 시**, **작업 완료 시**등 알림을 트리거할 조건을 선택합니다.  
  
**호출**  
작업이 완료되었을 때 운영자의 호출기로 전자 메일을 보내려면 이 옵션을 선택합니다. 이 옵션을 선택한 후 알릴 운영자와 **작업 성공 시**, **작업 실패 시**, **작업 완료 시**등 알림을 트리거할 조건을 지정합니다.  
  
**Net Send**  
작업이 완료되었을 때 Net Send를 사용하여 운영자에게 알리려면 이 옵션을 선택합니다. 이 옵션을 선택한 후 알릴 운영자와 **작업 성공 시**, **작업 실패 시**, **작업 완료 시**등 알림을 트리거할 조건을 지정합니다.  
  
**Windows 응용 프로그램 이벤트 로그에 쓰기**  
작업이 완료되었을 때 응용 프로그램 이벤트 로그에 항목을 쓰려면 이 옵션을 선택합니다. 이 옵션을 선택한 후 **작업 성공 시**, **작업 실패 시**, **작업 완료 시**등 항목을 쓰도록 할 조건을 지정합니다.  
  
**자동으로 작업 삭제**  
작업이 완료되었을 때 작업을 삭제하려면 이 옵션을 선택합니다. 이 옵션을 선택한 후 **작업 성공 시**, **작업 실패 시**, **작업 완료 시**등 작업 삭제를 트리거할 조건을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
[작업 구현](../../ssms/agent/implement-jobs.md)  
[방법: 데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성(SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
