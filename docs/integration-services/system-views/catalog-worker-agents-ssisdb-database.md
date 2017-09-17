---
title: "catalog.worker_agents (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d56af0ab150255c53746898a638a32112938755c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/08/2017

---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

에 대 한 정보를 표시는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스케일 아웃 작업자입니다.

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|작업자 에이전트 ID의 스케일 아웃 작업자입니다.|
|IsEnabled|**bit**|스케일 아웃 작업자 활성화 되어 있는지 여부를 나타냅니다.|
|DisplayName|**nvarchar(256)**|스케일 아웃 작업자의 표시 이름입니다.|
|Description|**nvarchar(256)**|스케일 아웃 작업자의 설명입니다.|
|MachineName|**nvarchar(256)**|스케일 아웃 작업자에 대 한 컴퓨터 이름입니다.|
|Tags|**nvarchar(max)**|스케일 아웃 작업자의 태그입니다.|
|UserAccount|**nvarchar(256)**|스케일 아웃 Worker 서비스를 실행 하는 사용자 계정입니다.|
|LastOnlineTime|**(7)**|마지막 시간 스케일 아웃 작업자는 온라인입니다.|

## <a name="remarks"></a>주의
이 뷰는 각 스케일 아웃 작업자 SSISDB 카탈로그 작업 마스터 스케일 아웃 연결에 대 한 행을 표시 합니다.

## <a name="permissions"></a>Permissions
이 뷰를 보려면 다음 권한 중 하나가 필요합니다.

- 멤버 자격에는 **ssis_admin** 데이터베이스 역할

- 멤버 자격에는 **ssis_cluster_executor** 데이터베이스 역할

- 멤버 자격에는 **sysadmin** 서버 역할

