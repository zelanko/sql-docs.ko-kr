---
title: sys.fn_cdc_get_max_lsn (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn_TSQL
- sys.fn_cdc_get_max_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_max_lsn
- sys.fn_cdc_get_max_lsn
ms.assetid: 93f3a4c8-b91f-4ebb-8e96-9397bb3a1c43
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fae4f476005cb227b198b193712e4a564a1418fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789961"
---
# <a name="sysfncdcgetmaxlsn-transact-sql"></a>sys.fn_cdc_get_max_lsn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  최대 LSN (로그 시퀀스 번호)의 start_lsn 열에서 반환 된 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 시스템 테이블입니다. 이 함수를 사용하면 원하는 캡처 인스턴스에 대한 변경 데이터 캡처 시간대의 상위 엔드포인트를 반환할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_cdc_get_max_lsn ()  
```  
  
## <a name="return-types"></a>반환 형식  
 **binary(10)**  
  
## <a name="remarks"></a>Remarks  
 이 함수는의 start_lsn 열에서 최대 LSN을 반환 합니다 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 테이블입니다. 즉, 이 LSN은 변경 내용이 데이터베이스 변경 테이블로 전파될 때 캡처 프로세스에 의해 처리되는 마지막 LSN이며, 데이터베이스에 대해 정의된 캡처 인스턴스와 연결된 모든 시간대의 상위 엔드포인트 역할도 합니다.  
  
 일반적으로 이 함수는 쿼리 간격에 대한 적절한 상위 엔드포인트를 가져오는 데 사용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 public 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-maximum-lsn-value"></a>1. 최대 LSN 값 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 모든 캡처 인스턴스에 대한 최대 LSN을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT sys.fn_cdc_get_max_lsn()AS max_lsn;  
```  
  
### <a name="b-setting-the-high-endpoint-of-a-query-range"></a>2. 쿼리 범위의 상위 엔드포인트 설정  
 다음 예에서는 `sys.fn_cdc_get_max_lsn`에서 반환된 최대 LSN을 사용하여 `HumanResources_Employee` 캡처 인스턴스에 대한 쿼리 범위의 상위 엔드포인트를 설정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn(N'HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.fn_cdc_get_min_lsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
