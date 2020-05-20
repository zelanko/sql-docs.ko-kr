---
title: 변경 데이터 캡처 테이블 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e98c770db0f1fc9c89275fc973a2bdee8ee4508f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825948"
---
# <a name="change-data-capture-tables-transact-sql"></a>변경 데이터 캡처 테이블(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  변경 데이터 캡처를 사용하면 테이블에 대한 변경 추적이 가능하므로 테이블에 적용된 DML(데이터 조작 언어) 및 DDL(데이터 정의 언어) 변경 내용을 데이터 웨어하우스에 증분 로드할 수 있습니다. 이 섹션의 항목에서는 변경 데이터 캡처 작업에 사용되는 정보를 저장하는 시스템 테이블에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [cdc. <capture_instance>_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
 관련된 원본 테이블에서 캡처된 열에 적용된 각 변경에 대해 한 개의 행을 반환합니다.  
  
 [cdc.captured_columns](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
 캡처 인스턴스에서 추적된 각 열에 대해 하나의 행을 반환합니다.  
  
 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
 데이터베이스 내의 각 변경 테이블에 대해 한 개의 행을 반환합니다.  
  
 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)  
 변경 데이터 캡처가 활성화된 테이블에 적용된 각 DDL(데이터 정의 언어) 변경에 대해 한 개의 행을 반환합니다.  
  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)  
 변경 테이블에 행이 있는 각 트랜잭션에 대해 한 개의 행을 반환합니다. 이 테이블은 LSN(로그 시퀀스 번호) 커밋 값과 트랜잭션 커밋 시간을 매핑하는 데 사용됩니다.  
  
 [cdc.index_columns](../../relational-databases/system-tables/cdc-index-columns-transact-sql.md)  
 변경 테이블과 관련된 각 인덱스 열에 대해 하나의 행을 반환합니다.  
  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 변경 데이터 캡처 에이전트 작업에 대한 구성 매개 변수를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;변경 데이터 캡처 저장 프로시저](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [변경 데이터 캡처 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
