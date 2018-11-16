---
title: sys.sensitivity_classifications (TRANSACT-SQL) | Microsoft Docs
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
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
ms.openlocfilehash: 0fb7b7719ce53fe4f20863cb3f44c9483bc6b472
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660352"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

데이터베이스의 분류 된 각 항목에 대 한 행을 반환 합니다.

|열 이름|데이터 형식|설명|
|-----------------|---------------|-----------------|  
|**class**|**int**|분류 존재 하는 항목의 클래스를 식별|  
|**class_desc**|**varchar(16)**|분류 존재 하는 항목의 클래스에 대 한 설명|  
|**major_id**|**int**|분류 존재 하는 항목의 ID입니다. < b r \>< b r \>클래스 0 이면 major_id는 항상 0입니다.<br>class가 1, 2 또는 7이면 major_id는 object_id입니다.|  
|**minor_id**|**int**|분류 존재 하는 항목의 보조 ID는 해당 클래스에 따라 해석 됩니다.<br><br>경우 클래스 = 1 이면 minor_id는 column_id이 (하는 경우 열), 그렇지 않으면 0 (하는 경우 개체).<br>class = 2이면 minor_id는 parameter_id입니다.<br>경우 클래스 = 7 minor _id는 index_id입니다. |  
|**label**|**sysname**|민감도 분류에 할당 된 레이블 (사람이 읽을 수 있음)|  
|**label_id**|**sysname**|ID가 같은 AIP Azure Information Protection ()는 정보 보호 시스템에서 사용할 수 있는 레이블 연결|  
|**information_type**|**sysname**|민감도 분류에 대 한 할당 정보 유형 (사람이 읽을 수 있음)|  
|**information_type_id**|**sysname**|ID가 같은 AIP Azure Information Protection ()는 정보 보호 시스템에서 사용할 수 있는 정보 유형과 사용 하 여 연결|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Remarks  

- 이 뷰는 데이터베이스 분류 상태에 대 한 가시성을 제공 합니다. 보고서를 생성할 뿐만 아니라 데이터베이스 분류를 관리 하기 위한 사용할 수 있습니다.
- 데이터베이스 열의 현재 전용 분류가 지원 됩니다. 결과적으로:
    - **클래스** -1 (열) 값은 항상
    - **class_desc** -값은 항상 *OBJECT_OR_COLUMN*
    - **major_id** -sys.all_objects.object_id를 사용 하 여 해당 분류 된 열이 포함 된 테이블의 ID를 나타내는
    - **minor_id** -기반이 분류 있으면 sys.all_columns.column_id를 사용 하 여 해당 열의 ID를 나타내는

## <a name="examples"></a>예

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>1. 분류 된 모든 열과 해당 분류를 나열합니다.

다음 예제에서는 반환 테이블 이름, 열 이름, 레이블 나열 되어 있는 표 레이블 ID, 정보 유형, 데이터베이스의 각 분류 된 열에 대 한 정보 유형 ID입니다.

```sql
SELECT
    sys.all_objects.name AS TableName, sys.all_columns.name As ColumnName,
    Label, Label_ID, Information_Type, Information_Type_ID
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="see-also"></a>관련 항목  

[ADD SENSITIVITY CLASSIFICTION(Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICTION(Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[SQL Information Protection 시작](https://aka.ms/sqlip)
