---
title: sys. sp_cdc_get_captured_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
author: rothja
ms.author: jroth
ms.openlocfilehash: cf7c7ff03ec1318b1fe2fca8454f8ff39cd336a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083745"
---
# <a name="syssp_cdc_get_captured_columns-transact-sql"></a>sys.sp_cdc_get_captured_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 캡처 인스턴스에서 추적한 캡처된 원본 열에 대한 변경 데이터 캡처 메타데이터 정보를 반환합니다. 변경 데이터 캡처는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>인수  
 [ @capture_instance = ] '*capture_instance*'  
 원본 테이블과 연결된 캡처 인스턴스의 이름입니다. *capture_instance* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
 테이블에 대 한 캡처 인스턴스를 보고 하려면 [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|원본 테이블 스키마의 이름입니다.|  
|source_table|**sysname**|원본 테이블의 이름입니다.|  
|capture_instance|**sysname**|캡처 인스턴스의 이름입니다.|  
|column_name|**sysname**|캡처된 원본 열의 이름입니다.|  
|column_id|**int**|원본 테이블에 있는 열의 ID입니다.|  
|column_ordinal|**int**|원본 테이블 내의 열 위치입니다.|  
|data_type|**sysname**|열의 데이터 형식입니다.|  
|character_maximum_length|**int**|문자 기반 열일 경우 최대 문자 길이이고, 그렇지 않으면 NULL입니다.|  
|numeric_precision|**tinyint**|숫자 기반일 경우에는 열의 전체 자릿수이고, 그렇지 않으면 NULL입니다.|  
|numeric_precision_radix|**smallint**|숫자 기반일 경우에는 열의 전체 자릿수 기수이고, 그렇지 않으면 NULL입니다.|  
|numeric_scale|**int**|숫자 기반일 경우에는 열의 소수 자릿수이고, 그렇지 않으면 NULL입니다.|  
|datetime_precision|**smallint**|datetime 기반일 경우에는 열의 전체 자릿수이고, 그렇지 않으면 NULL입니다.|  
  
## <a name="remarks"></a>설명  
 Sp_cdc_get_captured_columns를 사용 하 여 캡처 인스턴스 쿼리 함수 cdc를 쿼리하여 반환 된 캡처된 열에 대 한 열 정보를 가져올 수 있습니다 [. fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 또는 [cdc ](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)fn_cdc_get_net_changes_<capture_instance>. 열 이름, ID 및 위치는 캡처 인스턴스의 수명 동안 일정하게 유지됩니다. 추적된 테이블에서 기본 원본 열의 데이터 형식이 변경될 경우에만 열 데이터 형식이 변경됩니다. 원본 테이블에서 추가되거나 제거된 열은 기존 캡처 인스턴스의 캡처된 열에 영향을 미치지 않습니다.  
  
 원본 테이블에 적용 된 DDL (데이터 정의 언어) 문에 대 한 정보를 얻으려면 [sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) 를 사용 합니다. 추적되는 원본 열의 구조를 수정하는 모든 DDL 변경이 결과 집합에 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다. 다른 모든 사용자의 경우 원본 테이블에서 캡처된 모든 열에 대한 SELECT 권한이 필요하며 캡처 인스턴스에 대한 제어 역할이 정의된 경우 해당 데이터베이스 역할의 멤버 자격이 필요합니다. 호출자에게 원본 데이터를 볼 수 있는 권한이 없으면 함수는 오류 22981(개체가 없거나 액세스가 거부되었습니다)을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HumanResources_Employee` 캡처 인스턴스의 캡처된 열에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
