---
description: sys.dm_repl_schemas(Transact-SQL)
title: sys. dm_repl_schemas (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_repl_schemas_TSQL
- dm_repl_schemas
- sys.dm_repl_schemas_TSQL
- sys.dm_repl_schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_schemas dynamic management function
ms.assetid: 6f5fefff-8492-4360-bd5b-a97287367914
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4e6a790db9fc4b072eb474157c1f25c46bca4e7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481860"
---
# <a name="sysdm_repl_schemas-transact-sql"></a>sys.dm_repl_schemas(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  복제로 게시된 테이블 열에 대한 정보를 반환합니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artcache_schema_address**|**varbinary(8)**|게시된 테이블 아티클에 대한 캐시된 스키마 구조의 메모리 내 주소입니다.|  
|**tabid**|**bigint**|복제된 테이블 ID입니다.|  
|**indexid**|**smallint**|게시된 테이블의 클러스터형 인덱스 ID입니다.|  
|**idSch**|**bigint**|테이블 스키마의 ID입니다.|  
|**tabschema**|**nvarchar (510)**|테이블 스키마의 이름입니다.|  
|**ccTabschema**|**smallint**|테이블 스키마의 문자 길이입니다.|  
|**tabname**|**nvarchar (510)**|게시된 테이블의 이름입니다.|  
|**ccTabname**|**smallint**|게시된 테이블 이름의 문자 길이입니다.|  
|**rowsetid_delete**|**bigint**|삭제된 행의 ID입니다.|  
|**rowsetid_insert**|**bigint**|삽입된 행의 ID입니다.|  
|**num_pk_cols**|**int**|기본 키 열의 수입니다.|  
|**pcitee**|**binary (8000)**|계산 열 평가에 사용되는 쿼리 식 구조에 대한 포인터입니다.|  
|**re_numtextcols**|**int**|복제된 테이블에 있는 BLOB(Binary Large Object) 열의 수입니다.|  
|**re_schema_lsn_begin**|**binary (8000)**|스키마 버전 로깅의 시작 LSN(로그 시퀀스 번호)입니다.|  
|**re_schema_lsn_end**|**binary (8000)**|스키마 버전 로깅의 끝 LSN입니다.|  
|**re_numcols**|**int**|게시된 열의 수입니다.|  
|**re_colid**|**int**|게시자에 있는 열 ID입니다.|  
|**re_awcName**|**nvarchar (510)**|게시된 열의 이름입니다.|  
|**re_ccName**|**smallint**|열 이름의 문자 수입니다.|  
|**re_pk**|**tinyint**|게시된 열이 기본 키의 일부인지 여부를 나타냅니다.|  
|**re_unique**|**tinyint**|게시된 열이 고유 인덱스인지 여부를 나타냅니다.|  
|**re_maxlen**|**smallint**|게시된 열의 최대 길이입니다.|  
|**re_prec**|**tinyint**|게시된 열의 전체 자릿수입니다.|  
|**re_scale**|**tinyint**|게시된 열의 소수 자릿수입니다.|  
|**re_collatid**|**bigint**|게시된 열의 데이터 정렬 ID입니다.|  
|**re_xvtype**|**smallint**|게시된 열의 형식입니다.|  
|**re_offset**|**smallint**|게시된 열의 오프셋입니다.|  
|**re_bitpos**|**tinyint**|바이트 벡터에서 게시된 열의 비트 위치입니다.|  
|**re_fNullable**|**tinyint**|게시된 열에 NULL 값을 사용할 수 있는지 여부를 지정합니다.|  
|**re_fAnsiTrim**|**tinyint**|게시된 열에 ANSI 지우기가 사용되는지 여부를 지정합니다.|  
|**re_computed**|**smallint**|게시된 열이 계산 열인지 여부를 지정합니다.|  
|**se_rowsetid**|**bigint**|행 집합의 ID입니다.|  
|**se_schema_lsn_begin**|**binary (8000)**|스키마 버전 로깅의 시작 LSN입니다.|  
|**se_schema_lsn_end**|**binary (8000)**|스키마 버전 로깅의 끝 LSN입니다.|  
|**se_numcols**|**int**|열의 수입니다.|  
|**se_colid**|**int**|구독자에 있는 열 ID입니다.|  
|**se_maxlen**|**smallint**|열의 최대 길이입니다.|  
|**se_prec**|**tinyint**|열의 전체 자릿수입니다.|  
|**se_scale**|**tinyint**|값의 소수 자릿수입니다.|  
|**se_collatid**|**bigint**|열의 데이터 정렬 ID입니다.|  
|**se_xvtype**|**smallint**|열의 형식입니다.|  
|**se_offset**|**smallint**|열의 오프셋입니다.|  
|**se_bitpos**|**tinyint**|바이트 벡터에서 열의 비트 위치입니다.|  
|**se_fNullable**|**tinyint**|열에 NULL 값을 사용할 수 있는지 여부를 지정합니다.|  
|**se_fAnsiTrim**|**tinyint**|열에 ANSI 지우기가 사용되는지 여부를 지정합니다.|  
|**se_computed**|**smallint**|열이 계산 열인지 여부를 지정합니다.|  
|**se_nullBitInLeafRows**|**int**|열 값이 NULL인지 여부를 지정합니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Dm_repl_schemas**를 호출 하려면 게시 데이터베이스에 대 한 VIEW DATABASE STATE 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 현재 복제 아티클 캐시에 로드되어 있는 복제된 데이터베이스 개체에 대한 정보만 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [복제 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

