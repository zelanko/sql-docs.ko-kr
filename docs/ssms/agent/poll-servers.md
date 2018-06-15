---
title: 서버 폴링 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f2245f6f524c9087d3c8d6a9d2c9c22d18120a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33042100"
---
# <a name="poll-servers"></a>서버 폴링
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

다중 서버 관리가 구현될 때 대상 서버는 정기적으로 마스터 서버에 연결하여 실행된 작업에 대한 정보를 업로드하고 새 작업을 다운로드합니다. 마스터 서버에 연결하는 프로세스를 *서버 폴링* 이라고 하며 서버 폴링은 정기적인 *폴링 간격*마다 발생합니다.  
  
## <a name="polling-intervals"></a>폴링 간격  
폴링 간격(기본적으로 1분)은 대상 서버가 명령을 다운로드하고 작업 실행 결과를 업로드하기 위해 마스터 서버에 연결하는 시간 간격을 제어합니다.  
  
대상 서버가 마스터 서버를 폴링할 때는 **msdb** 데이터베이스의 **sysdownloadlist** 테이블에서 대상 서버에 할당된 작업을 읽습니다. 이 작업에서는 다중 서버 작업 및 대상 서버의 다양한 작업 항목을 제어합니다. 작업 삭제, 작업 삽입, 작업 시작, 대상 서버의 폴링 간격 업데이트 등이 이러한 작업의 예입니다.  
  
작업은 다음 방법 중 하나로 **sysdownloadlist** 테이블에 게시됩니다.  
  
-   명시적으로 **sp_post_msx_operation** 저장 프로시저를 사용하는 방법  
  
-   암시적으로 다른 작업 저장 프로시저를 사용하는 방법  
  
작업 저장 프로시저를 사용하여 다중 서버 작업 일정 또는 작업 단계를 수정하거나 SQL-DMO(SQL Distributed Management Objects)를 사용하여 다중 서버 작업을 제어하는 경우 다중 서버 작업의 단계 또는 일정을 수정한 후 다음 명령을 실행합니다.  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
이 명령을 실행하면 대상 서버가 현재 작업 정의와 동기화됩니다.  
  
다음 항목을 사용하는 경우 작업을 명시적으로 게시하지 않아도 됩니다.  
  
-   Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 를 사용하여 다중 서버 작업을 제어하는 경우  
  
-   작업 저장 프로시저를 사용하여 작업 일정이나 작업 단계를 수정하지 않을 경우  
  
**대상 서버가 마스터 서버를 폴링하도록 설정하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>참고 항목  
[이벤트 관리](../../ssms/agent/manage-events.md)  
  
