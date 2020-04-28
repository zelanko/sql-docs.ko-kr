---
title: database_usage (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0a0789ebd9a5aa4bd10605d69afa59a586ce75b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70155542"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **참고: Azure SQL Database V11 적용 됩니다.**  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 있는 데이터베이스의 수, 유형 및 기간을 나열 합니다.  
  
 **Database_usage** 뷰에는 다음 열이 포함 되어 있습니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|time|사용 이벤트가 발생한 날짜입니다.|  
|sku|데이터베이스의 서비스 계층 형식: **Web**, **Business**, **Basic**, **Standard**, **Premium**|  
|quantity|하루 동안 존재한 SKU 형식 데이터베이스의 최대 수입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Master** 데이터베이스에 대 한 연결 권한이 있는 모든 사용자는이 뷰에 대 한 읽기 전용 액세스를 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **Database_usage** 뷰는 구독의 각 날짜에 대해 하나의 행을 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Database 가격 정보](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Azure SQL 데이터베이스에서 계정 및 요금 청구](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
