---
title: sp_setdefaultdatatypemapping (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 96e4959ffa88e96d6236b460d515353d6817f656
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901310"
---
# <a name="sp_setdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS (데이터베이스 관리 시스템)가 아닌 기존 데이터 형식 매핑을 기본값으로 표시 합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_setdefaultdatatypemapping [ [ @mapping_id = ] mapping_id ]  
    [ , [ @source_dbms = ] 'source_dbms' ]  
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @source_length_min = ] source_length_min ]  
    [ , [ @source_length_max = ] source_length_max ]  
    [ , [ @source_precision_min = ] source_precision_min ]  
    [ , [ @source_precision_max = ] source_precision_max ]  
    [ , [ @source_scale_min = ] source_scale_min ]  
    [ , [ @source_scale_max = ] source_scale_max ]  
    [ , [ @source_nullable = ] source_nullable ]  
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @destination_length = ] destination_length ]  
    [ , [ @destination_precision = ] destination_precision ]  
    [ , [ @destination_scale = ] destination_scale ]  
    [ , [ @destination_nullable = ] source_nullable ]  
```  
  
## <a name="arguments"></a>인수  
`[ @mapping_id = ] mapping_id`기존 데이터 형식 매핑을 식별 합니다.  *mapping_id* 은 **int**이며 기본값은 NULL입니다. *Mapping_id*지정 하는 경우 나머지 매개 변수는 필요 하지 않습니다.  
  
`[ @source_dbms = ] 'source_dbms'`데이터 형식이 매핑되는 DBMS의 이름입니다. *source_dbms* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**|원본은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|원본은 Oracle 데이터베이스입니다.|  
|NULL(기본값)||  
  
 *MAPPING_ID* NULL 인 경우이 매개 변수를 지정 해야 합니다.  
  
`[ @source_version = ] 'source_version'`원본 DBMS의 버전 번호입니다. *source_version* 는 **varchar (10)** 이며 기본값은 NULL입니다.  
  
`[ @source_type = ] 'source_type'`원본 DBMS의 데이터 형식입니다. *source_type* 는 **sysname**입니다. *MAPPING_ID* NULL 인 경우이 매개 변수를 지정 해야 합니다.  
  
`[ @source_length_min = ] source_length_min`원본 DBMS에 있는 데이터 형식의 최소 길이입니다. *source_length_min* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @source_length_max = ] source_length_max`원본 DBMS에 있는 데이터 형식의 최대 길이입니다. *source_length_max* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @source_precision_min = ] source_precision_min`원본 DBMS에 있는 데이터 형식의 최소 전체 자릿수입니다. *source_precision_min* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @source_precision_max = ] source_precision_max`원본 DBMS에 있는 데이터 형식의 최대 전체 자릿수입니다. *source_precision_max* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @source_scale_min = ] source_scale_min`원본 DBMS에 있는 데이터 형식의 최소 소수 자릿수입니다. *source_scale_min* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @source_scale_max = ] source_scale_max`원본 DBMS에 있는 데이터 형식의 최대 소수 자릿수입니다. *source_scale_max* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @source_nullable = ] source_nullable`원본 DBMS의 데이터 형식이 NULL 값을 지원 하는지 여부입니다. *source_nullable* 은 **bit**이며 기본값은 NULL입니다. **1** 은 NULL 값이 지원 됨을 의미 합니다.  
  
`[ @destination_dbms = ] 'destination_dbms'`대상 DBMS의 이름입니다. *destination_dbms* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**|대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|대상은 Oracle 데이터베이스입니다.|  
|**DB2**|대상은 IBM DB2 데이터베이스입니다.|  
|**SYBASE**|대상은 Sybase 데이터베이스입니다.|  
|NULL(기본값)||  
  
`[ @destination_version = ] 'destination_version'`대상 DBMS의 제품 버전입니다. *destination_version* 는 **varchar (10)** 이며 기본값은 NULL입니다.  
  
`[ @destination_type = ] 'destination_type'`대상 DBMS에 나열 된 데이터 형식입니다. *destination_type* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @destination_length = ] destination_length`대상 DBMS에 있는 데이터 형식의 길이입니다. *destination_length* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @destination_precision = ] destination_precision`대상 DBMS에 있는 데이터 형식의 전체 자릿수입니다. *destination_precision* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @destination_scale = ] destination_scale`대상 DBMS에 있는 데이터 형식의 소수 자릿수입니다. *destination_scale* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @destination_nullable = ] destination_nullable`대상 DBMS의 데이터 형식이 NULL 값을 지원 하는지 여부입니다. *destination_nullable* 은 **bit**이며 기본값은 NULL입니다. **1** 은 NULL 값이 지원 됨을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_setdefaultdatatypemapping** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 비 DBMS 간에 모든 유형의 복제에 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 기본 데이터 형식 매핑은 지정된 DBMS를 포함하는 모든 복제 토폴로지에 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_setdefaultdatatypemapping**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Transact-sql&#41;sp_getdefaultdatatypemapping &#40;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [Transact-sql&#41;sp_helpdatatypemap &#40;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
