---
title: sys. dm_os_enumerate_fixed_drives (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c45db91b29c85d6ffced4e31e01fb8f24f338c16
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830540"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys. dm_os_enumerate_fixed_drives (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

SQL Server 2019에서 도입 되었습니다.

과 같은 드라이브 문자에 탑재 된 볼륨을 열거 `C:\` 합니다.

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|와 같은 볼륨의 경로 `C:\` 입니다.|  
|`drive_type`|`int`|드라이브 종류에 대 한 코드입니다. [ `GetDriveTypeW` 함수](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)를 참조 하세요.|
|`drive_type_desc`|`nvarchar(512)`|드라이브 유형에 대 한 설명입니다. [ `GetDriveTypeW` 함수](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)를 참조 하세요.|
|`free_space_in_bytes`|`bigint`|사용 가능한 디스크 공간 (바이트)입니다.|

## <a name="permissions"></a>사용 권한

사용자에 게 `VIEW SERVER STATE` 서버에 대 한 권한이 있어야 합니다.

## <a name="see-also"></a>참고 항목  

 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;i/o 관련 동적 관리 뷰 및 함수](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
