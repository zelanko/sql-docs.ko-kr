---
title: sysarticlecolumns (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 61e1329fe35ae032b5d35f94dd2e1ce5e8d08d38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130524"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **sysarticlecolumns** 스냅숏 또는 트랜잭션 게시에 게시 되 고 해당 문서에 각 열을 매핑하는 각 테이블 열당 하나의 행을 포함 하는 테이블입니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클을 식별합니다.|  
|**colid**|**smallint**|아티클의 열을 식별합니다.|  
|**is_udt**|**bit**|열이 UDT(사용자 정의 데이터 형식) 열인지 여부를 나타냅니다. 값이 **1** UDT 열을 나타냅니다.|  
|**is_xml**|**bit**|열이 있는지 여부를 나타냅니다는 **xml** 열입니다. 값이 **1** xml 열을 나타냅니다.|  
|**is_max**|**bit**|열에 큰 값 데이터 형식 열이 있는지 여부를 나타냅니다 **varchar (max)** 하십시오 **nvarchar (max)** , 및 **varbinary (max)** 합니다. 값이 **1** 큰 값 열을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
