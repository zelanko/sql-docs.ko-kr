---
title: managed_backup. fn_get_current_xevent_settings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_current_xevent_settings
- smart_admin.fn_get_current_xevent_settings_TSQL
- fn_get_current_xevent_settings_TSQL
- smart_admin.fn_get_current_xevent_settings
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_current_xevent_settings
- fn_get_current_xevent_settings
ms.assetid: 95d3adaa-bb9d-4833-b8b4-3d9fd4f9c82a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4133f8bb64d5d7e2e2b511c2128b9ddbca1fa550
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67910241"
---
# <a name="managed_backupfn_get_current_xevent_settings-transact-sql"></a>managed_backup. fn_get_current_xevent_settings (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스마트 관리에서 지원되는 각 확장 이벤트 유형에 대해 1개 행을 반환합니다.  
  
 구성 가능한 이벤트 유형 및 현재 구성을 확인하려면 이 함수를 사용하여 현재 확장 이벤트 설정을 반환하거나 검토합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
smart_admin.fn_get_current_xevent_settings ()   
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>인수의  
 이 함수에는 인수가 없습니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 확장 이벤트의 Admin, Analytic 및 Operational 채널은 기본적으로 사용하도록 설정되며 구성할 수 없습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|Event_name|NVARCHAR(128)|확장 이벤트 유형|  
|is_configurable|NVARCHAR(128)|이 이벤트는 이벤트를 구성할 수 있는 경우 **True** 로 설정 되 고, 그렇지 않으면 **False**로 설정 됩니다.|  
|is_enabled|NVARCHAR(128)|이벤트가 사용하도록 설정되어 있으면 True로 설정되고 그렇지 않으면 False로 설정됩니다. 디버그 이벤트를 사용하도록 설정하려면 smart_admin.sp_set_parameter를 사용합니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 함수에 대 한 **SELECT** 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 상태와 함께 모든 확장 이벤트를 반환합니다.  
  
```  
SELECT *   
FROM smart_admin.fn_get_current_xevent_settings ()  
  
```  
  
  
