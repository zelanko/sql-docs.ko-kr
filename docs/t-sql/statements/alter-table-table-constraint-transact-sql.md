---
description: ALTER TABLE table_constraint(Transact-SQL)
title: table_constraint(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9597b6c0811ff2fe917a2282b43e677b74eebd4f
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97490073"
---
# <a name="alter-table-table_constraint-transact-sql"></a>ALTER TABLE table_constraint(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 사용하여 테이블에 추가한 PRIMARY KEY, UNIQUE, FOREIGN KEY, CHECK 제약 조건이나 DEFAULT 정의의 속성을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CONNECTION
        ( { node_table TO node_table } 
          [ , {node_table TO node_table }]
          [ , ...n ]
        )
        [ ON DELETE { NO ACTION | CASCADE } ]
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 CONSTRAINT  
 PRIMARY KEY, UNIQUE, FOREIGN KEY 또는 CHECK 제약 조건이나 DEFAULT에 대한 정의의 시작을 지정합니다.  
  
 *constraint_name*  
 제약 조건의 이름입니다. 제약 조건 이름은 [identifiers](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 하지만 숫자 기호(#)로 시작될 수 없습니다. constraint_name을 지정하지 않으면 시스템에서 생성한 이름이 제약 조건에 할당됩니다.  
  
 PRIMARY KEY  
 지정한 열에 대해 고유 인덱스를 사용하여 엔터티 무결성을 적용하는 제약 조건입니다. PRIMARY KEY 제약 조건은 테이블마다 한 개씩만 만들 수 있습니다.  
  
 UNIQUE  
 지정한 열에 대해 고유 인덱스를 사용하여 엔터티 무결성을 제공하는 제약 조건입니다.  
  
 CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 인덱스나 비클러스터형 인덱스를 만들도록 지정합니다. PRIMARY KEY 제약 조건의 기본값은 CLUSTERED입니다. UNIQUE 제약 조건의 기본값은 NONCLUSTERED입니다.  
  
 테이블에 클러스터형 제약 조건이나 인덱스가 이미 있으면 CLUSTERED를 지정할 수 없습니다. 이 경우 PRIMARY KEY 제약 조건은 기본적으로 NONCLUSTERED로 설정됩니다.  
  
 데이터 형식이 **ntext**, **text**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml** 또는 **image** 인 열은 인덱스의 열로 지정할 수 없습니다.  
  
 *column*  
 새 제약 조건에 사용되는 열 또는 열 목록을 괄호 안에 지정합니다.  
  
 [ **ASC** | DESC ]  
 테이블 제약 조건에 사용되는 열의 정렬 순서를 지정합니다. 기본값은 ASC입니다.  
  
 WITH FILLFACTOR **=** _fillfactor_  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 인덱스 데이터를 저장하는 데 사용되는 각 인덱스 페이지를 채우는 정도를 지정합니다. 사용자가 지정한 *fillfactor* 값은 1에서 100 사이일 수 있습니다. 값을 지정하지 않으면 기본값 0이 사용됩니다.  
  
> [!IMPORTANT]  
>  현재 WITH FILLFACTOR = *fillfactor* 가 PRIMARY KEY 또는 UNIQUE 제약 조건에 적용되는 유일한 인덱스 옵션으로 기술되어 있는 것은 이전 버전과의 호환성을 위한 것이며 이후 릴리스에서는 이런 식으로 기술되지 않을 것입니다. ALTER TABLE의 [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) 절에 다른 인덱스 옵션을 지정할 수 있습니다.  
  
 ON { _partition\_scheme\_name_ **(** _partition\_column\_name_ **)**  | _filegroup_|  **"** default **"** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 제약 조건에 대해 만들어진 인덱스의 스토리지 위치를 지정합니다. *partition_scheme_name* 을 지정하면 인덱스가 분할되고 파티션이 *partition_scheme_name* 으로 지정된 파일 그룹에 매핑됩니다. *filegroup* 을 지정하면 명명된 파일 그룹에 인덱스가 생성됩니다. **"** default **"** 를 지정하거나, ON을 지정하지 않으면 테이블이 있는 동일한 파일 그룹에 인덱스가 생성됩니다. PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 인덱스를 추가할 때 ON을 지정하면 클러스터형 인덱스가 생성될 때 전체 테이블이 지정한 파일 그룹으로 이동됩니다.  
  
 이 컨텍스트에서 기본값은 키워드가 아니라 기본 파일 그룹에 대한 식별자이며 ON **"** default **"** 또는 ON **[** default **]** 와 같이 구분해야 합니다. **"** default **"** 를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다.  
  
 FOREIGN KEY REFERENCES  
 특정 열의 데이터에 대한 참조 무결성을 제공하는 제약 조건입니다. FOREIGN KEY 제약 조건을 지정하려면 해당 열의 각 값이 참조되는 테이블의 지정한 열에 있어야 합니다.  
  
 *referenced_table_name*  
 FOREIGN KEY 제약 조건에 의해 참조되는 테이블입니다.  
  
 *ref_column*  
 새 FOREIGN KEY 제약 조건에 의해 참조되는 열 또는 열 목록을 괄호 안에 표시합니다.  
  
 ON DELETE { **NO ACTION** \| CASCADE \| SET NULL \| SET DEFAULT }  
 행에 참조 관계가 있고 참조되는 행이 부모 테이블에서 삭제될 경우 변경된 테이블의 행에 수행될 동작을 지정합니다. 기본값은 NO ACTION입니다.  
  
 NO ACTION  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 삭제 동작이 롤백됩니다.  
  
 CASCADE  
 부모 테이블에서 행을 삭제한 경우 참조 테이블에서 해당 행이 삭제됩니다.  
  
 SET NULL  
 부모 테이블에서 행을 삭제하면 해당 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다.  
  
 SET DEFAULT  
 부모 테이블에서 행을 삭제하면 해당 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적으로 설정된 기본값이 없을 경우 열의 암시적 기본값은 NULL이 됩니다.  
  
 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
 변경할 테이블에 INSTEAD OF 트리거 ON DELETE가 이미 있으면 ON DELETE CASCADE를 정의할 수 없습니다.  
  
 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 **ProductVendor** 테이블은 **Vendor** 테이블과 참조 관계를 갖습니다. **ProductVendor.VendorID** 외래 키는 **Vendor.VendorID** 기본 키를 참조합니다.  
  
 **Vendor** 테이블의 행에 대해 DELETE 문을 실행하고 **ProductVendor.VendorID** 에 대해 ON DELETE CASCADE 동작을 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 **ProductVendor** 테이블에 하나 이상의 종속 행이 있는지 확인합니다. **ProductVendor** 테이블에 종속 행이 있는 경우 삭제되며 **Vendor** 테이블에서 참조된 행도 삭제됩니다.  
  
 반대로 NO ACTION을 지정한 경우 **ProductVendor** 테이블에 **Vendor** 행을 참조하는 행이 하나 이상 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생하고 참조된 행의 삭제 동작이 롤백됩니다.  
  
 ON UPDATE { **NO ACTION** \| CASCADE \| SET NULL \| SET DEFAULT }  
 변경된 테이블의 행에 참조 관계가 있고 참조된 행이 부모 테이블에서 업데이트될 경우 해당 행에 대해 발생할 동작을 지정합니다. 기본값은 NO ACTION입니다.  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 업데이트 동작이 롤백됩니다.  
  
 CASCADE  
 부모 테이블에서 행이 업데이트될 때 참조 테이블에서도 해당 행이 업데이트됩니다.  
  
 SET NULL  
 부모 테이블에서 행을 업데이트하면 해당 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다.  
  
 SET DEFAULT  
 부모 테이블에서 행을 업데이트하면 해당 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적 기본값이 설정되어 있지 않은 경우 NULL은 해당 열의 암시적 기본값이 됩니다.  
  
 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
 변경할 테이블에 INSTEAD OF 트리거 ON UPDATE가 이미 존재하면 ON UPDATE CASCADE, SET NULL 또는 SET DEFAULT를 정의할 수 없습니다.  
  
 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 **ProductVendor** 테이블은 **Vendor** 테이블과 참조 관계를 갖습니다. **ProductVendor.VendorID** 외래 키는 **Vendor.VendorID** 기본 키를 참조합니다.  
  
 **Vendor** 테이블의 행에 대해 UPDATE 문을 실행하고 **ProductVendor.VendorID** 에 대해 ON UPDATE CASCADE 동작을 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]는 **ProductVendor** 테이블에 하나 이상의 종속 행이 있는지 확인합니다. **ProductVendor** 테이블에 종속 행이 있는 경우 업데이트되며 **Vendor** 테이블에 있는 참조된 행도 업데이트됩니다.  
  
 반대로 NO ACTION을 지정한 경우 **ProductVendor** 테이블에 **Vendor** 행을 참조하는 행이 하나 이상 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생하고 참조된 행의 업데이트 동작이 롤백됩니다.  
  
 NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 FOREIGN KEY 제약 조건 및 CHECK 제약 조건에 대해 지정할 수 있습니다. 제약 조건에 대해 이 절을 지정하면 복제 에이전트가 삽입, 업데이트 또는 삭제 작업을 수행할 때 해당 제약 조건이 강제로 적용되지 않습니다.  

 CONNECTION은 에지 제약 조건이 부여된 노드 테이블 쌍의 연결을 허용하도록 지정합니다. ON DELETE는 이 에지 테이블의 에지를 통해 연결된 노드가 삭제될 때 에지 테이블의 행에 어떤 일이 발생하는 지 지정합니다. 
 
 DEFAULT  
 열에 대한 기본값을 지정합니다. DEFAULT 정의를 사용하여 기존 데이터 행에 새 열의 값을 제공할 수 있습니다. **timestamp** 데이터 형식, IDENTITY 속성, 기존 DEFAULT 정의 또는 바인딩된 기본값을 가진 열에는 DEFAULT 정의를 추가할 수 없습니다. 기존 기본값이 있는 열은 새 기본값을 추가하기 전에 기존 기본값을 삭제해야 합니다. 사용자 정의 형식 열에 대해 기본값을 지정할 경우 *constant_expression* 에서 해당 사용자 정의 형식으로 암시적으로 변환할 수 있어야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 DEFAULT에 제약 조건 이름을 할당할 수 있습니다.  
  
 *constant_expression*  
 기본 열 값으로 사용되는 리터럴 값, NULL 또는 시스템 함수입니다. *constant_expression* 을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식으로 정의된 열과 함께 사용할 경우 *constant_expression* 에서 해당 사용자 정의 형식으로의 암시적 전환이 지원되어야 합니다.  
  
 FOR *column*  
 테이블 수준 DEFAULT 정의와 관련된 열을 지정합니다.  
  
 WITH VALUES  
 열 및 DEFAULT 제약 조건을 추가할 때 열에서 NULLS를 허용하는 경우 기존 행에 WITH VALUES를 사용하면 새 열의 값이 DEFAULT *constant_expression* 에 제공된 값으로 설정됩니다. 추가되는 열에서 NULLS를 허용하지 않으면 기존 행의 열 값은 항상 DEFAULT *constant expression* 에 제공된 값으로 설정됩니다. SQL Server 2012부터 이 작업은 메타데이터 작업 [온라인 작업으로 null 열을 추가하지 않음](alter-table-transact-sql.md#adding-not-null-columns-as-an-online-operation)입니다.
관련 열이 추가되지 않을 때 이 작업이 사용되면 아무런 영향을 주지 않습니다. 
  
 CHECK  
 열에 입력 가능한 값을 제한하여 도메인 무결성을 적용하는 제약 조건입니다.  
  
 *logical_expression*  
 CHECK 제약 조건에 사용되는 논리 식이며 TRUE 또는 FALSE를 반환합니다. *logical_expression* 을 CHECK 제약 조건에 사용하면 다른 테이블을 참조할 수 없지만 같은 행에 대해 동일한 테이블의 다른 열은 참조할 수 있습니다. 식은 별칭 데이터 형식을 참조할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 WITH NOCHECK 옵션을 지정하지 않으면 FOREIGN KEY 또는 CHECK 제약 조건이 추가될 경우 기존의 모든 데이터에 대해 제약 조건 위반 검사가 수행됩니다. 제약 조건 위반이 발생할 경우 ALTER TABLE이 실패하고 오류가 반환됩니다. 기존 열에 PRIMARY KEY 또는 UNIQUE 제약 조건을 새로 추가하려면 열의 데이터가 고유해야 합니다. 중복된 값이 있으면 ALTER TABLE이 실패합니다. PRIMARY KEY 또는 UNIQUE 제약 조건을 추가하면 WITH NOCHECK 옵션이 적용되지 않습니다.  
  
 각 PRIMARY KEY 및 UNIQUE 제약 조건은 인덱스를 생성합니다. UNIQUE 및 PRIMARY KEY 제약 조건의 수가 많아도 테이블의 비클러스터형 인덱스는 999개, 클러스터형 인덱스는 1개를 초과할 수 없습니다. FOREIGN KEY 제약 조건은 인덱스를 자동으로 생성하지 않습니다. 그러나 외래 키 열은 쿼리에서 한 테이블의 FOREIGN KEY 제약 조건 열을 다른 테이블의 기본 또는 고유 키 열과 연결하는 조인에서 자주 사용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 외래 키 열의 인덱스를 만들어 외래 키 테이블에 있는 관련 데이터를 빠르게 찾을 수 있습니다.  
  
## <a name="examples"></a>예제  
 예제는 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
