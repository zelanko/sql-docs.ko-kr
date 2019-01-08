---
title: sp_setdefaultdatatypemapping (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c229fe6355e4fe463038dd7ef44d89217b0de77
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202232"
---
# <a name="spsetdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  표시 간에 기존 데이터 형식 매핑을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 관리 시스템 (DBMS)를 기본값으로 합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@mapping_id=** ] *mapping_id*  
 기존 데이터 형식 매핑을 식별합니다.  *mapping_id* 됩니다 **int**, 기본값은 NULL입니다. 지정 하는 경우 *mapping_id*, 나머지 매개 변수를 필요 하지 않습니다.  
  
 [ **@source_dbms**=] **'***source_dbms***'**  
 데이터 형식이 매핑된 DBMS의 이름입니다. *source_dbms* 됩니다 **sysname**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|원본은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|원본은 Oracle 데이터베이스입니다.|  
|NULL(기본값)||  
  
 경우에이 매개 변수를 지정 해야 합니다 *mapping_id* NULL입니다.  
  
 [  **@source_version=** ] **'***source_version***'**  
 원본 DBMS의 버전 번호입니다. *source_version* 됩니다 **varchar(10)**, 기본값은 NULL입니다.  
  
 [ **@source_type**=] **'***source_type***'**  
 원본 DBMS의 데이터 형식입니다. *source_type* 됩니다 **sysname**합니다. 경우에이 매개 변수를 지정 해야 합니다 *mapping_id* NULL입니다.  
  
 [  **@source_length_min=** ] *source_length_min*  
 원본 DBMS에서 해당 데이터 형식의 최소 길이입니다. *source_length_min* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
 [  **@source_length_max=** ] *source_length_max*  
 원본 DBMS에서 해당 데이터 형식의 최대 길이입니다 *source_length_max* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
 [  **@source_precision_min=** ] *source_precision_min*  
 원본 DBMS에서 해당 데이터 형식의 최소 전체 자릿수입니다. *source_precision_min* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
 [  **@source_precision_max=** ] *source_precision_max*  
 원본 DBMS에서 해당 데이터 형식의 최대 전체 자릿수입니다. *source_precision_max* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
 [  **@source_scale_min=** ] *source_scale_min*  
 원본 DBMS에서 해당 데이터 형식의 최소 소수 자릿수입니다. *source_scale_min* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@source_scale_max=** ] *source_scale_max*  
 원본 DBMS에서 해당 데이터 형식의 최대 소수 자릿수입니다. *source_scale_max* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@source_nullable=** ] *source_nullable*  
 원본 DBMS의 데이터 형식이 NULL 값을 지원하는지 여부입니다. *source_nullable* 됩니다 **비트**, 기본값은 NULL입니다. **1** NULL 값이 지원 되는 것을 의미 합니다.  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 대상 DBMS의 이름입니다. *destination_dbms* 됩니다 **sysname**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|대상은 Oracle 데이터베이스입니다.|  
|**DB2**|대상은 IBM DB2 데이터베이스입니다.|  
|**SYBASE**|대상은 Sybase 데이터베이스입니다.|  
|NULL(기본값)||  
  
 [ **@destination_version**=] **'***destination_version***'**  
 대상 DBMS의 제품 버전입니다. *destination_version* 됩니다 **varchar(10)**, 기본값은 NULL입니다.  
  
 [ **@destination_type**=] **'***destination_type***'**  
 대상 DBMS에 나열된 데이터 형식입니다. *destination_type* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@destination_length=** ] *destination_length*  
 대상 DBMS에서 해당 데이터 형식의 길이입니다. *destination_length* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
 [  **@destination_precision=** ] *destination_precision*  
 대상 DBMS에서 해당 데이터 형식의 전체 자릿수입니다. *destination_precision* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
 [  **@destination_scale=** ] *destination_scale*  
 대상 DBMS에서 해당 데이터 형식의 소수 자릿수입니다. *destination_scale* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@destination_nullable=** ] *destination_nullable*  
 대상 DBMS의 데이터 형식이 NULL 값을 지원하는지 여부입니다. *destination_nullable* 됩니다 **비트**, 기본값은 NULL입니다. **1** NULL 값이 지원 되는 것을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_setdefaultdatatypemapping** 간 복제의 모든 형식에 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS 합니다.  
  
 기본 데이터 형식 매핑은 지정된 DBMS를 포함하는 모든 복제 토폴로지에 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_setdefaultdatatypemapping**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
