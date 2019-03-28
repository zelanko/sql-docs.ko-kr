---
title: sp_server_info (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_info
- sp_server_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_info
ms.assetid: 2dc2c262-3cfa-4a84-8127-3632ba583543
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 034c4ab2c8ce57ac072e9711fb4e6d621584f273
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529305"
---
# <a name="spserverinfo-transact-sql"></a>sp_server_info(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터베이스 게이트웨이 또는 기본 데이터 원본에 대해 특성 이름의 목록과 특성 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_server_info [[@attribute_id = ] 'attribute_id']  
```  
  
## <a name="arguments"></a>인수  
`[ @attribute_id = ] 'attribute_id'` 특성의 정수 ID입니다. *attribute_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**ATTRIBUTE_ID**|**int**|특성의 ID 번호입니다.|  
|**ATTRIBUTE_NAME**|**varchar(** 60 **)**|특성 이름입니다.|  
|**ATTRIBUTE_VALUE**|**varchar(** 255 **)**|특성의 현재 설정입니다.|  
  
 다음 표에서는 특성을 나열합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC 클라이언트 라이브러리는 현재 특성을 사용 **1**, **2**합니다 **18**를 **22**, 및 **500** 연결 시 시간입니다.  
  
|ATTRIBUTE_ID|ATTRIBUTE_NAME 설명|ATTRIBUTE_VALUE|  
|-------------------|---------------------------------|----------------------|  
|**1**|DBMS_NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**2**|DBMS_VER|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - *x.xx.xxxx*|  
|**10**|OWNER_TERM|owner|  
|**11**|TABLE_TERM|테이블|  
|**12**|MAX_OWNER_NAME_LENGTH|128|  
|**13**|TABLE_LENGTH<br /><br /> 테이블 이름에 사용할 수 있는 최대 문자 수를 나타냅니다.|128|  
|**14**|MAX_QUAL_LENGTH<br /><br /> 테이블 한정자 이름(세 부분으로 구성된 테이블 이름의 첫 번째 부분)에 사용할 수 있는 최대 길이를 나타냅니다.|128|  
|**15**|COLUMN_LENGTH<br /><br /> 열 이름에 사용할 수 있는 최대 문자 수를 나타냅니다.|128|  
|**16**|IDENTIFIER_CASE<br /><br /> 데이터베이스 내의 테이블, 열, 저장 프로시저(시스템 카탈로그 내의 개체)의 사용자 정의 이름에 대한 대/소문자 구분 여부를 나타냅니다.|SENSITIVE|  
|**17**|TX_ISOLATION<br /><br /> 서버가 가정하는 초기 트랜잭션 격리 수준을 나타냅니다. 이 값은 SQL-92에 정의된 격리 수준에 해당합니다.|2|  
|**18**|COLLATION_SEQ<br /><br /> 해당 서버의 문자 집합 순서를 나타냅니다.|charset=iso_1 sort_order=dictionary_iso charset_num=1 sort_order_num=51|  
|**19**|SAVEPOINT_SUPPORT<br /><br /> 기본 DBMS가 명명된 저장점을 지원하는지를 나타냅니다.|Y|  
|**20**|MULTI_RESULT_SETS<br /><br /> 기본 데이터베이스 또는 게이트웨이가 여러 결과 집합을 지원하는지를 나타냅니다. 지원될 경우 게이트웨이를 통해 여러 결과 집합을 클라이언트에 반환하는 여러 문을 보낼 수 있습니다.|Y|  
|**22**|ACCESSIBLE_TABLES<br /><br /> 지정에서 든 **sp_tables**, 게이트웨이가 테이블, 뷰 및 등등으로 현재 사용자 (즉, 테이블에 대해 최소한 SELECT 권한이 있는 사용자)가 액세스할 수를 반환 합니다.|Y|  
|**100**|USERID_LENGTH<br /><br /> 사용자 이름에 사용할 수 있는 최대 문자 수를 나타냅니다.|128|  
|**101**|QUALIFIER_TERM<br /><br /> 세 부분으로 구성된 이름 중 첫 번째 부분인 테이블 한정자에 대한 DBMS 공급업체 용어를 나타냅니다.|database|  
|**102**|NAMED_TRANSACTIONS<br /><br /> 기본 DBMS가 명명된 트랜잭션을 지원하는지를 나타냅니다.|Y|  
|**103**|SPROC_AS_LANGUAGE<br /><br /> 저장 프로시저가 언어 이벤트로 실행될 수 있는지 나타냅니다.|Y|  
|**104**|ACCESSIBLE_SPROC<br /><br /> 지정에서 든 **sp_stored_procedures**, 게이트웨이가 현재 사용자가 실행 된 저장된 프로시저만 반환 합니다.|Y|  
|**105**|MAX_INDEX_COLS<br /><br /> DBMS의 인덱스에 사용 가능한 최대 열 수를 나타냅니다.|16|  
|**106**|RENAME_TABLE<br /><br /> 테이블의 이름을 바꿀 수 있는지를 나타냅니다.|Y|  
|**107**|RENAME_COLUMN<br /><br /> 열의 이름을 바꿀 수 있는지를 나타냅니다.|Y|  
|**108**|DROP_COLUMN<br /><br /> 열을 삭제할 수 있는지를 나타냅니다.|Y|  
|**109**|INCREASE_COLUMN_LENGTH<br /><br /> 열 크기를 늘일 수 있는지 나타냅니다.|Y|  
|**110**|DDL_IN_TRANSACTION<br /><br /> 트랜잭션에 DDL 문을 표시할 수 있는지를 나타냅니다.|Y|  
|**111**|DESCENDING_INDEXES<br /><br /> 내림차순 인덱스를 지원하는지를 나타냅니다.|Y|  
|**112**|SP_RENAME<br /><br /> 저장 프로시저의 이름을 다시 정할 수 있는지를 나타냅니다.|Y|  
|**113**|REMOTE_SPROC<br /><br /> DB-Library의 원격 저장 프로시저 기능을 통해 저장 프로시저를 실행할 수 있는지 나타냅니다.|Y|  
|**500**|SYS_SPROC_VERSION<br /><br /> 저장 프로시저가 현재 구현하고 있는 카탈로그의 버전을 나타냅니다.|현재 버전 번호|  
  
## <a name="remarks"></a>Remarks  
 **sp_server_info** 에서 제공 된 정보의 하위 집합을 반환 **SQLGetInfo** ODBC에서.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
