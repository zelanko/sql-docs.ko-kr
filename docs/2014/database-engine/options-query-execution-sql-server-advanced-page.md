---
title: '옵션 (쿼리 실행: SQL Server: 고급 페이지) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5323054b77ed26a3ada816f44c1bf6764ded931d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089368"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>옵션(쿼리 실행:SQL Server:고급 페이지)
  SET 명령을 사용할 때 이용할 수 있는 몇 가지 옵션이 있습니다. 이 페이지를 사용하면 SQL Server 쿼리 편집기에서 **** 쿼리 실행에 대한 set[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 옵션을 지정할 수 있습니다. 설정한 옵션은 다른 코드 편집기에는 영향을 주지 않습니다. 이러한 옵션의 변경 사항은 새로운 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리에만 적용됩니다. 현재 쿼리에 대한 옵션을 변경하려면 **쿼리** 메뉴 또는 **쿼리 창의 바로 가기 메뉴에서** 쿼리 옵션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 을 클릭하고 
  **실행**에서 **고급**을 클릭합니다. 각 옵션에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **SET NOCOUNT**  
 행 개수를 결과 집합이 포함된 메시지로 반환하지 않습니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **NOEXEC 설정**  
 쿼리를 실행하지 않습니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **PARSEONLY 설정**  
 각 쿼리 구문을 검사하지만 쿼리를 실행하지는 않습니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **CONCAT_NULL_YIELDS_NULL 설정**  
 이 확인란을 선택하면 기존 값에 NULL을 연결하는 쿼리의 경우 결과로 항상 NULL을 반환합니다. 이 확인란의 선택을 취소하면 NULL과 연결된 기존 값이 기존 값을 반환합니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **ARITHABORT 설정**  
 이 확인란을 선택하면 식 평가 중 INSERT, DELETE 또는 UPDATE 문에서 산술 오류(오버플로, 0으로 나누기, 도메인 오류)가 발생할 경우 쿼리나 일괄 처리가 종료됩니다. 이 확인란의 선택을 취소하면 가능한 경우 해당 값에 대해 NULL이 제공되고 쿼리가 계속 실행되며 결과에 메시지가 포함됩니다. 자세한 내용은 [SET ARITHABORT&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)를 참조하세요. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **SHOWPLAN_TEXT 설정**  
 이 확인란을 선택하면 각 쿼리에 대한 쿼리 계획이 텍스트 형식으로 반환됩니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **통계 시간 설정**  
 이 확인란을 선택하면 각 쿼리의 시간 통계가 반환됩니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **통계 IO 설정**  
 이 확인란을 선택하면 각 쿼리의 입출력 통계가 반환됩니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 기본적으로 READ COMMITTED 트랜잭션 격리 수준이 설정됩니다. 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)을 참조하세요. SNAPSHOT 트랜잭션 격리 수준은 사용할 수 없습니다. SNAPSHOT 격리를 사용하려면 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 추가합니다.  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **SET DEADLOCK PRIORITY**  
 기본값인 Normal은 교착 상태가 발생할 경우 각 쿼리가 동일한 우선 순위를 가지도록 합니다. 해당 쿼리를 교착 상태를 해제하고 종료할 쿼리로 선택하려면 Low 우선 순위를 선택합니다.  
  
 **SET LOCK TIMEOUT**  
 기본값 -1은 트랜잭션이 완료될 때까지 잠금이 유지된다는 것을 나타냅니다. 0은 기다리지 않음을 나타내고 잠금이 있으면 바로 오류 메시지가 반환됩니다. 트랜잭션 잠금을 이 시간보다 오래 유지해야 하는 경우 0밀리초보다 큰 값을 지정하여 트랜잭션을 종료합니다.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 
  **QUERY_GOVERNOR_COST_LIMIT** 옵션을 사용하여 쿼리를 실행할 수 있는 시간의 상한값을 지정할 수 있습니다. 쿼리 비용이란 특정 하드웨어 구성에서 쿼리를 완료하는 데 필요한 예상 소요 시간(초)입니다. 기본 설정인 0은 쿼리 실행 시간에 제한이 없음을 나타냅니다.  
  
 **공급자 메시지 머리글 무시**  
 이 확인란을 선택하면 SQLClient 공급자와 같은 공급자의 상태 메시지가 표시되지 않습니다. 이 확인란은 기본적으로 선택되어 있습니다. 공급자 수준에서 오류가 발생할 수 있는 쿼리 문제를 해결할 때 공급자 메시지를 보려면 이 확인란의 선택을 취소합니다.  
  
 **쿼리 실행 후 연결 끊기**  
 이 확인란을 선택하면 쿼리 실행이 완료된 후 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결이 종료됩니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
