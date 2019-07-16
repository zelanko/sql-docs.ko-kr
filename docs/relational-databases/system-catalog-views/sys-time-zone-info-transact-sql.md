---
title: sys.time_zone_info (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.time_zone_info
- sys.time_zone_info_TSQL
- time_zone_info
- time_zone_info_TSQL
helpviewer_keywords:
- sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 69bfcbb7e1eeaf6b456a2e10d1f3bfcc581c3d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106699"
---
# <a name="systimezoneinfo-transact-sql"></a>sys.time_zone_info (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  지원 되는 표준 시간대에 대 한 정보를 반환합니다. 컴퓨터에 설치 하는 모든 표준 시간대는 다음 레지스트리 하이브에 저장 됩니다.  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`항목을 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Windows 표준 형식에 있는 표준 시간대의 이름입니다. 예를 들어 **중부 오스트레일리아 표준시** 나 **중앙 유럽 표준시**합니다.|  
|**current_utc_offset**|**nvarchar(12)**|현재 UTC 오프셋입니다. 예를 들어 **01:00** 하거나 **-07:00**합니다.|  
|**is_currently_dst**|**bit**|현재 일광 절약 시간제를 관찰 하는 경우 true입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [GETUTCDATE &#40;TRANSACT-SQL&#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [서버 차원의 구성 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
