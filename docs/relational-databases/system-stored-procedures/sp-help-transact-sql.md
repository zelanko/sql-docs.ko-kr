---
title: sp_help (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac6e69db443bd23c3e9b1119b21d8fd98ebe39c4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815753"
---
# <a name="sp_help-transact-sql"></a>sp_help(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스 개체 ( **sys.debug** 호환성 보기에 나열 된 개체), 사용자 정의 데이터 형식 또는 데이터 형식에 대 한 정보를 보고 합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @objname = ] 'name'`**Sysobject** 또는 **systypes** 테이블에 있는 모든 사용자 정의 데이터 형식의 개체 이름입니다. *name* 은 **nvarchar (** 776 **)** 이며 기본값은 NULL입니다. 데이터베이스 이름은 허용되지 않습니다.  'Person.AddressType' 또는 [Person.AddressType]과 같이 둘 또는 세 부분으로 된 이름을 구분해야 합니다.   
   
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 반환 되는 결과 집합은 *name* 이 지정 되었는지 여부, 지정 된 경우 및 해당 개체에 대 한 데이터베이스 개체에 따라 달라 집니다.  
  
1.  인수 없이 **sp_help** 를 실행 하면 현재 데이터베이스에 있는 모든 유형의 개체에 대 한 요약 정보가 반환 됩니다.  
  
    |열 이름|데이터 형식|Description|  
    |-----------------|---------------|-----------------|  
    |**이름**|**nvarchar (** 128 **)**|개체 이름|  
    |**소유자**|**nvarchar (** 128 **)**|개체 소유자. 개체를 소유한 데이터베이스 보안 주체로, 기본적으로 개체가 포함된 스키마의 소유자로 설정됩니다.|  
    |**Object_type**|**nvarchar (** 31 **)**|개체 유형|  
  
2.  *Name* 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 또는 사용자 정의 데이터 형식인 경우 **sp_help** 는이 결과 집합을 반환 합니다.  
  
    |열 이름|데이터 형식|Description|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar (** 128 **)**|데이터 형식의 이름입니다.|  
    |**Storage_type**|**nvarchar (** 128 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식의 이름입니다.|  
    |**길이**|**smallint**|데이터 형식의 물리적 길이(바이트)입니다.|  
    |**Prec**|**int**|전체 자릿수(총 자릿수)입니다.|  
    |**크기 조정**|**int**|소수점 이하 자릿수입니다.|  
    |**Null 허용**|**varchar (** 35 **)**|NULL 값이 허용 되는지 여부를 나타냅니다 (예 또는 아니요).|  
    |**Default_name**|**nvarchar (** 128 **)**|해당 형식에 바인딩된 기본값의 이름입니다.<br /><br /> NULL = 기본값이 바인딩되지 않습니다.|  
    |**Rule_name**|**nvarchar (** 128 **)**|해당 형식에 바인딩된 규칙의 이름입니다.<br /><br /> NULL = 기본값이 바인딩되지 않습니다.|  
    |**데이터 정렬**|**sysname**|데이터 형식의 데이터 정렬입니다. 문자가 아닌 데이터 형식의 경우 NULL입니다.|  
  
3.  *Name* 이 데이터 형식이 아닌 다른 데이터베이스 개체 이면 지정 된 개체 형식에 따라이 결과 집합과 추가 결과 집합을 반환 **sp_help** 반환 합니다.  

    |열 이름|데이터 형식|Description|  
    |-----------------|---------------|-----------------|  
    |**이름**|**nvarchar (** 128 **)**|테이블 이름|  
    |**소유자**|**nvarchar (** 128 **)**|테이블 소유자입니다.|  
    |**Type**|**nvarchar (** 31 **)**|테이블 유형입니다.|  
    |**Created_datetime**|**datetime**|테이블을 만든 날짜입니다.|  
  
     지정 된 데이터베이스 개체에 따라 **sp_help** 는 추가 결과 집합을 반환 합니다.  
  
     *Name* 이 시스템 테이블, 사용자 테이블 또는 뷰 인 경우 **sp_help** 는 다음 결과 집합을 반환 합니다. 단, 뷰의 경우 파일 그룹에서 데이터 파일의 위치를 설명하는 결과 집합은 반환되지 않습니다.  
  
    -   열 개체에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar (** 128 **)**|열 이름입니다.|  
        |**Type**|**nvarchar (** 128 **)**|열의 데이터 형식입니다.|  
        |**더한**|**varchar (** 35 **)**|열의 값이 계산 되는지 여부를 나타냅니다 (예 또는 아니요).|  
        |**길이**|**int**|열 길이(바이트)입니다.<br /><br /> 참고: 열 데이터 형식이 많은 값 형식 (**varchar (max)**, **nvarchar (max)**, **varbinary (max)** 또는 **xml**) 이면 값이-1로 표시 됩니다.|  
        |**Prec**|**char (** 5 **)**|열의 전체 자릿수입니다.|  
        |**크기 조정**|**char (** 5 **)**|열의 소수 자릿수입니다.|  
        |**Null 허용**|**varchar (** 35 **)**|열에 NULL 값을 사용할 수 있는지 여부를 나타냅니다 (예 또는 아니요).|  
        |**TrimTrailingBlanks**|**varchar (** 35 **)**|후행 공백을 자를지 여부를 Yes 또는 No로 표시합니다.|  
        |**FixedLenNullInSource**|**varchar (** 35 **)**|이전 버전과의 호환성을 위해서만 지원됩니다.|  
        |**데이터 정렬**|**sysname**|열의 데이터 정렬입니다. 문자가 아닌 데이터 형식의 경우 NULL을 반환합니다.|  
  
    -   ID 열에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**ID**|**nvarchar (** 128 **)**|데이터 형식이 ID로 선언되는 열의 이름입니다.|  
        |**Seed**|**numeric**|ID 열의 시작 값입니다.|  
        |**씩**|**numeric**|해당 열의 값에 대해 사용하는 증가값입니다.|  
        |**복제용 아님**|**int**|**Sqlrepl**과 같은 복제 로그인이 테이블에 데이터를 삽입 하는 경우 IDENTITY 속성이 적용 되지 않습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   열에 대해 반환된 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|GUID(Globally Unique Identifier) 열의 이름입니다.|  
  
    -   파일 그룹에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar (** 128 **)**|데이터가 있는 파일 그룹 (주, 보조 또는 트랜잭션 로그)입니다.|  
  
    -   인덱스에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|인덱스 이름입니다.|  
        |**Index_description**|**varchar (** 210 **)**|인덱스에 대한 설명입니다.|  
        |**index_keys**|**nvarchar (** 2078 **)**|인덱스가 작성된 열의 이름입니다. xVelocity 메모리 최적화 columnstore 인덱스에 대해서는 NULL을 반환합니다.|  
  
    -   제약 조건에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar (** 146 **)**|제약 조건의 유형입니다.|  
        |**constraint_name**|**nvarchar (** 128 **)**|제약 조건의 이름입니다.|  
        |**delete_action**|**nvarchar (** 9 **)**|DELETE 동작이 NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT 또는 N/A 인지 여부를 나타냅니다.<br /><br /> FOREIGN KEY 제약 조건에만 적용됩니다.|  
        |**update_action**|**nvarchar (** 9 **)**|업데이트 동작이 NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT 또는 N/A 인지를 나타냅니다.<br /><br /> FOREIGN KEY 제약 조건에만 적용됩니다.|  
        |**status_enabled**|**varchar (** 8 **)**|제약 조건이 사용 되는지 여부를 나타냅니다. Enabled, Disabled 또는 N/A입니다.<br /><br /> CHECK 및 FOREIGN KEY 제약 조건에만 적용됩니다.|  
        |**status_for_replication**|**varchar (** 19 **)**|복제에 제약 조건을 적용할지 여부를 나타냅니다.<br /><br /> CHECK 및 FOREIGN KEY 제약 조건에만 적용됩니다.|  
        |**constraint_keys**|**nvarchar (** 2078 **)**|제약 조건을 구성하는 열의 이름이거나, 기본값 및 규칙의 경우에는 기본값 또는 규칙을 정의하는 텍스트입니다.|  
  
    -   참조하는 개체에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**Table is referenced by**|**nvarchar (** 516 **)**|테이블을 참조하는 다른 데이터베이스 개체를 식별합니다.|  
  
    -   저장 프로시저, 함수 또는 확장 저장 프로시저에 대해 반환되는 추가 결과 집합입니다.  
  
        |열 이름|데이터 형식|Description|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**nvarchar (** 128 **)**|저장 프로시저 매개 변수의 이름입니다.|  
        |**Type**|**nvarchar (** 128 **)**|저장 프로시저 매개 변수의 데이터 형식입니다.|  
        |**길이**|**smallint**|물리적 스토리지의 최대 길이(바이트)입니다.|  
        |**Prec**|**int**|전체 자릿수 또는 총 자릿수입니다.|  
        |**크기 조정**|**int**|소수점 오른쪽 자릿수입니다.|  
        |**Param_order**|**smallint**|매개 변수의 순서입니다.|  
  
## <a name="remarks"></a>설명  
 **Sp_help** 프로시저는 현재 데이터베이스 에서만 개체를 찾습니다.  
  
 *Name* 을 지정 하지 않으면 **sp_help** 는 현재 데이터베이스의 모든 개체에 대 한 개체 이름, 소유자 및 개체 유형을 나열 합니다. **sp_helptrigger** 는 트리거에 대 한 정보를 제공 합니다.  
  
 **sp_help** 는 정렬 가능 인덱스 열만 노출 합니다. 따라서 XML 인덱스 또는 공간 인덱스에 대 한 정보를 노출 하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 사용자에 게는 *objname*에 대해 하나 이상의 사용 권한이 있어야 합니다. 열 제약 조건 키, 기본값 또는 규칙을 보려면 테이블에 대한 VIEW DEFINITION 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-information-about-all-objects"></a>A. 모든 개체에 대한 정보 반환  
 다음 예에서는 `master` 데이터베이스의 각 개체에 대한 정보를 나열합니다.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>B. 단일 개체에 대한 정보 반환  
 다음 예에서는 `Person` 테이블에 대한 정보를 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_helpindex &#40;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [Transact-sql&#41;sp_helprotect &#40;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [Transact-sql&#41;sp_helpserver &#40;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [Transact-sql&#41;sp_helpuser &#40;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
