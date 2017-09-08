---
title: DBCC DROPCLEANBUFFERS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1a7a1507e230995df1c2b67a8499a12270b535c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Columnstore 개체 columnstore 개체 풀에서 버퍼 풀에서 빈 버퍼를 모두 제거합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문
SQL Server에 대 한 구문: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Azure SQL 웨어하우스 및 병렬 데이터 웨어하우스에 대 한 구문:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다. 정보 메시지는 항상에 억제 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
 COMPUTE  
 각 계산 노드가에서 쿼리 계획 캐시를 제거 합니다.  
  
 ALL  
 각 계산 노드 및 제어 노드가에서 쿼리 계획 캐시를 제거 합니다. 값을 지정 하지 않으면 기본값은입니다.  
  
## <a name="remarks"></a>주의  
DBCC DROPCLEANBUFFERS를 사용하면 서버를 종료하고 다시 시작하지 않아도 완전히 빈 버퍼 캐시를 사용하여 쿼리를 테스트할 수 있습니다.
Columnstore 개체 풀에서 버퍼 풀와 columnstore 개체에서 빈 버퍼를 삭제 하려면 먼저 빈 버퍼 캐시를 생성 하기 위해 검사점을 사용 합니다. 이 과정은 현재 데이터베이스에 대한 모든 커밋되지 않은 페이지를 디스크로 기록하고 버퍼를 비웁니다. 버퍼를 비운 후에 DBCC DROPCLEANBUFFERS 명령을 실행해 버퍼 풀에서 모든 버퍼를 제거할 수 있습니다.
  
## <a name="result-sets"></a>결과 집합  
DBCC DROPCLEANBUFFERS [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  

적용 대상: SQL Server, 병렬 데이터 웨어하우스 

- **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  

적용 대상: Azure SQL Data Warehouse

- DB_OWNER 고정된 서버 역할의 멤버 자격이 필요 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  

