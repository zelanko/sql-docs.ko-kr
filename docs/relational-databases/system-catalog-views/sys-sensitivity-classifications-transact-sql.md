---
title: sensitivity_classifications (Transact-sql) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: mibar
author: barmichal
f1_keywords:
- 'sys.sensitivity_classifications '
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sensitivity_classifications statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a9d14cd93b08c0094ad984a6469b433e0b266479
ms.sourcegitcommit: 77293fb1f303ccfd236db9c9041d2fb2f64bce42
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929776"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sensitivity_classifications (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

데이터베이스의 각 분류 된 항목에 대해 행을 반환 합니다.

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|  
|**class**|**int**|분류가 존재 하는 항목의 클래스를 식별 합니다.|  
|**class_desc**|**varchar(16)**|분류가 존재 하는 항목의 클래스에 대 한 설명입니다.|  
|**major_id**|**int**|분류가 있는 항목의 ID입니다. < br \>< br \>클래스가 0 이면 major_id는 항상 0입니다.<br>class가 1, 2 또는 7이면 major_id는 object_id입니다.|  
|**minor_id**|**int**|분류가 존재 하는 항목의 보조 ID입니다. 해당 클래스에 따라 해석 됩니다.<br><br>Class = 1 인 경우 minor_id은 column_id (if 열)이 고, 그렇지 않으면 0 (object)입니다.<br>class = 2이면 minor_id는 parameter_id입니다.<br>Class = 7 인 경우 minor_id은 index_id입니다. |  
|**label**|**sysname**|민감도 분류에 할당 된 레이블 (사람이 읽을 수 있음)|  
|**label_id**|**sysname**|레이블과 연결 된 ID입니다 .이 ID는 AIP (Azure Information Protection)와 같은 정보 보호 시스템에서 사용할 수 있습니다.|  
|**information_type**|**sysname**|민감도 분류에 할당 된 정보 유형 (사람이 읽을 수 있음)|  
|**information_type_id**|**sysname**|정보 보호 시스템에서 사용할 수 있는 정보 유형과 연결 된 ID입니다 (AIP (Azure Information Protection)).|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>설명  

- 이 보기는 데이터베이스의 분류 상태에 대 한 가시성을 제공 합니다. 데이터베이스 분류를 관리 하는 데 사용할 수 있으며 보고서를 생성 하는 데에도 사용할 수 있습니다.
- 현재 데이터베이스 열의 분류만 지원 됩니다. 하므로
    - **클래스** -항상 값 1 (열을 나타냄)을 갖습니다.
    - **class_desc** -항상 *OBJECT_OR_COLUMN* 값을 갖습니다.
    - **major_id** -object_id에 해당 하는 분류 된 열이 포함 된 테이블의 id를 나타냅니다.
    - **minor_id** -column_id에 해당 하는 분류가 있는 열의 id를 나타냅니다.

## <a name="examples"></a>예

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 모든 분류 된 열 및 해당 분류 나열

다음 예에서는 데이터베이스의 각 분류 된 열에 대 한 테이블 이름, 열 이름, 레이블, 레이블 ID, 정보 유형, 정보 유형 ID를 나열 하는 테이블을 반환 합니다.

> [!NOTE]
> Label은 Azure SQL Data Warehouse에 대 한 키워드입니다.

```sql
SELECT
    SCHEMA_NAME(sys.all_objects.schema_id) as SchemaName,
    sys.all_objects.name AS [TableName], sys.all_columns.name As [ColumnName],
    [Label], [Label_ID], [Information_Type], [Information_Type_ID]
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  

## <a name="see-also"></a>관련 항목  

[ADD SENSITIVITY CLASSIFICATION(Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICATION(Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[SQL Information Protection 시작](https://aka.ms/sqlip)
