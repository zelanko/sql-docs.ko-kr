---
description: sys.sp_cdc_scan(Transact-SQL)
title: sys. sp_cdc_scan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0ad39bba5f8a3fbee5bcecde3e41ad9a7f7f4442
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463948"
---
# <a name="syssp_cdc_scan-transact-sql"></a>sys.sp_cdc_scan(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  변경 데이터 캡처 로그 검색 작업을 실행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>인수  
`[ @maxtrans = ] max_trans` 각 검색 주기에서 처리할 최대 트랜잭션 수입니다. *max_trans* 는 **int** 이며 기본값은 500입니다.  
  
`[ @maxscans = ] max_scans` 로그에서 모든 행을 추출 하기 위해 실행할 최대 검색 주기 수입니다. *max_scans* 은 **int** 이며 기본값은 10입니다.  
  
`[ @continuous = ] continuous` 단일 검색 주기를 실행 한 후 저장 프로시저를 종료할지 (0), 아니면 검색 주기를 다시 실행 하기 전에 *polling_interval* 에 지정 된 시간 동안 일시 중지 해야 하는지를 나타냅니다 (1). *연속* 은 **tinyint** 이며 기본값은 0입니다.  
  
`[ @pollinginterval = ] polling_interval` 로그 검색 주기 사이의 시간 (초)입니다. *polling_interval* 는 **bigint** 이며 기본값은 0입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 변경 데이터 캡처에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 캡처 작업이 사용되면 sys.sp_cdc_scan이 sys.sp_MScdc_capture_job에 의해 내부적으로 호출됩니다. 변경 데이터 캡처 로그 검색 작업이 이미 활성화되어 있거나 데이터베이스에 트랜잭션 복제가 설정되어 있는 경우에는 이 프로시저를 명시적으로 실행할 수 없습니다. 이 저장 프로시저는 자동으로 구성되는 캡처 작업의 동작을 사용자 지정하려는 관리자만 사용해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
