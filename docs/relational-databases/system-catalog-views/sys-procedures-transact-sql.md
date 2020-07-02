---
title: sys. 프로시저 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- procedures
- sys.procedures_TSQL
- sys.procedures
- procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.procedures catalog view
ms.assetid: d17af274-b2dd-464e-9523-ee1f43e1455b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5e6d1842989766c0cf77f141a62ebb6e146281f3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85678303"
---
# <a name="sysprocedures-transact-sql"></a>sys.procedures(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  예를 들어 **sys. type** = P, X, RF 및 PC와 같은 일종의 프로시저인 각 개체에 대 한 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 을 참조 하세요&#41;|  
|**is_auto_executed**|**bit**|1인 경우 서버 시작 시 프로시저가 자동으로 실행됩니다. 자동으로 실행하지 않으려면 0으로 설정합니다. master 데이터베이스의 프로시저에 대해서만 설정할 수 있습니다.|  
|**is_execution_replicated**|**bit**|이 프로시저의 실행이 복제됩니다.|  
|**is_repl_serializable_only**|**bit**|프로시저 실행 복제는 트랜잭션을 직렬화할 수 있는 경우에만 수행됩니다.|  
|**skips_repl_constraints**|**bit**|실행하는 동안 프로시저는 NOT FOR REPLICATION이라고 표시된 제약 조건을 건너뜁니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
