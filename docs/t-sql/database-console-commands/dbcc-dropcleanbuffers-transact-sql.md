---
description: DBCC DROPCLEANBUFFERS(Transact-SQL)
title: DBCC DROPCLEANBUFFERS(Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c820f664d6d8b56453c39f117d373f44312f898e
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076748"
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS(Transact-SQL)

[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

버퍼 풀에서 빈 버퍼를 제거하고 columnstore 개체 풀에서 columnstore 개체를 모두 제거합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문:

```syntaxsql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 구문:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다. 정보 메시지는 항상 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 무시됩니다.  
  
 COMPUTE  
 각 컴퓨팅 노드에서 메모리 내 데이터 캐시를 제거합니다.  
  
 ALL  
 각 컴퓨팅 노드 및 제어 노드에서 메모리 내 데이터 캐시를 제거합니다. 값을 지정하지 않으면 이것이 기본값입니다.  
  
## <a name="remarks"></a>설명  
DBCC DROPCLEANBUFFERS를 사용하면 서버를 종료하고 다시 시작하지 않아도 완전히 빈 버퍼 캐시를 사용하여 쿼리를 테스트할 수 있습니다.
버퍼 풀에서 빈 버퍼를 삭제하고 columnstore 개체 풀에서 columnstore 개체를 삭제하려면 먼저 CHECKPOINT를 사용해 콜드 버퍼 캐시를 생성합니다. 이 과정은 현재 데이터베이스에 대한 모든 커밋되지 않은 페이지를 디스크로 기록하고 버퍼를 비웁니다. 버퍼를 비운 후에 DBCC DROPCLEANBUFFERS 명령을 실행해 버퍼 풀에서 모든 버퍼를 제거할 수 있습니다.
  
## <a name="result-sets"></a>결과 집합  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 DBCC DROPCLEANBUFFERS는 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 `sysadmin` 고정 서버 역할의 멤버 자격이 필요합니다.  
[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에 대한 `DB_OWNER` 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
