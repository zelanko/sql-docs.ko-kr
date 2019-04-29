---
title: MSmerge_settingshistory (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 25505e0b96c627feb51fd59abfe587851520b724
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026563"
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_settingshistory** 병합 복제 토폴로지에서 각 변경에 대 한 하나의 행이 병합 복제의 경우 아티클 및 게시 속성에 대 한 변경 내용의 기록을 유지 관리 테이블을 사용 합니다. 또한 이 테이블에는 초기 속성 설정이 이루어진 시간에 대한 정보도 저장됩니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|이벤트가 발생한 datetime입니다.|  
|**pubid**|**uniqueidentifier**|지정된 게시의 고유 ID입니다.|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**eventtype**|**tinyint**|기록될 이벤트 유형을 지정하며 값은 다음 중 하나일 수 있습니다.<br /><br /> **1** -초기 게시 수준 속성 설정 합니다.<br /><br /> **2** -게시 속성을 변경 합니다.<br /><br /> **101** -초기 아티클 속성 설정 합니다.<br /><br /> **102** -아티클 속성에서 변경 합니다.|  
|**propertyname**|**sysname**|설정 또는 변경된 속성의 이름입니다.|  
|**previousvalue**|**sysname**|속성이 변경된 경우 이전 속성 값입니다.|  
|**newvalue**|**sysname**|변경되거나 생성된 속성 값입니다.|  
|**eventtext**|**nvarchar(2000)**|이벤트를 설명하는 문자열입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
