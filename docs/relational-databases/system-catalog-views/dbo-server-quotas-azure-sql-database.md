---
title: dbo.server_quotas (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8338b6768f25f31b4b217f938357de8090b55326
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **중요!!** 이에 적용 됩니다  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11만!**  
>   
>  이 기능은 미리 보기 상태입니다. 이 기능은 향후 릴리스에서 변경되거나 제거될 수 있으므로 이 기능의 특정 구현에 의존하지 마세요.  
  
 서버의 사용 가능한 데이터베이스 할당량 유형을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|서버의 할당량 유형입니다. 형식 **Premium_database** 리소스 예약을 사용 하 여 데이터베이스에 해당 합니다.|  
|quota_value|**int**|서버에서 허용되는 할당량 유형의 수입니다.|  
  
## <a name="permissions"></a>Permissions  
 이 뷰는 가상에 연결할 수 있는 권한 가진 모든 사용자 역할에 사용할 수 있는 **마스터** 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Premium 데이터베이스 관리](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
