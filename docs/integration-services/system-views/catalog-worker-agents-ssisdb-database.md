---
title: catalog.worker_agents(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2678853d13436811b53b40473a04191625535db
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295140"
---
# <a name="catalogworker_agents-ssisdb-database"></a>catalog.worker_agents(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker에 대한 정보를 표시합니다.

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Scale Out Worker의 작업자 에이전트 ID입니다.|
|IsEnabled|**bit**|Scale Out Worker의 사용 여부를 나타냅니다.|
|DisplayName|**nvarchar(256)**|Scale Out Worker의 표시 이름입니다.|
|설명|**nvarchar(256)**|Scale Out Worker에 대한 설명입니다.|
|MachineName|**nvarchar(256)**|Scale Out Worker의 컴퓨터 이름입니다.|
|Tags|**nvarchar(max)**|Scale Out Worker의 태그입니다.|
|UserAccount|**nvarchar(256)**|Scale Out Worker 서비스를 실행하는 사용자 계정입니다.|
|LastOnlineTime|**datetimeoffset(7)**|Scale Out Worker가 마지막으로 온라인 상태인 시간입니다.|

## <a name="remarks"></a>Remarks
이 보기는 SSISDB 카탈로그와 함께 작동하는 Scale Out 마스터에 연결하는 각 Scale Out Worker의 행을 표시합니다.

## <a name="permissions"></a>사용 권한
이 뷰를 보려면 다음 권한 중 하나가 필요합니다.

- **ssis_admin** 데이터베이스 역할에 대한 멤버 자격

- **ssis_cluster_executor** 데이터베이스 역할에 대한 멤버 자격

- **sysadmin** 서버 역할에 대한 멤버 자격
