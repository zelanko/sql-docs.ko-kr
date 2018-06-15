---
title: computed_column_definition(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
ms.assetid: 746eabda-3b4f-4940-b0b5-1c379f5cf7a5
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 00ed2233653ea5a98fdc389bbfc470f65c817f3f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33073800"
---
# <a name="alter-table-computedcolumndefinition-transact-sql"></a>ALTER TABLE computed_column_definition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 사용하여 테이블에 추가되는 계산 열의 속성을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
column_name AS computed_column_expression  
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [ WITH FILLFACTOR = fillfactor ]  
        [ WITH ( <index_option> [, ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ) | filegroup   
            | "default" } ]  
    | [ FOREIGN KEY ]   
        REFERENCES ref_table [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
]  
```  
  
## <a name="arguments"></a>인수  
*column_name*  
 변경, 추가 또는 삭제할 열의 이름입니다. *column_name*은 1~128자의 문자를 포함할 수 있습니다. 새 열의 경우 **타임스탬프** 데이터 형식으로 만들어진 열에 대해 *column_name*을 생략할 수 있습니다. **타임스탬프** 데이터 형식 열에 대해 *column_name*이 지정되지 않으면 **타임스탬프**가 이름으로 사용됩니다.  
  
*computed_column_expression*  
 계산 열의 값을 정의하는 식입니다. 계산 열은 테이블에 물리적으로 저장된 열이 아니라 해당 테이블의 다른 열을 사용하여 식으로 계산된 가상의 열입니다. 예를 들어 계산 열은 cost AS price * qty 정의를 가질 수 있습니다. 식은 계산되지 않은 열 이름, 상수, 함수, 변수 및 이러한 요소를 하나 이상의 연산자로 연결한 조합이 될 수 있습니다. 식은 하위 쿼리가 될 수 없으며 별칭 데이터 형식을 포함할 수 없습니다.  
  
 다음과 같은 경우를 제외하면 SELECT 목록, WHERE 절, ORDER BY 절 및 정규식이 사용되는 모든 위치에 계산 열을 사용할 수 있습니다.  
  
-   계산 열은 DEFAULT 또는 FOREIGN KEY 제약 조건 정의로 사용하거나 NOT NULL 제약 조건 정의와 함께 사용할 수 없습니다. 그러나 계산 열 값이 명확한 식에 의해 정의되고 결과의 데이터 형식이 인덱스 열에 허용되는 경우에는 계산 열을 인덱스의 키 열이나 PRIMARY KEY 또는 UNIQUE 제약 조건의 일부로 사용할 수 있습니다.  
  
     예를 들어 테이블에 a와 b라는 정수 열이 있을 때 계산 열 a + b에는 인덱스를 작성할 수 있지만 계산 열 a+DATEPART(dd, GETDATE())는 다음 호출 시 값이 바뀌므로 인덱스를 작성할 수 없습니다.  
  
-   계산 열은 INSERT 또는 UPDATE 문의 대상이 될 수 없습니다.  
  
    > [!NOTE]  
    >  계산 열과 관련된 테이블의 각 행은 서로 다른 값을 가질 수 있으므로 계산 열은 각 행에 대해 동일한 결과를 갖지 않을 수도 있습니다.  
  
PERSISTED  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 계산된 값을 테이블에 물리적으로 저장하고 계산 열이 종속된 다른 열이 업데이트되면 해당 값을 업데이트하도록 지정합니다. 계산 열을 PERSISTED로 표시하면 결정적이지만 정확하지 않은 계산 열에 대해 인덱스를 만들 수 있습니다. 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요. 분할된 테이블의 분할 열로 사용되는 계산 열은 명시적으로 PERSISTED로 표시되어야 합니다. PERSISTED를 지정할 때 *computed_column_expression*은 결정적이어야 합니다. 

NULL | NOT NULL  
 열의 Null 값 허용 여부를 지정합니다. NULL은 엄격하게 말해 제약 조건이 아니지만 NOT NULL과 같이 지정할 수 있습니다. 계산 열에서는 PERSISTED를 지정한 경우에만 NOT NULL을 지정할 수 있습니다.  
  
CONSTRAINT  
 PRIMARY KEY 또는 UNIQUE 제약 조건 정의의 시작을 지정합니다.  
  
*constraint_name*  
 새 제약 조건입니다. 제약 조건 이름은 [identifiers](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 하지만 숫자 기호(#)로 시작될 수 없습니다. *constraint_name*을 지정하지 않으면 시스템에서 생성한 이름이 제약 조건에 할당됩니다.  
  
PRIMARY KEY  
 지정한 열에 대해 고유 인덱스를 사용하여 엔터티 무결성을 적용하는 제약 조건입니다. PRIMARY KEY 제약 조건은 테이블마다 한 개씩만 만들 수 있습니다.  
  
UNIQUE  
 고유 인덱스를 사용하여 지정한 열에 엔터티 무결성을 제공하는 제약 조건입니다.  
  
CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 인덱스나 비클러스터형 인덱스를 만들도록 지정합니다. PRIMARY KEY 제약 조건의 기본값은 CLUSTERED입니다. UNIQUE 제약 조건의 기본값은 NONCLUSTERED입니다.  
  
 테이블에 클러스터형 제약 조건이나 인덱스가 이미 있으면 CLUSTERED를 지정할 수 없습니다. 이 경우 PRIMARY KEY 제약 조건은 기본적으로 NONCLUSTERED로 설정됩니다.  
  
WITH FILLFACTOR =*fillfactor*  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 인덱스 데이터를 저장하는 데 사용되는 각 인덱스 페이지를 채우는 정도를 지정합니다. 사용자가 지정한 *fillfactor* 값은 1에서 100 사이일 수 있습니다. 값을 지정하지 않으면 기본값 0이 사용됩니다.  
  
> [!IMPORTANT]  
>  현재 WITH FILLFACTOR = *fillfactor*가 PRIMARY KEY 또는 UNIQUE 제약 조건에 적용되는 유일한 인덱스 옵션으로 기술되어 있는 것은 이전 버전과의 호환성을 위한 것이며 이후 릴리스에서는 이런 식으로 기술되지 않을 것입니다. ALTER TABLE의 [index_option &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md) 절에 다른 인덱스 옵션을 지정할 수 있습니다.  
  
FOREIGN KEY REFERENCES  
 열에 있는 데이터에 대한 참조 무결성을 제공하는 제약 조건입니다. FOREIGN KEY 제약 조건을 지정하려면 열의 각 값이 참조된 테이블의 참조된 해당 열에 있어야 합니다. FOREIGN KEY 제약 조건은 참조되는 테이블의 PRIMARY KEY 또는 UNIQUE 제약 조건 열이나 참조되는 테이블의 UNIQUE INDEX에서 참조되는 열만 참조할 수 있습니다. 계산 열의 외래 키 또한 PERSISTED로 표시되어야 합니다.  
  
*ref_table*  
 FOREIGN KEY 제약 조건이 참조하는 테이블의 이름입니다.  
  
(*ref_column* )  
 FOREIGN KEY 제약 조건이 참조하는 테이블의 열입니다.  
  
ON DELETE { **NO ACTION** | CASCADE }  
 행에 참조 관계가 있고 참조되는 행이 부모 테이블에서 삭제될 경우 테이블의 행에 수행될 동작을 지정합니다. 기본값은 NO ACTION입니다.  
  
NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 삭제 동작이 롤백됩니다.

CASCADE  
 부모 테이블에서 행을 삭제한 경우 참조 테이블에서 해당 행이 삭제됩니다.  
  
 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 ProductVendor 테이블은 Vendor 테이블과 참조 관계를 갖습니다. ProductVendor.BusinessEntityID 외래 키는 Vendor.BusinessEntityID 기본 키를 참조합니다.  
  
 Vendor 테이블의 행에 대해 DELETE 문을 실행하고 ProductVendor.BusinessEntityID에 대해 ON DELETE CASCADE 동작을 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 ProductVendor 테이블에서 하나 이상의 종속 행이 있는지 확인합니다. ProductVendor 테이블에 종속 행이 있는 경우 삭제되며 Vendor 테이블에서 참조된 행도 삭제됩니다.  
  
 반대로 NO ACTION을 지정한 경우 ProductVendor 테이블에 Vendor 행을 참조하는 행이 하나 이상 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생하고 Vendor 행의 삭제 동작이 롤백됩니다.  
  
 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
ON UPDATE { **NO ACTION** }  
 만들어진 테이블의 행에 참조 관계가 있고 참조된 행이 부모 테이블에서 업데이트될 경우 해당 행에 적용될 동작을 지정합니다. NO ACTION을 지정한 경우 ProductVendor 테이블에 Vendor 행을 참조하는 행이 하나 이상 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생하고 Vendor 행의 업데이트 동작이 롤백됩니다.  
  
NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 FOREIGN KEY 제약 조건 및 CHECK 제약 조건에 대해 지정할 수 있습니다. 제약 조건에 대해 이 절을 지정하면 복제 에이전트가 삽입, 업데이트 또는 삭제 작업을 수행할 때 해당 제약 조건이 강제로 적용되지 않습니다.  
  
CHECK  
 열에 입력 가능한 값을 제한하여 도메인 무결성을 적용하는 제약 조건입니다. 계산 열의 CHECK 제약 조건 또한 PERSISTED로 표시되어야 합니다.  
  
*logical_expression*  
 TRUE 또는 FALSE를 반환하는 논리 식입니다. 이 식은 별칭 데이터 형식에 대한 참조를 포함할 수 없습니다.  
  
ON { *partition_scheme_name*(*partition_column_name*) | *filegroup*| "default"}  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 제약 조건에 대해 만들어진 인덱스의 저장 위치를 지정합니다. *partition_scheme_name*을 지정하면 인덱스가 분할되고 파티션이 *partition_scheme_name*으로 지정된 파일 그룹에 매핑됩니다. *filegroup*을 지정하면 명명된 파일 그룹에 인덱스가 생성됩니다. "default"를 지정하거나 ON을 지정하지 않으면 테이블이 있는 동일한 파일 그룹에 인덱스가 생성됩니다. PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 인덱스를 추가할 때 ON을 지정하면 클러스터형 인덱스가 생성될 때 전체 테이블이 지정한 파일 그룹으로 이동됩니다.  
  
> [!NOTE]  
>  이 컨텍스트에서 default는 키워드가 아니라 이것은 기본 파일 그룹에 대한 식별자이며 ON "default" 또는 ON [default]와 같이 구분되어야 합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 각 PRIMARY KEY 및 UNIQUE 제약 조건은 인덱스를 생성합니다. UNIQUE 및 PRIMARY KEY 제약 조건의 수가 많아도 테이블의 비클러스터형 인덱스는 999개, 클러스터형 인덱스는 1개를 초과할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
