---
description: sys.dm_os_host_info (Transact-sql)
title: sys.dm_os_host_info (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee91975b31d16845c56f27e872998809fb252838
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468394"
---
# <a name="sysdm_os_host_info-transact-sql"></a>sys.dm_os_host_info (Transact-sql)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

운영 체제 버전 정보를 표시 하는 한 행을 반환 합니다.  
  
|열 이름 |데이터 형식 |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |운영 체제 유형: Windows 또는 Linux |
|**host_distribution** |**nvarchar(256)** |운영 체제에 대 한 설명입니다. |
|**host_release**|**nvarchar(256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제 릴리스(버전 번호)입니다. 값 및 설명 목록은 [운영 체제 버전 (Windows)](/windows/desktop/SysInfo/operating-system-version)을 참조 하세요. <br> Linux의 경우 빈 문자열을 반환 합니다. |  
|**host_service_pack_level**|**nvarchar(256)**|Windows 운영 체제의 서비스 팩 수준입니다. <br> Linux의 경우 빈 문자열을 반환 합니다. |  
|**host_sku**|**int**|Windows SKU(Stock Keeping Unit) ID입니다. SKU Id 및 설명 목록은 [GetProductInfo 함수](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getproductinfo)를 참조 하세요. Null을 허용합니다. <br> Linux의 경우 NULL을 반환 합니다. |  
|**os_language_version**|**int**|운영 체제의 Windows LCID(로캘 ID)입니다. LCID 값 및 설명 목록은 [Microsoft에서 할당 한 로캘 id](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)를 참조 하세요. null일 수 없습니다.|  

## <a name="remarks"></a>설명  
이 보기는 [sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)와 비슷하며 Windows와 Linux를 구분 하는 열을 추가 합니다.
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
`SELECT`에 대 한 사용 권한은 `sys.dm_os_host_info` `public` 기본적으로 역할에 부여 됩니다. 해지 된 경우 `VIEW SERVER STATE` 서버에 대 한 권한이 필요 합니다.   
 
> [!CAUTION]
>  버전 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3부터 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 버전 17부터 `SELECT` 에 연결 하기 위해에 대 한 권한이 필요 `sys.dm_os_host_info` [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 합니다. `SELECT`사용 권한이에서 해지 된 경우 `public` 권한이 있는 로그인만 `VIEW SERVER STATE` 최신 버전의 SSMS와 연결할 수 있습니다. 과 같은 다른 도구는 `sqlcmd.exe` `SELECT` 에 대 한 권한 없이 연결할 수 있습니다 `sys.dm_os_host_info` .

  
## <a name="examples"></a>예  
 다음 예에서는 **sys.dm_os_host_info** 뷰에서 모든 열을 반환 합니다.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Windows의 예제 결과 집합은 다음과 같습니다.
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

Linux의 예제 결과 집합은 다음과 같습니다.
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>참고 항목  
 [sys.dm_os_sys_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
