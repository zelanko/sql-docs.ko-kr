---
title: column_definition(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eb3802578b7eb500d6b5fd64725a1a03f86fb9c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68232150"
---
# <a name="alter-table-column_definition-transact-sql"></a>ALTER TABLE column_definition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 사용하여 테이블에 추가된 열의 속성을 지정합니다.  
  
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
 변경, 추가 또는 삭제할 열의 이름입니다. *column_name*은 1~128자로 구성될 수 있습니다. 새 열의 경우 타임스탬프 데이터 형식으로 만들어진 *column_name*을 생략할 수 있습니다. **타임스탬프** 데이터 형식 열에 대해 *column_name*이 지정되지 않으면 **타임스탬프**가 이름으로 사용됩니다.  
  
 [ _type_schema_name_ **.** ] *type_name*  
 추가된 열 및 해당 열이 속한 스키마의 데이터 형식입니다.  
  
 *type_name*은 다음과 같을 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 별칭 데이터 형식. 별칭 데이터 형식은 테이블 정의에 사용하기 전에 CREATE TYPE을 사용하여 생성되어야 합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식 및 이 형식이 속한 스키마. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식은 테이블 정의에 사용하기 전에 CREATE TYPE을 사용하여 생성되어야 합니다.  
  
 *type_schema_name*을 지정하지 않으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 다음 순서로 *type_name*을 참조합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식  
  
-   현재 데이터베이스에 있는 현재 사용자의 기본 스키마  
  
-   현재 데이터베이스의 **dbo** 스키마  
  
*전체 자릿수*  
 지정된 데이터 형식의 전체 자릿수입니다. 유효한 전체 자릿수 값에 대한 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
*scale*  
 지정된 데이터 형식의 소수 자릿수입니다. 유효한 소수 자릿수 값에 대한 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
**max**  
 **varchar**, **nvarchar** 및 **varbinary** 데이터 유형에만 적용됩니다. 2^31바이트의 문자 및 이진 데이터와 2^30바이트의 유니코드 데이터를 저장하는 데 사용됩니다.  
  
**CONTENT**  
 *column_name*에 있는 **xml** 데이터 형식의 각 인스턴스가 여러 개의 최상위 요소를 포함할 수 있도록 지정합니다. CONTENT는 **xml** 데이터 형식에만 적용되며 *xml_schema_collection*도 지정한 경우에만 지정할 수 있습니다. 지정되지 않은 경우 기본 동작은 CONTENT입니다.  
  
DOCUMENT  
 *column_name*에 있는 **xml** 데이터 형식의 각 인스턴스가 최상위 요소를 하나만 포함할 수 있도록 지정합니다. DOCUMENT는 **xml** 데이터 형식에만 적용되며 *xml_schema_collection*도 지정한 경우에만 지정할 수 있습니다.  
  
 *xml_schema_collection*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 XML 스키마 컬렉션과의 연결을 위해 **xml** 데이터 형식에만 적용됩니다. 스키마에 **xml** 열을 입력하기 전에 먼저 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)을 사용하여 데이터베이스에 해당 스키마를 만들어야 합니다.  
  
FILESTREAM  
 선택적으로 **varbinary(max)** 의 *type_name*인 열에 대해 FILESTREAM 스토리지 특성을 지정합니다.  
  
 열에 대해 FILESTREAM이 지정된 경우 ROWGUIDCOL 특성을 갖는 **uniqueidentifier** 데이터 형식의 열도 테이블에 있어야 합니다. 이 열은 Null 값을 허용하지 않으며 UNIQUE 또는 PRIMARY KEY 단일 열 제약 조건을 가져야 합니다. 열의 GUID 값은 애플리케이션(데이터가 삽입되는 경우)에 의해 또는 NEWID () 함수를 사용하는 DEFAULT 제약 조건에 의해 제공되어야 합니다.  
  
 테이블에 대해 정의된 FILESTREAM 열이 있는 동안에는 ROWGUIDCOL 열을 삭제하고 관련 제약 조건을 변경할 수 없습니다. ROWGUIDCOL 열은 마지막 FILESTREAM 열이 삭제된 이후에만 삭제될 수 있습니다.  
  
 열에 대해 FILESTREAM 스토리지 특성이 지정된 경우 해당 열의 모든 값이 파일 시스템에 있는 FILESTREAM 데이터 컨테이너에 저장됩니다.  
  
 열 정의 사용 방법을 보여 주는 예는 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)를 참조하세요.  
  
COLLATE *collation_name*  
 열에 대한 데이터 정렬을 지정합니다. 이를 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 목록 및 자세한 내용은 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)을 참조하세요.  
  
 COLLATE 절은 **char**, **varchar**, **nchar** 및 **nvarchar** 데이터 형식의 열에 데이터 정렬을 지정하는 데만 사용할 수 있습니다.  
  
 COLLATE 절에 대한 자세한 내용은 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)을 참조하세요.  
  
 NULL | NOT NULL  
 열의 Null 값 허용 여부를 결정합니다. NULL은 엄격하게 말해 제약 조건이 아니지만 NOT NULL처럼 지정할 수 있습니다.  
  
[ CONSTRAINT *constraint_name* ]  
 DEFAULT 값 정의의 시작을 지정합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 DEFAULT에 제약 조건 이름을 할당할 수 있습니다. *constraint_name*은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 하지만 숫자 기호(#)로 시작될 수 없습니다. *constraint_name*을 지정하지 않으면 시스템 생성 이름이 DEFAULT 정의에 할당됩니다.  
  
DEFAULT  
 열의 기본값을 지정하는 키워드입니다. DEFAULT 정의를 사용하여 기존 데이터 행에 새 열의 값을 제공할 수 있습니다. DEFAULT 정의는 **timestamp** 열 또는 IDENTITY 속성이 있는 열에는 적용할 수 없습니다. 사용자 정의 형식 열에 대해 기본값을 지정할 경우 *constant_expression*에서 해당 사용자 정의 형식으로 암시적으로 변환할 수 있어야 합니다.  
  
*constant_expression*  
 기본 열 값으로 사용되는 리터럴 값, NULL, 시스템 함수입니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 유형으로 정의된 열과 함께 사용할 경우 *constant_expression*에서 사용자 정의 유형으로의 암시적 변환이 지원되어야 합니다.  
  
WITH VALUES   
 열 및 DEFAULT 제약 조건을 추가할 때 열에서 NULLS를 허용하는 경우 기존 행에 WITH VALUES를 사용하면 새 열의 값이 DEFAULT *constant_expression*에 제공된 값으로 설정됩니다. 추가되는 열에서 NULLS를 허용하지 않으면 기존 행의 열 값은 항상 DEFAULT *constant expression*에 제공된 값으로 설정됩니다. SQL Server 2012부터 이 작업은 메타데이터 작업 [온라인 작업으로 null 열을 추가하지 않음](alter-table-transact-sql.md?view=sql-server-2017#adding-not-null-columns-as-an-online-operation)입니다.
관련 열이 추가되지 않을 때 이 작업이 사용되면 아무런 영향을 주지 않습니다.
 
 DEFAULT *constant_expression*에 지정된 값이 기존 행에 추가된 새 열에 저장되도록 지정합니다. 추가된 열이 Null 값을 허용하고 WITH VALUES가 지정된 경우 기존 행에 추가된 새 열에 기본값이 저장됩니다. Null을 허용하는 열에 WITH VALUES를 지정하지 않으면 NULL 값은 기존 행의 새 열에 저장됩니다. 새 열이 Null을 허용하지 않으면 WITH VALUES의 지정 여부에 관계없이 새 행에 기본값이 저장됩니다.  
  
IDENTITY  
 새 열이 ID 열임을 지정합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 열에 고유한 증가값을 제공합니다. 기존 테이블에 ID 열을 추가하면 ID 번호가 테이블의 기존 행에 추가되며 초기값과 증가값이 적용됩니다. 행이 업데이트되는 순서는 보장되지 않습니다. 새로 추가한 모든 행에 대한 ID 열도 생성됩니다.  
  
 ID 열은 일반적으로 PRIMARY KEY 제약 조건과 함께 사용되어 테이블의 고유한 행 식별자 역할을 합니다. IDENTITY 속성은 **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** 또는 **numeric(p,0)** 열에 할당할 수 있습니다. ID 열은 테이블당 하나만 만들 수 있습니다. DEFAULT 키워드 및 바인딩된 기본값은 ID 열에 사용할 수 없습니다. 초기값과 증가값은 모두 지정하거나 둘 다 지정하지 말아야 합니다. 아무 것도 지정하지 않으면 기본값은 (1,1)입니다.  
  
> [!NOTE]  
>  기존 테이블 열을 수정하여 IDENTITY 속성을 추가할 수는 없습니다.  
  
 열이 구독자로 복제될 때 데이터가 일치하지 않을 수 있기 때문에 게시된 테이블에는 ID 열을 추가할 수 없습니다. 게시자의 ID 열 값은 영향을 받는 테이블 행이 실제로 저장된 순서에 따라 달라집니다. 구독자에서는 행이 다르게 저장될 수 있으므로 ID 열의 값이 같은 행에 대해 다를 수 있습니다.  
  
 값을 명시적으로 삽입할 수 있도록 허용하여 열의 IDENTITY 속성을 해제하려면 [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)를 사용하세요.  
  
*seed*  
 테이블에 로드된 첫 번째 행에 사용되는 값입니다.  
  
*increment*  
 이전에 로드된 행의 ID 값에 더해지는 증가 값입니다.  
  
NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 IDENTITY 속성에 지정할 수 있습니다. 이 절이 IDENTITY 속성에 지정된 경우 복제 에이전트가 삽입 작업을 수행할 때 ID 열의 값이 증가하지 않습니다.  
  
ROWGUIDCOL  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 열이 ROWGUIDCOL(행 전역 고유 식별자 열)인지 여부를 지정합니다. ROWGUIDCOL은 **uniqueidentifier** 열에만 할당될 수 있고 한 테이블당 한 개의 **uniqueidentifier** 열만 ROWGUIDCOL 열로 지정할 수 있습니다. ROWGUIDCOL은 사용자 정의 데이터 형식의 열에 할당할 수 없습니다.  
  
 ROWGUIDCOL로 인해 열에 저장된 값이 고유하도록 설정되거나 테이블에 삽입된 새 행에 대한 값을 자동으로 생성하지 않습니다. 각 열에 대해 고유한 값을 생성하려면 INSERT 문에 NEWID 함수를 사용하거나 NEWID 함수를 열의 기본값으로 지정합니다. 자세한 내용은 [NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md) 및 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)를 참조하세요.  
  
SPARSE  
 열이 스파스 열임을 나타냅니다. 스파스 열의 스토리지는 Null 값에 대해 최적화됩니다. 스파스 열은 NOT NULL로 지정할 수 없습니다. 추가 제한 사항 및 스파스 열에 대한 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.  
  
\<column_constraint>  
 열 제약 조건 인수에 대한 정의는 [column_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)을 참조하세요.  
  
 ENCRYPTED WITH  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능을 사용하여 열 암호화를 지정합니다.  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 열 암호화 키를 지정합니다. 자세한 내용은 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)을 참조하세요.  
  
ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED }  
 **결정적 암호화** 는 지정된 일반 텍스트 값에 대해 항상 동일한 암호화된 값을 생성하는 방법을 사용합니다. 결정적 암호화를 사용하면 암호화된 값을 기반으로 같음 비교를 이용한 검색, 그룹화 및 같음 조인을 이용한 조인이 가능하지만, 권한이 없는 사용자가 암호화된 열의 패턴을 검사하여 암호화된 값에 관한 정보를 추측할 수도 있습니다. 결정적으로 암호화된 열의 두 테이블 조인은 두 열이 모두 같은 열 암호화 키를 사용하여 암호화된 경우에만 가능합니다. 결정적 암호화에서는 문자 열에 대해 binary2 정렬 순서를 적용하는 열 데이터 정렬을 사용해야 합니다.  
  
 **임의 암호화** 는 예측하기 어려운 방식으로 데이터를 암호화하는 방법을 사용합니다. 임의 암호화는 좀 더 안전하지만 SQL Server 인스턴스가 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 지원하지 않으면, 암호화된 열에서 계산 및 인덱싱을 수행할 수 없습니다.
  
 Always Encrypted(보안 Enclave를 사용하지 않음)를 사용할 경우 매개 변수 또는 그룹화 매개 변수(예: 정부 ID 번호)를 사용하여 검색할 열에 대해 결정적 암호화를 사용합니다. 다른 레코드와 함께 그룹화되지 않거나 테이블을 조인하는 데 사용되고 관심이 있는 암호화된 열을 포함한 행을 찾는 데에는 다른 열(거래 번호 등)을 사용하기 때문에 검색되지 않는 데이터(예: 신용 카드 번호)에 임의 암호화를 사용합니다.  

 보안 Enclave에서 Always Encrypted를 사용할 경우 임의 암호화가 권장되는 암호화 유형입니다.  
  
 열은 한정 데이터 형식이어야 합니다.  
  
ALGORITHM  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]까지  
**'AEAD_AES_256_CBC_HMAC_SHA_256'** 이어야 합니다.  
  
 기능 제약 조건을 포함한 자세한 내용은 [Always Encrypted &#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)을 참조하세요.  
  
   
ADD MASKED WITH ( FUNCTION = ' *mask_function* ')  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 동적 데이터 마스크를 지정합니다. *mask_function*은 적절한 매개 변수를 포함한 마스킹 함수의 이름입니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
-   default()  
  
-   email()  
  
-   partial()  
  
-   random()  
  
 함수 매개 변수에 대해서는 [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 **uniqueidentifier** 데이터 형식의 열이 추가되면 NEWID() 함수를 기본으로 사용하도록 하여 테이블의 기존 행에 새 열이 추가될 때 고유한 ID 값을 제공하도록 할 수 있습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 열 정의에 DEFAULT, IDENTITY, ROWGUIDCOL 또는 열 제약 조건을 순서에 관계없이 지정할 수 있습니다.  
  
 열을 추가하여 데이터 행 크기가 8060바이트를 초과하면 ALTER TABLE 문이 실패합니다.  
  
## <a name="examples"></a>예  
 예제는 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
