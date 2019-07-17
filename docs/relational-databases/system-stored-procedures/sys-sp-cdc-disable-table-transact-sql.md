---
title: sys.sp_cdc_disable_table (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
author: rothja
ms.author: jroth
ms.openlocfilehash: 693c449679433b733cfc3a45e2bbedf3f1d92185
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106515"
---
# <a name="sysspcdcdisabletable-transact-sql"></a>sys.sp_cdc_disable_table(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 지정된 원본 테이블 및 캡처 인스턴스에 대한 변경 데이터 캡처를 비활성화합니다. 변경 데이터 캡처는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @source_schema = ] 'source\_schema'` 원본 테이블이 포함 되는 스키마의 이름이입니다. *source_schema* 됩니다 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 *source_schema* 현재 데이터베이스에 존재 해야 합니다.  
  
`[ @source_name = ] 'source\_name'` 변경에서 데이터 캡처는 사용 하지 않도록 설정할 원본 테이블의 이름이입니다. *source_name* 됩니다 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 *source_name* 현재 데이터베이스에 존재 해야 합니다.  
  
`[ @capture_instance = ] 'capture\_instance' | 'all'` 지정된 된 원본 테이블에 대해 비활성화할 캡처 인스턴스의 이름이입니다. *capture_instance* 됩니다 **sysname** NULL 일 수 없습니다.  
  
 모든 캡처 인스턴스에 대해 정의 된 '모두'를 지정 하면 *source_name* 비활성화 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sys.sp_cdc_disable_table** 변경 데이터 캡처 변경 테이블 및 시스템 함수 지정 된 원본 테이블 및 캡처 인스턴스와 연결 된 삭제 합니다. 변경 데이터 캡처 시스템 테이블 및 집합에서 지정 된 캡처 인스턴스와 연결 된 모든 행을 삭제 합니다 **is_tracked_by_cdc** 테이블 항목에 대 한 열을 [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) 카탈로그 뷰 0.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 고정된 데이터베이스 역할.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HumanResources.Employee` 테이블에 대해 변경 데이터 캡처를 비활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
