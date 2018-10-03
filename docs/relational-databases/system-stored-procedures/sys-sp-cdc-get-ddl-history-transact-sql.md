---
title: sys.sp_cdc_get_ddl_history (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 657d7b6cc21c573d2d9535d36392f9b7eb94200f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827223"
---
# <a name="sysspcdcgetddlhistory-transact-sql"></a>sys.sp_cdc_get_ddl_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 캡처 인스턴스에 대해 변경 데이터 캡처를 사용하도록 설정한 시점부터의 캡처 인스턴스 관련 DDL(데이터 정의 언어) 변경 기록을 반환합니다. 변경 데이터 캡처는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>인수  
 [ @capture_instance =] '*capture_instance*'  
 원본 테이블과 연결된 캡처 인스턴스의 이름입니다. *capture_instance* 됩니다 **sysname** NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|원본 테이블 스키마의 이름입니다.|  
|source_table|**sysname**|원본 테이블의 이름입니다.|  
|capture_instance|**sysname**|캡처 인스턴스의 이름입니다.|  
|required_column_update|**bit**|DDL 변경 시에 원본 열에서 변경된 데이터 형식이 반영되도록 변경 테이블의 열을 변경했음을 나타냅니다.|  
|ddl_command|**nvarchar(max)**|원본 테이블에 적용된 DDL 문입니다.|  
|ddl_lsn|**binary(10)**|DDL 변경과 관련된 LSN(로그 시퀀스 번호)입니다.|  
|ddl_time|**datetime**|DDL 변경과 관련된 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 원본 테이블 열 구조의 추가 열을 삭제 하거나 기존 열의 데이터 형식을 변경 등을 변경 하는 원본 테이블에 DDL 수정에서 유지 관리 합니다 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) 테이블입니다. 이러한 변경 내용은 이 저장 프로시저를 사용하여 보고할 수 있습니다. cdc.ddl_history의 항목은 캡처 프로세스에서 로그의 DDL 트랜잭션을 읽을 때 생성됩니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스의 모든 캡처 인스턴스에 대한 행을 반환하려면 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다. 다른 모든 사용자의 경우 원본 테이블에서 캡처된 모든 열에 대한 SELECT 권한이 필요하며 캡처 인스턴스에 대한 제어 역할이 정의된 경우 해당 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음은 원본 테이블 `HumanResources.Employee`에 열을 추가하고 `sys.sp_cdc_get_ddl_history` 저장 프로시저를 실행하여 캡처 인스턴스 `HumanResources_Employee`와 연관된 원본 테이블에 적용되는 DDL 변경 내용을 보고하는 예입니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
