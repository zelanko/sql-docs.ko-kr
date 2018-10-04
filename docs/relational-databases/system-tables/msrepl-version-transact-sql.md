---
title: MSrepl_version (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSrepl_version
- MSrepl_version_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_version system table
ms.assetid: c1330f03-940b-4564-ac42-6030c6e21173
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: febf6e606d422d816cdf02f62fcaab6ed7e9c6b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830751"
---
# <a name="msreplversion-transact-sql"></a>MSrepl_version(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSrepl_version** 복제가 설치의 현재 버전을 사용 하 여 하나의 행을 포함 하는 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**major_version**|**int**|배포 데이터베이스의 주 버전 번호입니다.|  
|**minor_version**|**int**|배포 데이터베이스의 부 버전 번호입니다.|  
|**수정 버전**|**int**|수정 버전 번호입니다.|  
|**db_existed**|**bit**|배포 데이터베이스 앞에 있는지 여부를 나타냅니다 **sp_adddistributiondb** 라고 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
