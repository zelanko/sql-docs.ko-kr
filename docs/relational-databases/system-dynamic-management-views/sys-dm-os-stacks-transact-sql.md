---
title: sys.dm_os_stacks (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c31bf39c4f133aa6f693614845cb54a5cf2bfc6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899753"
---
# <a name="sysdmosstacks-transact-sql"></a>sys.dm_os_stacks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이 동적 관리 뷰는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부에서 다음 용도로 사용됩니다.  
  
-   완료되지 않은 할당과 같은 디버그 데이터를 추적합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 특정 호출이 실행되었다고 가정하는 위치에서 이 구성 요소가 사용하는 논리를 가정하거나 유효성을 검사합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|이 스택 할당의 고유한 주소입니다. Null을 허용하지 않습니다.|  
|**frame_index**|**int**|각 줄이 함수를 나타내는 특정 프레임 인덱스로 오름차순으로 정렬 될 경우 호출 하 **stack_address**, 전체 호출 스택을 반환 합니다. Null을 허용하지 않습니다.|  
|**frame_address**|**varbinary(8)**|함수 호출 주소입니다. Null을 허용하지 않습니다.|  
  
## <a name="remarks"></a>설명  
 **sys.dm_os_stacks** 기호 서버 및 기타 구성 요소 정보를 올바르게 표시 하려면 서버에 설치 되어 있어야 합니다.  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]에서 데이터베이스에 대한 `VIEW DATABASE STATE` 권한이 필요합니다.   


## <a name="see-also"></a>관련 항목  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
