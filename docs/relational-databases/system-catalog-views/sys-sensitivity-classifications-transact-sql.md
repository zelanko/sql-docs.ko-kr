---
title: sys. sensitivity_classifications (Transact-sql) | Microsoft Docs
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
- rank
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 376438a45d6b104cbf4e66dbdf8e5542cf3fd2c2
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542049"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sys.sensitivity_classifications(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

데이터베이스의 각 분류 된 항목에 대해 행을 반환 합니다.

|열 이름|데이터 형식|설명|
|-----------------|---------------|-----------------|  
|**클래스**|**int**|분류가 존재 하는 항목의 클래스를 식별 합니다. 항상 값 1 (열을 나타냄)이 있습니다.|  
|**class_desc**|**varchar (16)**|분류가 존재 하는 항목의 클래스에 대 한 설명입니다. 에는 항상 값이 포함 됩니다 *OBJECT_OR_COLUMN*|  
|**major_id**|**int**|All_objects에 해당 하는 분류 된 열을 포함 하는 테이블의 ID를 나타냅니다 object_id|  
|**minor_id**|**int**|All_columns에 해당 하는 분류가 있는 열의 ID를 나타냅니다 column_id|   
|**레이블**|**sysname 이며**|민감도 분류에 할당 된 레이블 (사람이 읽을 수 있음)|  
|**label_id**|**sysname 이며**|레이블과 연결 된 ID입니다 .이 ID는 AIP (Azure Information Protection)와 같은 정보 보호 시스템에서 사용할 수 있습니다.|  
|**information_type**|**sysname 이며**|민감도 분류에 할당 된 정보 유형 (사람이 읽을 수 있음)|  
|**information_type_id**|**sysname 이며**|정보 보호 시스템에서 사용할 수 있는 정보 유형과 연결 된 ID입니다 (AIP (Azure Information Protection)).|  
|**배열**|**int**|Rank의 숫자 값입니다. <br><br>없음의 경우 0<br>낮음의 경우 10<br>MEDIUM의 경우 20<br>높음의 경우 30<br>40 위험| 
|**rank_desc**|**sysname 이며**|Rank의 텍스트 표현입니다.  <br><br>없음, 낮음, 중간, 높음, 위험|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>설명  

- 이 보기는 데이터베이스의 분류 상태에 대 한 가시성을 제공 합니다. 데이터베이스 분류를 관리 하는 데 사용할 수 있으며 보고서를 생성 하는 데에도 사용할 수 있습니다.
- 현재 데이터베이스 열의 분류만 지원 됩니다.
 
## <a name="examples"></a>예

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 모든 분류 된 열 및 해당 분류 나열

다음 예에서는 데이터베이스의 각 분류 된 열에 대 한 테이블 이름, 열 이름, 레이블, 레이블 ID, 정보 유형, 정보 유형 ID를 나열 하는 테이블을 반환 합니다.

> [!NOTE]
> Label은 Azure SQL Data Warehouse에 대 한 키워드입니다.

```sql
SELECT
    SCHEMA_NAME(sys.all_objects.schema_id) as SchemaName,
    sys.all_objects.name AS [TableName], sys.all_columns.name As [ColumnName],
    [Label], [Label_ID], [Information_Type], [Information_Type_ID], [Rank], [Rank_Desc]
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="permissions"></a>권한  
 **민감도 분류 보기** 권한이 필요 합니다. 
 
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]자세한 내용은 [메타 데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조 하세요.  

## <a name="see-also"></a>참고 항목  

[민감도 분류 추가 (Transact-sql)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP 민감도 분류 (Transact-sql)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[SQL Information Protection 시작](https://aka.ms/sqlip)
