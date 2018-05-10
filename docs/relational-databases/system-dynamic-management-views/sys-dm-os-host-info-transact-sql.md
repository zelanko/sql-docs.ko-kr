---
title: sys.dm_os_host_info (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 613b7884342750e84aa6f6476bc040c2dd37bead
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

운영 체제 버전 정보를 표시 하는 하나의 행을 반환 합니다.  
  
|열 이름 |데이터 형식 |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |운영 체제의 유형: Windows 또는 Linux |
|**host_distribution** |**nvarchar(256)** |운영 체제의 설명입니다. |
|**host_release**|**nvarchar(256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제 릴리스(버전 번호)입니다. 값 및 설명 목록은 참조 하세요. [운영 체제 버전 (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx)합니다. <br> Linux 용 빈 문자열을 반환 합니다. |  
|**host_service_pack_level**|**nvarchar(256)**|Windows 운영 체제의 서비스 팩 수준입니다. <br> Linux 용 빈 문자열을 반환 합니다. |  
|**host_sku**|**int**|Windows SKU(Stock Keeping Unit) ID입니다. SKU Id 및 설명의 목록에 대 한 참조 [GetProductInfo 함수](http://msdn.microsoft.com/library/ms724358.aspx)합니다. Null을 허용합니다. <br> Linux에서 NULL을 반환합니다. |  
|**os_language_version**|**int**|운영 체제의 Windows LCID(로캘 ID)입니다. LCID 값 및 설명의 목록에 대 한 참조 [Microsoft에서 할당 한 로캘 Id](http://go.microsoft.com/fwlink/?LinkId=208080)합니다. null일 수 없습니다.|  

## <a name="remarks"></a>주의  
이 보기는 비슷합니다 [sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), Windows 및 Linux를 구분 하는 열을 추가 합니다.
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
`SELECT` 에 대 한 권한이 `sys.dm_os_host_info` 에 부여 되는 `public` 기본적으로 역할입니다. 취소 하는 경우 필요 `VIEW SERVER STATE` 서버에 대 한 권한이 있습니다.   
 
>  [!CAUTION]
>  버전 부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 17 버전에 필요한 `SELECT` 에 대 한 권한이 `sys.dm_os_host_info` 에 연결 하기 위해 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 경우 `SELECT` 에서 사용 권한을 취소할 `public`, 사용 하 여 로그인만 `VIEW SERVER STATE` 권한이 SSMS의 최신 버전으로 연결할 수 있습니다. (같은 다른 도구 `sqlcmd.exe` 하지 않고 연결할 수 `SELECT` 에 대 한 권한이 `sys.dm_os_host_info`.)

  
## <a name="examples"></a>예  
 다음 예에서는 모든 열을 반환 된 **sys.dm_os_host_info** 보기.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Windows에 설정 하는 예제 결과 다음과 같습니다.
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

Linux에서 설정 하는 예제 결과 다음과 같습니다.
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

