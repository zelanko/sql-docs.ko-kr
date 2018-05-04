---
title: sys.database_usage (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7754ed63cc6325b9b6cf1650e7b71daad03393ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **참고:이 Azure SQL 데이터베이스 V11에만 적용 합니다.**  
  
 개수, 형식 및 데이터베이스의 기간에 나열 된 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버입니다.  
  
 **sys.database_usage** 다음 열이 뷰에 포함 합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|time|사용 이벤트가 발생한 날짜입니다.|  
|sku|데이터베이스에 대 한 서비스 계층 유형은: **웹**, **비즈니스**, **기본**, **표준**, **Premium**|  
|quantity|하루 동안 존재한 SKU 형식 데이터베이스의 최대 수입니다.|  
  
## <a name="permissions"></a>Permissions  
 이 보기에 읽기 전용 액세스는 연결할 수 있는 권한이 있는 모든 사용자가 사용할 수는 **마스터** 데이터베이스입니다.  
  
## <a name="remarks"></a>주의  
 **sys.database_usage** 보기 각 날짜의 구독에 대 한 하나의 행을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터베이스 가격 정보](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [Windows Azure SQL 데이터베이스의 계정 및 청구](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
