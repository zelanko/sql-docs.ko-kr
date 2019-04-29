---
title: 쿼리 옵션 실행 (고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c598ca2dc2e1fd79e221c0c3d3fc1a5c3592dcb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844174"
---
# <a name="query-options-execution-advanced-page"></a>쿼리 옵션 실행(고급 페이지)
  **SET** 문을 사용하여 다양한 옵션을 사용할 수 있습니다. 이 페이지를 사용하여 Microsoft SQL Server 쿼리를 실행하기 위한 **set** 옵션을 지정할 수 있습니다. 이러한 각 옵션에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
 **SET NOCOUNT**  
 행 개수를 결과 집합이 포함된 메시지로 반환하지 않습니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **SET NOEXEC**  
 쿼리를 실행하지 않습니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **SET PARSEONLY**  
 각 쿼리 구문을 검사하지만 쿼리를 실행하지는 않습니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 이 확인란을 선택하면 기존 값을 `NULL`에 연결하는 쿼리의 결과로 항상 `NULL` 이 반환됩니다. 이 확인란의 선택을 취소하면 `NULL`에 연결된 기존 값이 기존 값을 반환합니다. 이 옵션은 기본적으로 선택되어 있습니다.  
  
 **SET ARITHABORT**  
 이 확인란을 선택하면 식을 평가하는 동안 `INSERT`, `DELETE` 또는 `UPDATE` 문에 산술 오류(오버플로, 0으로 나누기 또는 도메인 오류)가 발생하면 쿼리나 일괄 처리가 종료됩니다. 이 확인란의 선택을 취소하면 가능한 경우 해당 값으로 `NULL` 이 제공되고 쿼리가 계속된 다음 결과에 메시지가 포함됩니다. 이 동작에 대한 자세한 설명은 온라인 설명서를 참조하십시오. 이 옵션은 기본적으로 선택되어 있습니다.  
  
 **SET SHOWPLAN_TEXT**  
 이 확인란을 선택하면 각 쿼리의 쿼리 계획이 텍스트 형식으로 반환됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **SET STATISTICS TIME**  
 이 확인란을 선택하면 각 쿼리의 시간 통계가 반환됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **SET STATISTICS IO**  
 이 확인란을 선택하면 각 쿼리의 I/O(입/출력) 관련 통계가 반환됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 기본적으로 READ COMMITTED 트랜잭션 격리 수준이 설정됩니다. 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)을 참조하세요. SNAPSHOT 트랜잭션 격리 수준은 사용할 수 없습니다. SNAPSHOT 격리를 사용하려면 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 추가합니다.  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **교착 상태 우선 순위 설정**  
 기본값 **Normal** 로 설정하면 교착 상태가 발생할 때 각 쿼리의 우선 순위가 같아집니다. 이 쿼리를 교착 상태를 해제하고 종료할 쿼리로 선택하려면 드롭다운 목록에서 Low 우선 순위를 선택합니다.  
  
 **잠금 제한 시간 설정**  
 기본값 -1은 트랜잭션이 완료될 때까지 잠금이 유지된다는 것을 나타냅니다. 0은 기다리지 않음을 나타내고 잠금이 있으면 바로 오류 메시지가 반환됩니다. 트랜잭션 잠금을 이 시간보다 오래 유지해야 하는 경우 0밀리초보다 큰 값을 지정하여 트랜잭션을 종료합니다.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 **query governor cost limit** 옵션을 사용하여 쿼리 실행 제한 시간에 대한 상한값을 지정할 수 있습니다. 쿼리 비용이란 특정 하드웨어 구성에서 쿼리를 완료하는 데 필요한 예상 소요 시간(초)입니다. 기본값 0은 쿼리 실행 제한 시간이 없다는 것을 나타냅니다.  
  
 **공급자 메시지 헤더 표시 안 함**  
 이 확인란을 선택하면 OLE DB 공급자와 같은 공급자의 상태 메시지가 표시되지 않습니다. 이 확인란은 기본적으로 선택되어 있습니다. 공급자 수준에서 오류가 발생할 수 있는 쿼리 문제를 해결할 때 공급자 메시지를 보려면 이 확인란의 선택을 취소합니다.  
  
 **쿼리 실행 후 연결 끊기**  
 이 확인란을 선택하면 쿼리 완료 후 SQL Server에 대한 연결이 종료됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
