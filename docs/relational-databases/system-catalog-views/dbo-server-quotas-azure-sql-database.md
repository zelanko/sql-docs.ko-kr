---
title: dbo.server_quotas (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 657376be08e4cd404ce53d78114604cdd11fbda2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005839"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **중요!!** 이 적용 됩니다  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11만!**  
>   
>  이 기능은 미리 보기 상태입니다. 이 기능은 향후 릴리스에서 변경되거나 제거될 수 있으므로 이 기능의 특정 구현에 의존하지 마세요.  
  
 서버의 사용 가능한 데이터베이스 할당량 유형을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|서버의 할당량 유형입니다. 형식 **Premium_database** 리소스 예약을 사용 하 여 데이터베이스에 해당 합니다.|  
|quota_value|**int**|서버에서 허용되는 할당량 유형의 수입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 보기는 가상으로 연결할 수 있는 권한 가진 모든 사용자 역할에 사용할 수 있습니다 **마스터** 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Premium 데이터베이스 관리](https://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
