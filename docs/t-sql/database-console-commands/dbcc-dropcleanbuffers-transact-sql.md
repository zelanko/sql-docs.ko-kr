---
title: DBCC DROPCLEANBUFFERS(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 94830ffc100d0be451d34055a645e124a58325b7
ms.sourcegitcommit: 03021482208259e6c67599b47df23fbbe8f3a393
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2018
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

버퍼 풀에서 빈 버퍼를 제거하고 columnstore 개체 풀에서 columnstore 개체를 모두 제거합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문
SQL Server용 구문: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
SQL Data Warehouse 및 병렬 데이터 웨어하우스용 구문:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다. 정보 메시지는 항상 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 무시됩니다.  
  
 COMPUTE  
 각 계산 노드에서 메모리 내 데이터 캐시를 제거합니다.  
  
 ALL  
 각 계산 노드 및 제어 노드에서 메모리 내 데이터 캐시를 제거합니다. 값을 지정하지 않으면 이것이 기본값입니다.  
  
## <a name="remarks"></a>Remarks  
DBCC DROPCLEANBUFFERS를 사용하면 서버를 종료하고 다시 시작하지 않아도 완전히 빈 버퍼 캐시를 사용하여 쿼리를 테스트할 수 있습니다.
버퍼 풀에서 빈 버퍼를 삭제하고 columnstore 개체 풀에서 columnstore 개체를 삭제하려면 먼저 CHECKPOINT를 사용해 콜드 버퍼 캐시를 생성합니다. 이 과정은 현재 데이터베이스에 대한 모든 커밋되지 않은 페이지를 디스크로 기록하고 버퍼를 비웁니다. 버퍼를 비운 후에 DBCC DROPCLEANBUFFERS 명령을 실행해 버퍼 풀에서 모든 버퍼를 제거할 수 있습니다.
  
## <a name="result-sets"></a>결과 집합  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 DBCC DROPCLEANBUFFERS는 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  

적용 대상: SQL Server, 병렬 데이터 웨어하우스 

- **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  

적용 대상: Azure SQL Data Warehouse

- DB_OWNER 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
