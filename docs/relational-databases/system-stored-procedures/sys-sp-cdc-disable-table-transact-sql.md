---
description: sys.sp_cdc_disable_table(Transact-SQL)
title: sys. sp_cdc_disable_table (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e1dcc5dffd4c9a718227c85ce8f421b8cb45bbd8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492850"
---
# <a name="syssp_cdc_disable_table-transact-sql"></a>sys.sp_cdc_disable_table(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 지정된 원본 테이블 및 캡처 인스턴스에 대한 변경 데이터 캡처를 비활성화합니다. 변경 데이터 캡처는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @source_schema = ] 'source\_schema'` 원본 테이블이 포함 된 스키마의 이름입니다. *source_schema* 는 **sysname**이며 기본값은 없고 NULL 일 수 없습니다.  
  
 *source_schema* 는 현재 데이터베이스에 있어야 합니다.  
  
`[ @source_name = ] 'source\_name'` 변경 데이터 캡처가 비활성화 되는 원본 테이블의 이름입니다. *source_name* 는 **sysname**이며 기본값은 없고 NULL 일 수 없습니다.  
  
 *source_name* 는 현재 데이터베이스에 있어야 합니다.  
  
`[ @capture_instance = ] 'capture\_instance' | 'all'` 지정 된 원본 테이블에 대해 사용 하지 않도록 설정할 캡처 인스턴스의 이름입니다. *capture_instance* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
 ' A l l '을 지정 하면 *source_name* 에 대해 정의 된 모든 캡처 인스턴스가 비활성화 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_cdc_disable_table** 는 지정 된 원본 테이블 및 캡처 인스턴스와 연결 된 변경 데이터 캡처 변경 테이블 및 시스템 함수를 삭제 합니다. 변경 데이터 캡처 시스템 테이블에서 지정 된 캡처 인스턴스와 연결 된 모든 행을 삭제 하 고, [sys. tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) 카탈로그 뷰의 테이블 항목에 대 한 **is_tracked_by_cdc** 열을 0으로 설정 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `HumanResources.Employee` 테이블에 대해 변경 데이터 캡처를 비활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
