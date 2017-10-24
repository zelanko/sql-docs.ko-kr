---
title: column_definition (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_definition
- column_definition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column_definition
- ALTER TABLE statement
- column properties [SQL Server]
- column definitions [SQL Server]
ms.assetid: a1742649-ca29-4d9b-9975-661cdbf18f78
caps.latest.revision: 78
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c63dcea3473198ded46ebf84053fa9d8b36330f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-columndefinition-transact-sql"></a>ALTER TABLE column_definition (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용 하 여 테이블에 추가 된 열의 속성을 지정 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
column_name <data_type>  
[ FILESTREAM ]  
[ COLLATE collation_name ]   
[ NULL | NOT NULL ]  
[   
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression [ WITH VALUES ]   
    | IDENTITY [ ( seed , increment ) ] [ NOT FOR REPLICATION ]   
]  
[ ROWGUIDCOL ]   
[ SPARSE ]   
[ ENCRYPTED WITH  
  ( COLUMN_ENCRYPTION_KEY = key_name ,  
      ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
      ALGORITHM =  'AEAD_AES_256_CBC_HMAC_SHA_256'   
  ) ]  
[ MASKED WITH ( FUNCTION = ' mask_function ') ]  
[ <column_constraint> [ ...n ] ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}  
```  
  
## <a name="arguments"></a>인수  
 *column_name*  
 변경, 추가 또는 삭제할 열의 이름입니다. *column_name* 1-128 자로 구성 될 수 있습니다. 새 열의 경우 타임 스탬프 데이터 형식을 사용 하 여 만든 *column_name* 생략할 수 있습니다. 없는 경우 *column_name* 에 대해 지정 된는 **타임 스탬프** 이름, 데이터 형식 열 **타임 스탬프** 사용 됩니다.  
  
 [ *type_schema_name***합니다.** ] *type_name*  
 추가된 열 및 해당 열이 속한 스키마의 데이터 형식입니다.  
  
 *type_name* 될 수 있습니다.  
  
-   A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 별칭 데이터 형식. 별칭 데이터 형식은 테이블 정의에 사용하기 전에 CREATE TYPE을 사용하여 생성되어야 합니다.  
  
-   A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 속해 있는 스키마 및 사용자 정의 형식입니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식은 테이블 정의에 사용하기 전에 CREATE TYPE을 사용하여 생성되어야 합니다.  
  
 경우 *type_schema_name* 를 지정 하지 않으면는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 참조 *type_name* 다음과 같은 순서로:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식  
  
-   현재 데이터베이스에 있는 현재 사용자의 기본 스키마  
  
-   현재 데이터베이스의 **dbo** 스키마  
  
*전체 자릿수*  
 지정된 데이터 형식의 전체 자릿수입니다. 유효한 전체 자릿수 값에 대 한 자세한 내용은 참조 [전체 자릿수, 소수 자릿수 및 길이 &#40; Transact SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
*소수 자릿수*  
 지정된 데이터 형식의 소수 자릿수입니다. 유효한 소수 자릿수 값에 대 한 자세한 내용은 참조 [전체 자릿수, 소수 자릿수 및 길이 &#40; Transact SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
**max**  
 에 적용 됩니다는 **varchar**, **nvarchar**, 및 **varbinary** 데이터 형식입니다. 2^31바이트의 문자 및 이진 데이터와 2^30바이트의 유니코드 데이터를 저장하는 데 사용됩니다.  
  
**콘텐츠**  
 지정의 각 인스턴스는 **xml** 의 데이터 형식이 *column_name* 여러 개의 최상위 요소를 구성 될 수 있습니다. 콘텐츠에만 적용 됩니다는 **xml** 데이터 입력 한 경우에 지정할 수 있습니다 *xml_schema_collection* 도 지정 합니다. 지정되지 않은 경우 기본 동작은 CONTENT입니다.  
  
DOCUMENT  
 지정의 각 인스턴스는 **xml** 의 데이터 형식이 *column_name* 하나의 최상위 요소만 구성 될 수 있습니다. 문서에만 적용 됩니다는 **xml** 데이터 입력 한 경우에 지정할 수 있습니다 *xml_schema_collection* 도 지정 합니다.  
  
 *xml_schema_collection*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 에 적용 됩니다는 **xml** 형식과 XML 스키마 컬렉션을 연결 하기 위한 데이터 형식입니다. 입력 하기 전에 **xml** 스키마에 대 한 열에서 스키마 만들어야 데이터베이스에서 사용 하 여 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)합니다.  
  
FILESTREAM  
 필요에 따라 지정 된 열에 대 한 FILESTREAM 저장소 특성이 *type_name* 의 **varbinary (max)**합니다.  
  
 테이블의 열이 또한 있어야 FILESTREAM 열에 대해을 지정 하는 경우는 **uniqueidentifier** ROWGUIDCOL 특성을 갖는 데이터 형식입니다. 이 열은 Null 값을 허용하지 않으며 UNIQUE 또는 PRIMARY KEY 단일 열 제약 조건을 가져야 합니다. 열의 GUID 값은 응용 프로그램(데이터가 삽입되는 경우)에 의해 또는 NEWID () 함수를 사용하는 DEFAULT 제약 조건에 의해 제공되어야 합니다.  
  
 테이블에 대해 정의된 FILESTREAM 열이 있는 동안에는 ROWGUIDCOL 열을 삭제하고 관련 제약 조건을 변경할 수 없습니다. ROWGUIDCOL 열은 마지막 FILESTREAM 열이 삭제된 이후에만 삭제될 수 있습니다.  
  
 열에 대해 FILESTREAM 저장소 특성이 지정된 경우 해당 열의 모든 값이 파일 시스템에 있는 FILESTREAM 데이터 컨테이너에 저장됩니다.  
  
 열 정의 사용 하는 방법을 보여 주는 예제를 참조 하십시오. [FILESTREAM &#40; SQL Server &#41; ](../../relational-databases/blob/filestream-sql-server.md).  
  
COLLATE *데이터 정렬 이름*  
 열에 대한 데이터 정렬을 지정합니다. 이를 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 목록 및 자세한 정보에 대 한 참조 [Windows 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL Server 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 열에 대해서만 데이터 정렬을 지정할 수는 COLLATE 절을 사용할 수는 **char**, **varchar**, **nchar**, 및 **nvarchar** 데이터 형식 .  
  
 COLLATE 절에 대 한 자세한 내용은 참조 하십시오. [collate&#40; Transact SQL &#41; ](~/t-sql/statements/collations.md).  
  
 NULL | NOT NULL  
 열의 Null 값 허용 여부를 결정합니다. NULL은 엄격하게 말해 제약 조건이 아니지만 NOT NULL처럼 지정할 수 있습니다.  
  
[제약 조건 *constraint_name* ]  
 DEFAULT 값 정의의 시작을 지정합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 DEFAULT에 제약 조건 이름을 할당할 수 있습니다. *constraint_name* 에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)한다는 점을 제외 하는 이름은 #로 시작할 수 없습니다 (#). 경우 *constraint_name* 를 지정 하지 않으면 시스템 생성 이름이 DEFAULT 정의에 할당 됩니다.  
  
DEFAULT  
 열의 기본값을 지정하는 키워드입니다. DEFAULT 정의를 사용하여 기존 데이터 행에 새 열의 값을 제공할 수 있습니다. DEFAULT 정의에 적용할 수 없습니다 **타임 스탬프** 열 또는 IDENTITY 속성이 있는 열입니다. 형식에서의 암시적 변환이 지원 해야 기본 값을 사용자 정의 형식 열에 대해 지정 하는 경우 *constant_expression* 사용자 정의 형식에 있습니다.  
  
*constant_expression*  
 기본 열 값으로 사용되는 리터럴 값, NULL, 시스템 함수입니다. 되도록 정의 된 열과 함께 사용할 경우 한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식 형식 구현에서의 암시적 변환이 지원 해야 합니다는 *constant_expression* 사용자 정의 형식에 있습니다.  
  
WITH VALUES  
 기본 제공 하는 값을 지정 하는 *constant_expression* 기존 행에 추가 하는 새 열에 저장 됩니다. 추가된 열에 null 값을 사용할 수 있고 WITH VALUES가 지정된 경우 기존 행에 추가된 새 열에 기본값이 저장됩니다. Null을 허용 하는 열에 대 한 WITH VALUES를 지정 하지 않으면, NULL 값이 기존 행에 있는 새 열에 저장 됩니다. 새 열이 Null을 허용하지 않으면 WITH VALUES의 지정 여부에 관계없이 새 행에 기본값이 저장됩니다.  
  
IDENTITY  
 새 열이 ID 열임을 지정합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 열에 고유한 증가값을 제공합니다. 기존 테이블에 ID 열을 추가하면 ID 번호가 테이블의 기존 행에 추가되며 초기값과 증가값이 적용됩니다. 행이 업데이트되는 순서는 보장되지 않습니다. 새로 추가한 모든 행에 대한 ID 열도 생성됩니다.  
  
 ID 열은 일반적으로 PRIMARY KEY 제약 조건과 함께 사용되어 테이블의 고유한 행 식별자 역할을 합니다. IDENTITY 속성에 지정할 수는 **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, 또는 **numeric(p,0)** 열입니다. ID 열은 테이블당 하나만 만들 수 있습니다. DEFAULT 키워드 및 바인딩된 기본값은 ID 열에 사용할 수 없습니다. 초기값과 증가값은 모두 지정하거나 둘 다 지정하지 말아야 합니다. 아무 것도 지정하지 않으면 기본값은 (1,1)입니다.  
  
> [!NOTE]  
>  기존 테이블 열을 수정하여 IDENTITY 속성을 추가할 수는 없습니다.  
  
 열이 구독자로 복제될 때 데이터가 일치하지 않을 수 있기 때문에 게시된 테이블에는 ID 열을 추가할 수 없습니다. 게시자의 ID 열 값은 영향을 받는 테이블 행이 실제로 저장된 순서에 따라 달라집니다. 구독자에서는 행이 다르게 저장될 수 있으므로 ID 열의 값이 같은 행에 대해 다를 수 있습니다.  
  
 사용을 명시적으로 삽입할 값을 허용 하 여 열의 IDENTITY 속성 사용 하지 않으려면 [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)합니다.  
  
*시드*  
 테이블에 로드된 첫 번째 행에 사용되는 값입니다.  
  
*증가값*  
 이전에 로드된 행의 ID 값에 더해지는 증가 값입니다.  
  
NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 IDENTITY 속성에 지정할 수 있습니다. 이 절이 IDENTITY 속성에 지정된 경우 복제 에이전트가 삽입 작업을 수행할 때 ID 열의 값이 증가하지 않습니다.  
  
ROWGUIDCOL  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 열이 ROWGUIDCOL(행 전역 고유 식별자 열)인지 여부를 지정합니다. ROWGUIDCOL에만 할당할 수는 **uniqueidentifier** 열 및 하나에만 **uniqueidentifier** 테이블당 열 ROWGUIDCOL 열으로 지정 될 수 있습니다. ROWGUIDCOL은 사용자 정의 데이터 형식의 열에 할당할 수 없습니다.  
  
 ROWGUIDCOL로 인해 열에 저장된 값이 고유하도록 설정되거나 테이블에 삽입된 새 행에 대한 값을 자동으로 생성하지 않습니다. 각 열에 대해 고유한 값을 생성하려면 INSERT 문에 NEWID 함수를 사용하거나 NEWID 함수를 열의 기본값으로 지정합니다. 자세한 내용은 참조 [NEWID &#40; Transact SQL &#41; ](../../t-sql/functions/newid-transact-sql.md)및 [insert&#40; Transact SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
SPARSE  
 열이 스파스 열임을 나타냅니다. 스파스 열의 저장소는 Null 값에 대해 최적화됩니다. 스파스 열은 NOT NULL로 지정할 수 없습니다. 추가 제한 사항 및 스파스 열에 대 한 자세한 내용은 참조 [스파스 열을 사용 하 여](../../relational-databases/tables/use-sparse-columns.md)합니다.  
  
\<column_constraint >  
 열 제약 조건 인수 정의 대 한 참조 [column_constraint &#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-column-constraint-transact-sql.md).  
  
 사용 하 여 암호화  
 암호화 열을 사용 하 여 지정 된 [항상 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능입니다.  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 열 암호화 키를 지정합니다. 자세한 내용은 참조 [열 암호화 키 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
ENCRYPTION_TYPE = {결정적 | 임의}  
 **결정적 암호화** 는 지정된 일반 텍스트 값에 대해 항상 동일한 암호화된 값을 생성하는 방법을 사용합니다. 결정적 암호화를 사용 하 여 같음 비교를 암호화 된 값을 기반으로 동등 조인을 사용 하 여 테이블 조인 및 그룹화를 사용 하 여 검색을 허용 하지만 패턴을 검사 하 여 암호화 된 값에 대 한 정보를 추측할 권한이 없는 사용자가 사용할 수 있습니다. 암호화 된 열입니다. 명확 하 게 암호화 된 열에서 두 테이블을 조인는 두 열은 동일한 열 암호화 키를 사용 하 여 암호화 하는 경우에 가능 합니다. 결정적 암호화에서는 문자 열에 대해 binary2 정렬 순서를 적용하는 열 데이터 정렬을 사용해야 합니다.  
  
 **임의 암호화** 는 예측하기 어려운 방식으로 데이터를 암호화하는 방법을 사용합니다. 임의 암호화는 더 안전 하지만 동등 검색, 그룹화 및 암호화 된 열에서 조인를 금지 합니다. 임의 암호화를 사용 하 여 열을 인덱싱할 수 없습니다.  
  
 한 열을 검색 매개 변수 또는 그룹화 매개 변수를 예: 정부 ID 번호에 대 한 결정적 암호화를 사용 합니다. 임의 암호화를 사용 하 여, 신용 카드 번호 등 데이터용 하지 다른 레코드와 같은 그룹에 있거나, 테이블과 조인 하는 검색 되지 않습니다에 대 한 암호화 된 포함 된 행을 찾습니다 (예: transaction number) 다른 열을 사용 하는 데 사용 관심 있는 열입니다.  
  
 조건에 맞는 데이터 형식의 열 이어야 합니다.  
  
알고리즘  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
해야 **'AEAD_AES_256_CBC_HMAC_SHA_256'**합니다.  
  
 기능 제약 조건을 비롯 한 자세한 내용은 참조 하십시오. [상시 암호화 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)합니다.  
  
   
와 마스킹된 추가 (함수 = ' *mask_function* ')  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
 동적 데이터 마스크를 지정합니다. *mask_function* 적절 한 매개 변수를 사용 하 여 마스킹 함수 이름입니다. 다음 함수를 사용할 수 있습니다.  
  
-   default)  
  
-   email()  
  
-   partial()  
  
-   random()  
  
 함수 매개 변수를 참조 하십시오. [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)합니다.  
  
## <a name="remarks"></a>주의  
 열이 있는 추가 하는 경우는 **uniqueidentifier** 데이터 형식으로 정의할 수 있습니다 newid () 함수를 사용 하 여 테이블의 각 기존 행에 대 한 새 열에 고유한 식별자 값을 제공 하는 기본값입니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 열 정의에 DEFAULT, IDENTITY, ROWGUIDCOL 또는 열 제약 조건을 순서에 관계없이 지정할 수 있습니다.  
  
 열을 추가하여 데이터 행 크기가 8060바이트를 초과하면 ALTER TABLE 문이 실패합니다.  
  
## <a name="examples"></a>예  
 예제를 보려면 [ALTER table&#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  

