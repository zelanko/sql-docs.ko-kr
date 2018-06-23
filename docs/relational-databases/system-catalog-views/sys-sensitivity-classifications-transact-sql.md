---
title: sys.sensitivity_classifications (Transact SQL) | Microsoft Docs
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: t-sql
ms.suite: sql
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: d0adbbeb82c06d6a44f3a7439bcbf479d7358401
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262892"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

데이터베이스에 분류 된 각 항목에 대 한 행을 반환합니다.

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|  
|**class**|**int**|분류 존재 하는 항목의 클래스를 식별 합니다.|  
|**class_desc**|**varchar (16)**|분류 존재 하는 항목의 클래스에 대 한 설명|  
|**major_id**|**int**|분류 존재 하는 항목의 ID입니다. < b r \>< b r \>클래스 0 이면 major_id는 항상 0입니다.<br>class가 1, 2 또는 7이면 major_id는 object_id입니다.|  
|**minor_id**|**int**|분류의 존재는 항목의 보조 ID는 해당 클래스에 따라 해석 됩니다.<br><br>경우 클래스 = 1 이면 minor_id는 column_id이 고 (하는 경우 열), 그렇지 않으면 0 (하는 경우 개체).<br>class = 2이면 minor_id는 parameter_id입니다.<br>경우 클래스 = 7 까지의 유형은 minor _id는 index_id입니다. |  
|**label**|**sysname**|민감도 분류에 대 한 할당 레이블 (사람이 읽을 수 있음)|  
|**label_id**|**sysname**|정보 보호 시스템 Azure 정보 보호 (AIP) 등에서 사용할 수 있는 레이블과 연결 된 ID|  
|**information_type**|**sysname**|민감도 분류에 대 한 할당 정보 유형 (사람이 읽을 수 있음)|  
|**information_type_id**|**sysname**|정보 보호 시스템 Azure 정보 보호 (AIP) 등에서 사용할 수 있는 정보 유형에 연결 된 ID|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Remarks  

- 이 뷰는 데이터베이스의 분류 상태에 대 한 가시성을 제공합니다. 보고서 생성 뿐만 아니라 데이터베이스 분류 관리를 사용할 수 있습니다.
- 데이터베이스 열의 현재만 분류 지원 됩니다. 따라서:
    - **클래스** -은 항상 값 1 (열을 나타냄)
    - **class_desc** -값은 항상 *OBJECT_OR_COLUMN*
    - **major_id** -sys.all_objects.object_id에 해당 하는 분류 된 열을 포함 하는 테이블의 ID를 나타냅니다
    - **minor_id** -분류 존재 하는, sys.all_columns.column_id와 해당 하는 열의 ID를 나타냅니다.

## <a name="examples"></a>예

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>1. 모든 분류 된 열과 해당 분류를 나열합니다.

다음 예제에서는 반환 테이블 이름, 열 이름, 레이블 나열 되어 있는 표 ID, 정보 유형 정보 유형 ID는 데이터베이스에서 각 분류 된 열에 대 한 레이블을 지정 합니다.

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

[추가 구분 CLASSIFICTION (Transact SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP 민감도 CLASSIFICTION (Transact SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[SQL 정보 보호를 시작 하기](http://aka.ms/sqlip)
