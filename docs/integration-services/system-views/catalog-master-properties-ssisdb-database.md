---
title: "catalog.master_properties (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 0fcbdca57c7764eaec758d2ad9ef3ab8675a3a9b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/08/2017

---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

속성을 표시는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스케일 아웃 마스터 합니다.

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|마스터 속성 확장의 이름입니다.|  
|property_value|**nvarchar(max)**|확장 마스터 속성의 값입니다.|

## <a name="remarks"></a>주의
이 뷰는 각 확장 마스터 속성에 대 한 행을 표시 합니다. 이 뷰에 표시되는 속성은 다음과 같습니다.

|속성 이름|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|데이터베이스를 로그 하는 SQL Server에서 찾습니다.|
|**LAST_ONLINE_TIME**|스케일 아웃 마스터는 온라인 때 마지막 시간입니다.|
|**MACHINE_IP**|컴퓨터의 IP입니다.|
|**이며 여기에서 MACHINE_NAME**|컴퓨터의 이름입니다.|
|**MASTER_ADDRESS**|스케일 아웃 마스터의 끝점입니다.|
|**MASTER_SERVICE_PORT**|스케일 아웃 마스터의 끝점에 사용 되는 포트입니다.|
|**SSLCERT_THUMBPRINT**|스케일 아웃 마스터 인증서의 지문입니다.|

## <a name="permissions"></a>Permissions
Public 데이터베이스 역할의 모든 구성원 한 읽기이 보기에 대 한 권한이 있어야 합니다. 

