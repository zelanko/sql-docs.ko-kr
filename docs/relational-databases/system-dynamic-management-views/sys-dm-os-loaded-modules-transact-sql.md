---
title: sys.dm_os_loaded_modules (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_loaded_modules
- dm_os_loaded_modules
- sys.dm_os_loaded_modules_TSQL
- dm_os_loaded_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_loaded_modules dynamic management view
ms.assetid: 56c7743a-b568-4943-bd3b-73c57d9d641c
author: stevestein
ms.author: sstein
ms.openlocfilehash: f43e03e482bb7125100ed7bed56337fb75a2e711
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900084"
---
# <a name="sysdmosloadedmodules-transact-sql"></a>sys.dm_os_loaded_modules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 주소 공간으로 로드되는 각 모듈에 대해 행을 반환합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 이름을 사용 하 여 **sys.dm_pdw_nodes_os_loaded_modules**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary(8)**|처리 중인 모듈의 주소입니다.|  
|**file_version**|**varchar(23)**|파일 버전입니다. 형식은 다음과 같습니다.<br /><br /> x.x:x.x|  
|**product_version**|**varchar(23)**|제품 버전입니다. 형식은 다음과 같습니다.<br /><br /> x.x:x.x|  
|**debug**|**bit**|1 = 로드된 모듈의 디버그 버전입니다.|  
|**patched**|**bit**|1 = 모듈이 패치되었습니다.|  
|**prerelease**|**bit**|1 = 로드된 모듈의 시험판 버전입니다.|  
|**private_build**|**bit**|1 = 로드된 모듈의 프라이빗 빌드입니다.|  
|**special_build**|**bit**|1 = 로드된 모듈의 특수 빌드입니다.|  
|**language**|**int**|모듈 버전 정보의 언어입니다.|  
|**company**|**nvarchar(256)**|모듈을 만든 회사의 이름입니다.|  
|**description**|**nvarchar(256)**|모듈에 대한 설명입니다.|  
|**name**|**nvarchar(255)**|모듈의 이름입니다. 모듈의 전체 경로가 포함됩니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
