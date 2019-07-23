---
title: catalog.master_properties(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 537b9a1d1b0fb84ba26c56aeb2f897d268bb2d03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104840"
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 마스터의 속성을 표시합니다.

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|scale out 마스터 속성의 이름입니다.|  
|property_value|**nvarchar(max)**|scale out 마스터 속성의 값입니다.|

## <a name="remarks"></a>Remarks
이 보기는 각 scale out 마스터 속성의 행을 표시합니다. 이 뷰에 표시되는 속성은 다음과 같습니다.

|속성 이름|설명|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|로그 데이터베이스가 있는 SQL Server입니다.|
|**LAST_ONLINE_TIME**|Scale Out 마스터가 마지막으로 온라인 상태인 시간입니다.|
|**MACHINE_IP**|컴퓨터의 IP입니다.|
|**MACHINE_NAME**|컴퓨터의 이름입니다.|
|**MASTER_ADDRESS**|Scale Out 마스터의 엔드포인트입니다.|
|**MASTER_SERVICE_PORT**|Scale Out 마스터 엔드포인트의 포트입니다.|
|**SSLCERT_THUMBPRINT**|Scale Out 마스터 인증서의 지문입니다.|

## <a name="permissions"></a>사용 권한
공용 데이터베이스 역할의 모든 구성원은 이 보기에 대한 읽기 권한을 갖습니다. 
