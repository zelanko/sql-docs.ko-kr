---
description: MSpeer_response(Transact-SQL)
title: MSpeer_response (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e0bb95540f6731c9fc1d49711b85d03c9fa2efad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488709"
---
# <a name="mspeer_response-transact-sql"></a>MSpeer_response(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpeer_response** 테이블은 피어 투 피어 복제에서 게시 상태 요청에 대 한 각 노드의 응답을 저장 하는 데 사용 됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) 테이블의 상태 요청 항목을 식별 합니다.|  
|**피어는**|**sysname**|응답을 생성한 피어입니다.|  
|**peer_db**|**sysname**|응답을 생성한 피어에 있는 구독 데이터베이스입니다.|  
|**received_date**|**datetime**|피어 요청을 받은 날짜 및 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
