---
title: MSmerge_settingshistory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 89a936fa8dad5df860f72295c93c915b055a3c48
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784811"
---
# <a name="msmerge_settingshistory-transact-sql"></a>MSmerge_settingshistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_settingshistory** 테이블은 병합 복제에 대 한 아티클 및 게시 속성에 대 한 변경 기록을 유지 관리 하는 데 사용 되며 병합 복제 토폴로지에 대 한 각 변경 내용에 대해 행이 하나씩 있습니다. 또한 이 테이블에는 초기 속성 설정이 이루어진 시간에 대한 정보도 저장됩니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|이벤트가 발생한 datetime입니다.|  
|**pubid**|**uniqueidentifier**|지정된 게시의 고유 ID입니다.|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**이벤트**|**tinyint**|기록될 이벤트 유형을 지정하며 값은 다음 중 하나일 수 있습니다.<br /><br /> **1** -초기 게시 수준 속성 설정입니다.<br /><br /> **2** -게시 속성 변경<br /><br /> **101** -초기 아티클 속성 설정<br /><br /> **102** -아티클 속성을 변경 합니다.|  
|**propertyname**|**sysname**|설정 또는 변경된 속성의 이름입니다.|  
|**previousvalue**|**sysname**|속성이 변경된 경우 이전 속성 값입니다.|  
|**newvalue**|**sysname**|변경되거나 생성된 속성 값입니다.|  
|**eventtext**|**nvarchar (2000)**|이벤트를 설명하는 문자열입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
