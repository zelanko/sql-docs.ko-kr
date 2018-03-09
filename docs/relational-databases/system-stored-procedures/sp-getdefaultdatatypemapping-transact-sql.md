---
title: sp_getdefaultdatatypemapping (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords: sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db6ba2bdd02ed4ce9fe7b93132669d4f46ce40b9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spgetdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 된 데이터 형식 사이 대 한 기본 매핑에 정보를 반환 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 관리 시스템 (DBMS). 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@source_dbms** =] **'***source_dbms***'**  
 데이터 형식이 매핑된 DBMS의 이름입니다. *source_dbms* 은 **sysname**, 다음 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|원본은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|원본은 Oracle 데이터베이스입니다.|  
  
 이 매개 변수를 지정해야 합니다.  
  
 [  **@source_version=** ] **'***source_version***'**  
 원본 DBMS의 버전 번호입니다. *source_version* 은 **varchar (10)**, 기본값은 NULL입니다.  
  
 [  **@source_type** =] **'***source_type***'**  
 원본 DBMS의 데이터 형식입니다. *source_type* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@source_length=** ] *source_length*  
 원본 DBMS에서 해당 데이터 형식의 길이입니다. *source_length* 은 **bigint**, 기본값은 NULL입니다.  
  
 [  **@source_precision=** ] *source_precision*  
 원본 DBMS에서 해당 데이터 형식의 전체 자릿수입니다. *source_precision* 은 **bigint**, 기본값은 NULL입니다.  
  
 [  **@source_scale=** ] *source_scale*  
 원본 DBMS에서 해당 데이터 형식의 소수 자릿수입니다. *source_scale* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@source_nullable=** ] *source_nullable*  
 원본 DBMS의 데이터 형식이 NULL 값을 지원하는지 여부입니다. *source_nullable* 은 **비트**의 기본값은 **1**, 즉, NULL 값이 지원 됩니다.  
  
 [  **@destination_dbms**  =] **'***destination_dbms***'**  
 대상 DBMS의 이름입니다. *destination_dbms* 은 **sysname**, 다음 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|대상은 Oracle 데이터베이스입니다.|  
|**DB2**|대상은 IBM DB2 데이터베이스입니다.|  
|**SYBASE**|대상은 Sybase 데이터베이스입니다.|  
  
 이 매개 변수를 지정해야 합니다.  
  
 [  **@destination_version** =] **'***destination_version***'**  
 대상 DBMS의 제품 버전입니다. *destination_version* 은 **varchar (10)**, 기본값은 NULL입니다.  
  
 [  **@destination_type** =] **'***destination_type***'** 출력  
 대상 DBMS에 나열된 데이터 형식입니다. *destination_type* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@destination_length=** ] *destination_length* 출력  
 대상 DBMS에서 해당 데이터 형식의 길이입니다. *destination_length* 은 **bigint**, 기본값은 NULL입니다.  
  
 [  **@destination_precision=** ] *destination_precision* 출력  
 대상 DBMS에서 해당 데이터 형식의 전체 자릿수입니다. *destination_precision* 은 **bigint**, 기본값은 NULL입니다.  
  
 [  **@destination_scale=** ] *destination_scale***출력**  
 대상 DBMS에서 해당 데이터 형식의 소수 자릿수입니다. *destination_scale* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@destination_nullable=** ] *destination_nullable***출력**  
 대상 DBMS의 데이터 형식이 NULL 값을 지원하는지 여부입니다. *destination_nullable* 은 **비트**, 기본값은 NULL입니다. **1** NULL 값이 지원 됨을 의미 합니다.  
  
 [  **@dataloss=** ] *dataloss***출력**  
 매핑에서 데이터가 손실될 가능성이 있는지 여부입니다. *dataloss* 은 **비트**, 기본값은 NULL입니다. **1** 데이터 손실 가능성이 있다는 것을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_getdefaultdatatypemapping** 모든 유형의 간 복제에 사용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS 합니다.  
  
 **sp_getdefaultdatatypemapping** 기본 대상 데이터 형식에 지정 된 원본 데이터 형식이 가장 일치를 반환 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_getdefaultdatatypemapping**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_helpdatatypemap &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle 구독자](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
