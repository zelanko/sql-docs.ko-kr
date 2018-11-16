---
title: sys.database_usage (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f17e34de7c230b111652ea57a3baa072a442a6a5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656742"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **참고:이 Azure SQL Database V11에만 적용 합니다.**  
  
 개수, 형식 및 데이터베이스의 기간에 나열 된 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버.  
  
 합니다 **sys.database_usage** 뷰는 다음 열을 포함 합니다.  
  
|열 이름|설명|  
|-----------------|-----------------|  
|Time|사용 이벤트가 발생한 날짜입니다.|  
|sku|데이터베이스에 대 한 서비스 계층의 형식: **웹**를 **비즈니스**를 **기본**를 **표준**, **Premium**|  
|quantity|하루 동안 존재한 SKU 형식 데이터베이스의 최대 수입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 보기에 대 한 읽기 전용 액세스에 연결할 수 있는 권한이 있는 모든 사용자에 게 제공 되는 **마스터** 데이터베이스입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **sys.database_usage** 보기 구독의 각 날짜에 대해 하나의 행을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Database 가격 정보](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Windows Azure SQL Database의 계정 및 청구](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
