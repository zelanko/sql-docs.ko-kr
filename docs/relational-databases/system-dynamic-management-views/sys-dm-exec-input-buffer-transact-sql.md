---
description: sys. dm_exec_input_buffer (Transact-sql)
title: sys. dm_exec_input_buffer (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4fecdc698dc7015ab47e5a8c97b3990c7e5bf1f4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536957"
---
# <a name="sysdm_exec_input_buffer-transact-sql"></a>sys. dm_exec_input_buffer (Transact-sql)

[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

인스턴스에 전송 된 문에 대 한 정보를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.

## <a name="syntax"></a>구문

```
sys.dm_exec_input_buffer ( session_id , request_id )
```

## <a name="arguments"></a>인수

*session_id* 조회할 일괄 처리를 실행 하는 세션 ID입니다. *session_id* 은 **smallint**입니다. *session_id* 는 다음과 같은 동적 관리 개체에서 가져올 수 있습니다.

- [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
- [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)
- [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)

*request_id* [Dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)의 request_id입니다. *request_id* 은 **int**입니다.

## <a name="table-returned"></a>반환된 테이블

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|
|**event_type**|**nvarchar(256)**|지정 된 spid의 입력 버퍼에 있는 이벤트의 유형입니다.|
|**parameters**|**smallint**|문에 대해 제공 되는 모든 매개 변수입니다.|
|**event_info**|**nvarchar(max)**|지정 된 spid의 입력 버퍼에 있는 문의 텍스트입니다.|

## <a name="permissions"></a>사용 권한

에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자에 게 VIEW SERVER STATE 권한이 있는 경우 사용자는 인스턴스에서 실행 중인 모든 세션을 볼 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다. 그렇지 않으면 사용자에 게 현재 세션만 표시 됩니다.

> [!IMPORTANT]
> 뷰 서버 상태 권한 (예: 트리거, 저장 프로시저 또는 함수)이 없는 SQL Server에 대해이 DMV를 SQL Server Management Studio 외부에서 실행 하면 master 데이터베이스에 대 한 사용 권한 오류가 throw 됩니다.

에서 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 사용자가 데이터베이스 소유자 인 경우에서 실행 중인 모든 세션을 볼 수 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 있습니다. 그렇지 않으면 사용자에 게 현재 세션만 표시 됩니다.

> [!IMPORTANT]
> 트리거, 저장 프로시저 또는 함수와 같은 소유자 권한이 없는 Azure SQL Database에 대해이 DMV를 SQL Server Management Studio 외부에서 실행 하면 master 데이터베이스에 대 한 사용 권한 오류가 throw 됩니다.

## <a name="remarks"></a>설명

이 동적 관리 함수는 **CROSS APPLY**를 수행 하 여 dm_exec_sessions 또는 dm_exec_requests와 함께 사용할 수 있습니다.

## <a name="examples"></a>예제

### <a name="a-simple-example"></a>A. 간단한 예

다음 예에서는 세션 ID (SPID) 및 요청 ID를 함수에 전달 하는 방법을 보여 줍니다.

```sql
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```

### <a name="b-using-cross-apply-to-additional-information"></a>B. Cross apply를 사용 하 여 추가 정보

다음 예에서는 세션 ID가 50 보다 큰 세션의 입력 버퍼를 나열 합니다.

```sql
SELECT es.session_id, ib.event_info
FROM sys.dm_exec_sessions AS es
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib
WHERE es.session_id > 50;
GO
```

## <a name="see-also"></a>참고 항목

- [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
- [sys.dm_exec_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)
- [sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
- [DBCC INPUTBUFFER&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)
