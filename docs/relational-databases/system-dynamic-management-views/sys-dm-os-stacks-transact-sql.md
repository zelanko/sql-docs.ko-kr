---
description: sys.dm_os_stacks(Transact-SQL)
title: sys.dm_os_stacks (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04f9fe453b2f3e74a96ebd20565d92038bff4bae
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97325349"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 동적 관리 뷰는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부에서 다음 용도로 사용됩니다.  
  
-   완료되지 않은 할당과 같은 디버그 데이터를 추적합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 특정 호출이 실행되었다고 가정하는 위치에서 이 구성 요소가 사용하는 논리를 가정하거나 유효성을 검사합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|이 스택 할당의 고유한 주소입니다. Null을 허용하지 않습니다.|  
|**frame_index**|**int**|각 줄은 특정 **stack_address** 의 프레임 인덱스를 기준으로 오름차순으로 정렬 될 때 전체 호출 스택을 반환 하는 함수 호출을 나타냅니다. Null을 허용하지 않습니다.|  
|**frame_address**|**varbinary(8)**|함수 호출 주소입니다. Null을 허용하지 않습니다.|  
  
## <a name="remarks"></a>설명  
 **sys.dm_os_stacks** 를 사용 하려면 서버와 기타 구성 요소의 기호가 서버에 있어야 정보를 올바르게 표시할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   


## <a name="see-also"></a>참고 항목  
  [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
