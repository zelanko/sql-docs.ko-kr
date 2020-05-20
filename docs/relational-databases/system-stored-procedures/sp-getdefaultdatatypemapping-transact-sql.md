---
title: sp_getdefaultdatatypemapping (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e85eb432123c30338b15528edcb7c301e2dc458b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833182"
---
# <a name="sp_getdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS (데이터베이스 관리 시스템) 간에 지정 된 데이터 형식에 대 한 기본 매핑에 대 한 정보를 반환 합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @source_dbms = ] 'source_dbms'`데이터 형식이 매핑되는 DBMS의 이름입니다. *source_dbms* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**|원본은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|원본은 Oracle 데이터베이스입니다.|  
  
 이 매개 변수를 지정해야 합니다.  
  
`[ @source_version = ] 'source_version'`원본 DBMS의 버전 번호입니다. *source_version* 는 **varchar (10)** 이며 기본값은 NULL입니다.  
  
`[ @source_type = ] 'source_type'`원본 DBMS의 데이터 형식입니다. *source_type* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @source_length = ] source_length`원본 DBMS에 있는 데이터 형식의 길이입니다. *source_length* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @source_precision = ] source_precision`원본 DBMS에 있는 데이터 형식의 전체 자릿수입니다. *source_precision* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @source_scale = ] source_scale`원본 DBMS에 있는 데이터 형식의 소수 자릿수입니다. *source_scale* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @source_nullable = ] source_nullable`원본 DBMS의 데이터 형식이 NULL 값을 지원 하는지 여부입니다. *source_nullable* 은 **bit**이며 기본값은 **1**입니다 .이 값은 NULL 값이 지원 됨을 의미 합니다.  
  
`[ @destination_dbms = ] 'destination_dbms'`대상 DBMS의 이름입니다. *destination_dbms* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**|대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**ORACLE**|대상은 Oracle 데이터베이스입니다.|  
|**DB2**|대상은 IBM DB2 데이터베이스입니다.|  
|**SYBASE**|대상은 Sybase 데이터베이스입니다.|  
  
 이 매개 변수를 지정해야 합니다.  
  
`[ @destination_version = ] 'destination_version'`대상 DBMS의 제품 버전입니다. *destination_version* 는 **varchar (10)** 이며 기본값은 NULL입니다.  
  
`[ @destination_type = ] 'destination_type' OUTPUT`대상 DBMS에 나열 된 데이터 형식입니다. *destination_type* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @destination_length = ] destination_length OUTPUT`대상 DBMS에 있는 데이터 형식의 길이입니다. *destination_length* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @destination_precision = ] destination_precision OUTPUT`대상 DBMS에 있는 데이터 형식의 전체 자릿수입니다. *destination_precision* 는 **bigint**이며 기본값은 NULL입니다.  
  
`[ @destination_scale = ] _destination_scaleOUTPUT`대상 DBMS에 있는 데이터 형식의 소수 자릿수입니다. *destination_scale* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @destination_nullable = ] _destination_nullableOUTPUT`대상 DBMS의 데이터 형식이 NULL 값을 지원 하는지 여부입니다. *destination_nullable* 은 **bit**이며 기본값은 NULL입니다. **1** 은 NULL 값이 지원 됨을 의미 합니다.  
  
`[ @dataloss = ] _datalossOUTPUT`매핑의 데이터가 손실 될 가능성이 있는지 여부입니다. *데이터 손실을* 는 **bit**이며 기본값은 NULL입니다. **1** 은 데이터가 손실 될 가능성이 있음을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_getdefaultdatatypemapping** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 비 DBMS 간에 모든 유형의 복제에 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **sp_getdefaultdatatypemapping** 는 지정 된 원본 데이터 형식과 가장 일치 하는 기본 대상 데이터 형식을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_getdefaultdatatypemapping**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_helpdatatypemap &#40;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [Transact-sql&#41;sp_setdefaultdatatypemapping &#40;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 구독자](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle 구독자](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
