---
title: sys. dm_db_xtp_merge_requests (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f522fde05ce951575d3e02b3cdc4d3336056bd4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68026807"
---
# <a name="sysdm_db_xtp_merge_requests-transact-sql"></a>sys.dm_db_xtp_merge_requests(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

데이터베이스 병합 요청을 추적합니다. SQL Server에서 병합 요청을 생성 했거나 [sp_xtp_merge_checkpoint_files (transact-sql)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)를 사용 하는 사용자가 요청을 했을 수 있습니다.

> [!NOTE]
> 이 DMV (동적 관리 뷰), dm_db_xtp_merge_requests는 Microsoft SQL Server 2014까지 존재 합니다.
> 그러나 SQL Server 2016부터이 DMV는 더 이상 적용 되지 않습니다.

## <a name="columns-in-the-report"></a>보고서의 열

| 열 이름 | 데이터 형식 | Description |
| :-- | :-- | :-- |
| request_state | tinyint | 병합 요청의 상태입니다.<br/>0 = 요청됨<br/>1 = 보류 중<br/>2 = 설치 됨<br/>3 = 중단됨 |
| request_state_desc | nvarchar(60) | 요청의 현재 상태에 대 한 의미입니다.<br/><br/>요청 됨-병합 요청이 있습니다.<br/>보류 중-병합을 처리 하는 중입니다.<br/>설치 됨-병합이 완료 되었습니다.<br/>중단 됨-저장소 부족으로 인해 병합을 완료할 수 없습니다. |
| destination_file_id | GUID | 원본 파일 병합을 위한 대상 파일의 고유 식별자입니다. |
| lower_bound_tsn | bigint | 대상 병합 파일에 대한 최소 타임스탬프입니다. 병합할 모든 원본 파일의 최저 트랜잭션 타임스탬프입니다. |
| upper_bound_tsn | bigint | 대상 병합 파일에 대한 최대 타임스탬프입니다. 병합할 모든 원본 파일의 최고 트랜잭션 타임스탬프입니다. |
| collection_tsn | bigint | 현재 행을 수집할 수 있는 타임스탬프입니다.<br/><br/>checkpoint_tsn이 collection_tsn보다 크면 설치됨 상태의 행이 제거됩니다.<br/><br/>checkpoint_tsn이 collection_tsn보다 작으면 중단됨 상태의 행이 제거됩니다. |
| checkpoint_tsn | bigint | 검사점이 시작된 시간입니다.<br/><br/>이 값보다 작은 타임스탬프가 있는 트랜잭션에서 수행한 모든 삭제가 새로운 데이터 파일에서 반영됩니다. 나머지 삭제는 대상 델타 파일로 이동합니다. |
| sourcenumber_file_id | GUID | 병합에서 원본 파일을 고유 하 게 식별 하는 최대 16 개의 내부 파일 Id입니다. |

## <a name="permissions"></a>사용 권한

현재 데이터베이스에 대해 VIEW DATABASE STATE 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

[메모리 액세스에 최적화된 테이블 동적 관리 뷰(Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
