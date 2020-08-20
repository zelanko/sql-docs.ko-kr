---
description: sysarticlecolumns(Transact-SQL)
title: sysarticlecolumns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 45cc5fc3a39f13f7795e2f26aa91a15b618e2d38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460251"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns** 테이블은 스냅숏 또는 트랜잭션 게시에 게시 되는 각 테이블 열에 대해 하나의 행을 포함 하 고 각 열을 해당 아티클에 매핑합니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클을 식별합니다.|  
|**id**|**smallint**|아티클의 열을 식별합니다.|  
|**is_udt**|**bit**|열이 UDT(사용자 정의 데이터 형식) 열인지 여부를 나타냅니다. 값 **1** 은 UDT 열을 나타냅니다.|  
|**is_xml**|**bit**|열이 **xml** 열인지 여부를 나타냅니다. 값 **1** 은 xml 열을 나타냅니다.|  
|**is_max**|**bit**|열이 Large Value 데이터 형식 열, **varchar (max)**, **nvarchar (max)** 및 **varbinary (max)** 인지 여부를 나타냅니다. 값 **1** 은 많은 값 열을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
