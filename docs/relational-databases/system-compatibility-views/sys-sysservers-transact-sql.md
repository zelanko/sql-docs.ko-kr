---
title: sys.sysservers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
author: rothja
ms.author: jroth
ms.openlocfilehash: 03875d828940a2baa5d9f30f7beb58adb77abf07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018112"
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 OLE DB 데이터 원본으로 액세스할 수 있는 각 서버에 대해 한 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|원격 서버의 ID(로컬 전용)입니다.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|서버의 이름입니다.|  
|**srvproduct**|**sysname**|원격 서버의 제품 이름입니다.|  
|**providername**|**nvarchar(128)**|해당 서버에 대한 액세스의 OLE DB 공급자 이름입니다.|  
|**datasource**|**nvarchar(4000)**|OLE DB 데이터 원본 값입니다.|  
|**location**|**nvarchar(4000)**|OLE DB 위치 값입니다.|  
|**providerstring**|**nvarchar(4000)**|OLE DB 공급자 문자열 값입니다.|  
|**schemadate**|**datetime**|해당 행이 마지막으로 업데이트된 날짜입니다.|  
|**topologyx**|**int**|사용되지 않습니다.|  
|**topologyy**|**int**|사용되지 않습니다.|  
|**catalog**|**sysname**|OLE DB 공급자에 연결할 때 사용하는 카탈로그입니다.|  
|**srvcollation**|**sysname**|서버의 데이터 정렬입니다.|  
|**connecttimeout**|**int**|서버 연결의 제한 시간 설정입니다.|  
|**querytimeout**|**int**|서버에 대한 쿼리의 제한 시간 설정입니다.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = 서버가 원격 서버입니다.<br /><br /> 0 = 서버가 연결된 서버입니다.|  
|**rpc**|**bit**|1 = **sp_serveroption@rpc** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 = **sp_serveroption@rpc** 로 설정 **false** 하거나 **해제**합니다.|  
|**pub**|**bit**|1 = **sp_serveroption@pub** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 = **sp_serveroption@pub** 로 설정 **false** 하거나 **해제**합니다.|  
|**sub**|**bit**|1 = **sp_serveroption@sub** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 = **sp_serveroption@sub** 로 설정 **false** 하거나 **해제**합니다.|  
|**dist**|**bit**|1 = **sp_serveroption@dist** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 = **sp_serveroption@dist** 로 설정 **false** 하거나 **해제**합니다.|  
|**dpub**|**bit**|1 = **sp_serveroption@dpub** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 = **sp_serveroption@dpub** 로 설정 **false** 하거나 **해제**합니다.|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc 초과** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 =  **sp_serveroption@rpc 초과** 로 설정 **false** 하거나 **해제**합니다.|  
|**dataaccess**|**bit**|1 =  **sp_serveroption@data 액세스** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 =  **sp_serveroption@data 액세스** 로 설정 **false** 하거나 **해제**합니다.|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation 호환** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 =  **sp_serveroption@collation 호환** 로 설정 **false** 하거나 **해제**합니다.|  
|**system**|**bit**|1 = **sp_serveroption@system** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 = **sp_serveroption@system** 로 설정 **false** 하거나 **해제**합니다.|  
|**useremotecollation**|**bit**|1 =  **sp_serveroption@remote 데이터 정렬을** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 =  **sp_serveroption@remote 데이터 정렬을** 로 설정 **false** 하거나 **해제**합니다.|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy 스키마 유효성 검사** 로 설정 **true** 하거나 **에서**합니다.<br /><br /> 0 =  **sp_serveroption@lazy 스키마 유효성 검사** 로 설정 **false** 하거나 **해제**합니다.|  
|**collation**|**sysname**|서버 데이터 정렬에서 설정한 대로  **sp_serveroption@collation 이름**합니다.|  
|**nonsqlsub**|bit|0 = 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스입니다.<br /><br /> 1 = 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 아닙니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
