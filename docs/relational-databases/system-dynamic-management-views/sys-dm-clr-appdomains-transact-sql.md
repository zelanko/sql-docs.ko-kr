---
title: sys.dm_clr_appdomains (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b164c253f9e1bc90f65e143ef3490a4cca9542ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681711"
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버의 각 응용 프로그램 도메인에 대해 행을 반환합니다. 응용 프로그램 도메인 (**AppDomain**)의 구조 이며 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR (공용 언어 런타임) 응용 프로그램에 대 한 격리 단위입니다. 이 보기를 사용 하 여 이해 하 고 CLR 통합 개체에서 실행 하는 문제 해결 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 CLR 통합의 관리되는 데이터베이스 개체 유형은 다양합니다. 이러한 개체에 대 한 일반적인 정보를 참조 하세요 [공용 언어 런타임 (CLR) 통합을 사용 하 여 데이터베이스 개체 작성](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)합니다. 이러한 개체가 실행 될 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만듭니다는 **AppDomain** 있는 로드 고 필요한 코드를 실행 합니다. 에 대 한 격리 수준을 **AppDomain** 하나인 **AppDomain** 소유자 마다 데이터베이스당 합니다. 즉, 사용자가 소유한 모든 CLR 개체는 항상 동일한 실행 **AppDomain** 데이터베이스별 (다른 데이터베이스에 CLR 데이터베이스 개체는 다른 응용 프로그램 도메인에서 실행에 CLR 데이터베이스 개체를 등록 하는 사용자) 경우입니다. **AppDomain** 코드가 실행 완료 된 후 제거 되지 않습니다. 나중에 실행하도록 메모리에 캐시됩니다. 이 성능을 향상 시킵니다.  
  
 자세한 내용은 [응용 프로그램 도메인](http://go.microsoft.com/fwlink/p/?LinkId=299658)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|주소를 **AppDomain**합니다. 관리 되는 모든 데이터베이스 사용자가 소유 하는 개체가 동일한 항상 로드 됩니다 **AppDomain**합니다. 이 현재 로드 된 모든 어셈블리를 조회 하려면이 열을 사용할 수 있습니다 **AppDomain** 에 **sys.dm_clr_loaded_assemblies**합니다.|  
|**appdomain_id**|**int**|ID를 **AppDomain**합니다. 각 **AppDomain** 고유 ID가 있습니다.|  
|**appdomain_name**|**varchar(386)**|이름을 합니다 **AppDomain** 에 의해 할당 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**creation_time**|**datetime**|시간을 **AppDomain** 생성 되었습니다. 때문에 **Appdomain** 가 캐시 되 고 성능 향상을 위해 다시 **creation_time** 은 반드시 코드를 실행 하면 시간이 아닙니다.|  
|**db_id**|**int**|이 데이터베이스의 ID **AppDomain** 생성 되었습니다. 서로 다른 두 데이터베이스에 저장 된 코드 하나를 공유할 수 없습니다 **AppDomain**합니다.|  
|**user_id**|**int**|이 실행할 수 있는 개체 사용자의 ID **AppDomain**합니다.|  
|**state**|**nvarchar(128)**|현재 상태에 대 한 설명자를 **AppDomain**합니다. AppDomain은 생성부터 삭제까지 여러 가지 상태를 가질 수 있습니다. 자세한 내용은 이 항목의 주의 섹션을 참조하십시오.|  
|**strong_refcount**|**int**|이에 대 한 강력한 참조 횟수 **AppDomain**합니다. 현재 실행 하 고이 사용 하는 일괄 처리의 수를 반영 **AppDomain**합니다. 이 보기의 실행에서는 만듭니다는 **강력한 refcount**경우에; 현재 실행 중인 코드가 없습니다 **strong_refcount** 1의 값이 포함 됩니다.|  
|**weak_refcount**|**int**|이에 대 한 약한 참조 수가 **AppDomain**합니다. 내부 개체 수를 나타냅니다이 **AppDomain** 캐시 됩니다. 관리 되는 데이터베이스 개체를 실행할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 캐시 합니다 **AppDomain** 나중에 다시 사용에 대 한 합니다. 이 성능을 향상 시킵니다.|  
|**cost**|**int**|비용을 **AppDomain**합니다. 비용이 높을수록, 가능성이이 **AppDomain** 언로드될 메모리가 중 됩니다. 비용은 일반적으로이 다시 만들려면 얼마나 많은 메모리가 필요에 따라 달라 집니다 **AppDomain**합니다.|  
|**value**|**int**|값을 **AppDomain**합니다. 값이 작을수록, 가능성이이 **AppDomain** 언로드될 메모리가 중 됩니다. 값 일반적으로 얼마나 많은 연결 또는 일괄 처리는 사용 하 여이에 따라 달라 집니다 **AppDomain**합니다.|  
|**total_processor_time_ms**|**bigint**|프로세스가 시작된 후 현재 응용 프로그램 도메인에서 실행되는 동안 모든 스레드에서 사용되는 총 프로세서 시간(밀리초)입니다. 이 설정은 **System.AppDomain.MonitoringTotalProcessorTime**합니다.|  
|**total_allocated_memory_kb**|**bigint**|응용 프로그램 도메인이 만들어진 후 수집된 메모리를 포함하여 해당 도메인에서 할당한 모든 메모리의 총 크기(KB)입니다. 이 설정은 **System.AppDomain.MonitoringTotalAllocatedMemorySize**합니다.|  
|**survived_memory_kb**|**bigint**|마지막 전체 차단 수집 후에도 유지되고 현재 응용 프로그램 도메인에서 참조하는 것으로 알려진 KB 수입니다. 이 설정은 **System.AppDomain.MonitoringSurvivedMemorySize**합니다.|  
  
## <a name="remarks"></a>Remarks  
 사이는 하나 있습니다 관계가 **dm_clr_appdomains.appdomain_address** 하 고 **dm_clr_loaded_assemblies.appdomain_address**합니다.  
  
 다음 표에 가능한 **상태** 값, 해당 설명에서 발생 하는 경우 및 합니다 **AppDomain** 수명 주기입니다. 이 정보를 사용 하 여의 감시할 수 있습니다는 **AppDomain** 심 쩍 거 나 반복적인를 조사 하 고 **AppDomain** 인스턴스 언로드를 Windows 이벤트 로그를 구문 분석할 필요 없이 합니다.  
  
## <a name="appdomain-initialization"></a>AppDomain 초기화  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|합니다 **AppDomain** 만들어집니다.|  
  
## <a name="appdomain-usage"></a>AppDomain 사용  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|런타임에서 **AppDomain** 여러 사용자가 사용할 준비가 되었습니다.|  
|E_APPDOMAIN_SINGLEUSER|합니다 **AppDomain** DDL 작업에 사용할 준비가 되었습니다. 공유된 AppDomain이 DDL 작업이 아닌 CLR 통합 실행에 사용된다는 점에서 E_APPDOMAIN_SHARED와 다릅니다. 이러한 AppDomain은 동시에 실행되는 다른 작업과 격리됩니다.|  
|E_APPDOMAIN_DOOMED|**AppDomain** 언로드되도록 되도록 예약 되어 있지만 현재 실행 스레드 있습니다.|  
  
## <a name="appdomain-cleanup"></a>AppDomain 정리  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR가 언로드를 요청 합니다 **AppDomain**이므로 일반적으로 관리 되는 데이터베이스 개체를 포함 하는 어셈블리가 변경 되거나 삭제 되었으므로 합니다.|  
|E_APPDOMAIN_UNLOADED|CLR가 언로드 합니다 **AppDomain**합니다. 이로 인해는 에스컬레이션 프로시저의 결과 일반적으로 **ThreadAbort**를 **OutOfMemory**, 또는 사용자 코드에서 처리 되지 않은 예외입니다.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|합니다 **AppDomain** CLR에서 언로드 되었으며 의해 소멸 설정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|E_APPDOMAIN_DESTROY|합니다 **AppDomain** 하 여 소멸 될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|E_APPDOMAIN_ZOMBIE|**AppDomain** 에 의해 제거 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하지만, 일부에 대 한 참조를 **AppDomain** 정리 되었습니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는의 세부 정보를 보는 방법에는 **AppDomain** 지정된 된 어셈블리에 대 한 합니다.  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 다음 예제에서는 모든 어셈블리를 보는 방법에는 주어진 **AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_clr_loaded_assemblies &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [공용 언어 런타임 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
