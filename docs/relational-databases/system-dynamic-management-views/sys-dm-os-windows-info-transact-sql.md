---
title: sys.dm_os_windows_info (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6f6669704242a780d947dc271cb81724429992a
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466289"
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows 운영 체제 버전 정보를 표시하는 행을 반환합니다.  
  
  Windows에서 실행 되는 SQL Server에만 적용 됩니다. Linux와 같은 비-Windows 호스트에서 실행 중인 SQL Server에 대 한 유사한 정보를 보려면 사용 [sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|Windows의 경우 릴리스 번호를 반환합니다. 값 및 설명 목록은 참조 하세요. [운영 체제 버전 (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx)합니다. NULL이 될 수 없습니다.|  
|**windows_service_pack_level**|**nvarchar(256)**| Windows 용 서비스 팩 번호를 반환합니다. NULL이 될 수 없습니다. |  
|**windows_sku**|**int**|Windows, Windows 재고 유지 단위 (SKU) ID를 반환합니다. SKU Id 및 설명의 목록에 대 한 참조 [GetProductInfo 함수](http://msdn.microsoft.com/library/ms724358.aspx)합니다. 이 null을 허용 합니다. |  
|**os_language_version**|**int**| Windows 운영 체제의 Windows 로캘 식별자 (LCID)를 반환합니다. LCID 값 및 설명의 목록에 대 한 참조 [Microsoft에서 할당 한 로캘 Id](http://go.microsoft.com/fwlink/?LinkId=208080)합니다. NULL이 될 수 없습니다.|  
  
  
## <a name="permissions"></a>Permissions  
Sys.dm_os_windows_info 대 한 SELECT 권한이 기본적으로 public 역할에 부여 됩니다. 취소 하는 경우에 서버에 대 한 VIEW SERVER STATE 권한이 필요 합니다.  

## <a name="limitations-and-restrictions"></a>제한 사항
Linux와 같은 비-Windows 호스트에서 실행 되는 SQL에 대 한 정보를 보려면 사용 [sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)합니다. 
  
## <a name="examples"></a>예  
 다음 예에서는 모든 열을 반환 된 **sys.dm_os_windows_info** 보기.  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

