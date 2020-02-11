---
title: sysservers (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 333be9cb6c86c1db3801ac50159610c6d19d1611
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68941107"
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 OLE DB 데이터 원본으로 액세스할 수 있는 각 서버에 대해 한 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|원격 서버의 ID(로컬 전용)입니다.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|서버의 이름입니다.|  
|**srvproduct**|**sysname**|원격 서버의 제품 이름입니다.|  
|**providername**|**nvarchar(128)**|해당 서버에 대한 액세스의 OLE DB 공급자 이름입니다.|  
|**datasource**|**nvarchar(4000)**|OLE DB 데이터 원본 값입니다.|  
|**위치도**|**nvarchar(4000)**|OLE DB 위치 값입니다.|  
|**providerstring**|**nvarchar(4000)**|OLE DB 공급자 문자열 값입니다.|  
|**schemadate**|**datetime**|해당 행이 마지막으로 업데이트된 날짜입니다.|  
|**topologyx**|**int**|사용되지 않습니다.|  
|**topologyy**|**int**|사용되지 않습니다.|  
|**catalog**|**sysname**|OLE DB 공급자에 연결할 때 사용하는 카탈로그입니다.|  
|**srvcollation**|**sysname**|서버의 데이터 정렬입니다.|  
|**connecttimeout**|**int**|서버 연결의 제한 시간 설정입니다.|  
|**querytimeout**|**int**|서버에 대한 쿼리의 제한 시간 설정입니다.|  
|**srvnetname**|**char (30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = 서버가 원격 서버입니다.<br /><br /> 0 = 서버가 연결된 서버입니다.|  
|**상관**|**bit**|1 = **sp_serveroption\@rpc** 가 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **rpc\@** 를 **false** 또는 **off**로 설정 sp_serveroption 합니다.|  
|**술집**|**bit**|1 = **sp_serveroption\@pub** 가 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@pub** 가 **false** 또는 **off**로 설정 됩니다.|  
|**부분**|**bit**|1 = **sp_serveroption\@sub** 가 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@sub** 가 **false** 또는 **off**로 설정 됩니다.|  
|**dist**|**bit**|1 = **sp_serveroption\@** 이 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@** 을 **false** 또는 **off**로 설정 합니다.|  
|**dpub가**|**bit**|1 = **sp_serveroption\@** 하는 경우 **true** 또는 **on**으로 설정 합니다.<br /><br /> 0 = **sp_serveroption\@dpub가** 가 **false** 또는 **off**로 설정 되어 있습니다.|  
|**rpcout**|**bit**|1 = **sp_serveroption\@rpc out** 이 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@rpc out** 이 **false** 또는 **off**로 설정 되어 있습니다.|  
|**dataaccess**|**bit**|1 = **sp_serveroption\@data access** 가 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@데이터 액세스가** **false** 또는 **off**로 설정 되어 있습니다.|  
|**collationcompatible**|**bit**|1 = **sp_serveroption\@데이터 정렬 호환** 이 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@데이터 정렬 호환** 이 **false** 또는 **off**로 설정 되어 있습니다.|  
|**컴퓨터**|**bit**|1 = **sp_serveroption\@시스템이** **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@시스템** 을 **false** 또는 **off**로 설정 합니다.|  
|**useremotecollation**|**bit**|1 = **sp_serveroption\@remote collation** 이 **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@원격 데이터 정렬이** **false** 또는 **off**로 설정 되어 있습니다.|  
|**lazyschemavalidation**|**bit**|1 = **sp_serveroption\@지연 스키마 유효성 검사가** **true** 또는 **on**으로 설정 되어 있습니다.<br /><br /> 0 = **sp_serveroption\@지연 스키마 유효성 검사** 를 **false** 또는 **off**로 설정 합니다.|  
|**부씩**|**sysname**|**데이터 정렬 이름 sp_serveroption\@** 설정 된 서버 데이터 정렬입니다.|  
|**비 sqlsub**|bit|0 = 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스입니다.<br /><br /> 1 = 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 아닙니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;&#40;호환성 뷰](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
