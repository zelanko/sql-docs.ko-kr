---
title: sys. check_constraints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af931a3ac76186b0ac583155b0d45e4dbe7ed055
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718873"
---
# <a name="syscheck_constraints-transact-sql"></a>sys.check_constraints(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  CHECK 제약 조건에 해당 하는 각 개체에 대 한 행을 포함 합니다. 여기에는 **sys. type** = ' C '가 포함 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**is_disabled**|**bit**|CHECK 제약 조건이 비활성화되었습니다.|  
|**is_not_for_replication**|**bit**|CHECK 제약 조건이 NOT FOR REPLICATION 옵션으로 생성되었습니다.|  
|**is_not_trusted**|**bit**|시스템에서 모든 행에 대해 CHECK 제약 조건을 확인하지는 않았습니다.|  
|**parent_column_id**|**int**|0은 테이블 수준의 CHECK 제약 조건임을 의미합니다.<br /><br /> 0이 아닌 값은 지정된 ID 값을 가진 열에 정의된 열 수준의 CHECK 제약 조건임을 의미합니다.|  
|**정의**|**nvarchar(max)**|현재 CHECK 제약 조건을 정의하는 SQL 식입니다.|  
|**uses_database_collation**|**bit**|1 = 제약 조건 정의는 정확한 평가를 위해 데이터베이스의 기본 데이터 정렬에 의존합니다. 그렇지 않으면 0입니다. 이러한 종속성으로 인해 데이터베이스의 기본 데이터 정렬을 바꿀 수 없습니다.|  
|**is_system_named**|**bit**|1 = 시스템에서 이름을 생성했습니다.<br /><br /> 0 = 사용자가 제공한 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
