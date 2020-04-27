---
title: sys. 경로 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: bfdd322107da1a08edb3933aee9d5b79b6c2b47a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67904430"
---
# <a name="sysroutes-transact-sql"></a>sys.routes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  이 카탈로그 뷰에는 각 경로에 대한 행이 포함되어 있습니다. Service Broker는 이러한 경로를 사용하여 서비스의 네트워크 주소를 찾습니다.   

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 내에서 고유한 경로의 이름입니다. NULL을 허용하지 않습니다.|  
|**route_id**|**int**|경로의 식별자입니다. NULL을 허용하지 않습니다.|  
|**principal_id**|**int**|경로를 소유하는 데이터베이스 보안 주체의 식별자입니다. NULL을 허용합니다.|  
|**remote_service_name**|**nvarchar(256)**|원격 서비스의 이름입니다. NULL을 허용합니다.|  
|**broker_instance**|**nvarchar(128)**|원격 서비스를 호스팅하는 broker의 식별자입니다. NULL을 허용합니다.|  
|**수명**|**datetime**|경로가 만료되는 날짜 및 시간입니다. 이 값은 현지 표준 시간대 대신 UTC를 사용하여 만료 시간을 표시합니다. NULL을 허용합니다.|  
|**address**|**nvarchar(256)**|Service Broker에서 원격 서비스를 위한 메시지를 보내는 네트워크 주소입니다. NULL을 허용합니다. SQL Database Managed Instance의 경우 address는 local 이어야 합니다.|  
|**mirror_address**|**nvarchar(256)**|주소에 지정된 서버에 대한 미러링 파트너의 네트워크 주소입니다. NULL을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
