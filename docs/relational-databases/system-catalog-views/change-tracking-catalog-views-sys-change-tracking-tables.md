---
title: sys. change_tracking_tables (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_tables_TSQL
- sys.change_tracking_tables
- change_tracking_tables
- sys.change_tracking_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], sys.change_tracking_tables
- sys.change_tracking_tables
ms.assetid: 97ec69b6-0d49-4d98-82f0-d3e77ba1ad2b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 158203b7dedfec3228821f6368c8f6c92b8041f7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68050876"
---
# <a name="change-tracking-catalog-views---syschange_tracking_tables"></a>변경 내용 추적 카탈로그 뷰-sys. change_tracking_tables
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  변경 내용 추적이 설정된 현재 데이터베이스의 각 테이블에 대해 한 개의 행을 반환합니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|변경 업무 일지가 있는 테이블의 ID입니다. 변경 내용 추적이 현재 해제되어 있는 경우에도 테이블에 변경 업무 일지가 있을 수 있습니다.<br /><br /> 테이블 ID는 데이터베이스 내에서 고유합니다.|  
|is_track_columns_updated_on|**bit**|테이블에서 변경 내용 추적의 현재 상태입니다.<br /><br /> 0 = OFF<br /><br /> 1 = ON|  
|begin_version|**bigint**|테이블에 대한 변경 내용 추적이 시작된 경우 데이터베이스의 버전입니다. 이 버전은 일반적으로 변경 내용 추적이 설정된 경우를 나타내지만 이 값은 테이블이 잘린 경우에 다시 설정됩니다.|  
|cleanup_version|**bigint**|정리가 변경 내용 추적 정보를 제거한 최대 버전입니다.|  
|min_valid_version|**bigint**|테이블에 사용할 수 있는 변경 내용 추적 정보의 최소 유효한 버전입니다.<br /><br /> 이 행에 연결된 테이블의 변경 내용을 가져올 경우 last_sync_version 값은 이 열에 보고된 버전보다 크거나 같아야 합니다. 자세한 내용은 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;transact-sql&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)를 참조 하세요.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;CHANGE_TRACKING_MIN_VALID_VERSION &#40;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰 변경 내용 추적](https://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
