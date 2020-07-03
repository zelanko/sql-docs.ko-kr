---
title: sys. dm_clr_appdomains (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c3c0351bd541738e2540cc1a0624cf0ca9836c5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893984"
---
# <a name="sysdm_clr_appdomains-transact-sql"></a>sys.dm_clr_appdomains(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  서버의 각 애플리케이션 도메인에 대해 행을 반환합니다. 응용 프로그램 도메인 (**AppDomain**)은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 응용 프로그램에 대 한 격리 단위인 CLR (공용 언어 런타임)의 구문입니다. 이 뷰를 사용 하 여에서 실행 중인 CLR 통합 개체를 이해 하 고 문제를 해결할 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 CLR 통합의 관리되는 데이터베이스 개체 유형은 다양합니다. 이러한 개체에 대 한 일반적인 내용은 [CLR (공용 언어 런타임) 통합을 사용 하 여 데이터베이스 개체 작성](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)을 참조 하세요. 이러한 개체가 실행 될 때마다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 필요한 코드를 로드 하 고 실행할 수 있는 **AppDomain** 을 만듭니다. **Appdomain** 의 격리 수준은 데이터베이스당 데이터베이스당 하나의 **appdomain** 입니다. 즉, 사용자가 소유한 모든 CLR 개체는 항상 데이터베이스당 동일한 **AppDomain** 에서 실행 됩니다. 사용자가 다른 데이터베이스에 clr 데이터베이스 개체를 등록 하는 경우 clr 데이터베이스 개체는 다른 응용 프로그램 도메인에서 실행 됩니다. 코드 실행이 완료 된 후에는 **AppDomain** 이 제거 되지 않습니다. 나중에 실행하도록 메모리에 캐시됩니다. 이렇게 하면 성능이 향상됩니다.  
  
 자세한 내용은 [응용 프로그램 도메인](https://go.microsoft.com/fwlink/p/?LinkId=299658)을 참조 하세요.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|**AppDomain**의 주소입니다. 사용자가 소유 하는 모든 관리 되는 데이터베이스 개체는 항상 동일한 **AppDomain**에 로드 됩니다. 이 열을 사용 하 여 **dm_clr_loaded_assemblies**에서이 **AppDomain** 에 현재 로드 된 모든 어셈블리를 조회할 수 있습니다.|  
|**appdomain_id**|**int**|**AppDomain**의 ID입니다. 각 **AppDomain** 에는 고유한 ID가 있습니다.|  
|**appdomain_name**|**varchar (386)**|에 의해 할당 된 **AppDomain** 의 이름 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다.|  
|**creation_time**|**datetime**|**AppDomain** 이 생성 된 시간입니다. **Appdomain** 은 성능 향상을 위해 캐시 되 고 다시 사용 되기 때문에 **creation_time** 는 코드를 실행 하는 데 반드시 필요한 것은 아닙니다.|  
|**db_id**|**int**|이 **AppDomain** 이 생성 된 데이터베이스의 ID입니다. 서로 다른 두 데이터베이스에 저장 된 코드는 하나의 **AppDomain**을 공유할 수 없습니다.|  
|**user_id**|**int**|이 **AppDomain**에서 개체를 실행할 수 있는 사용자의 ID입니다.|  
|**상태**|**nvarchar(128)**|**AppDomain**의 현재 상태에 대 한 설명자입니다. AppDomain은 생성부터 삭제까지 여러 가지 상태를 가질 수 있습니다. 자세한 내용은 이 항목의 주의 섹션을 참조하십시오.|  
|**strong_refcount**|**int**|이 **AppDomain**에 대 한 강력한 참조 수입니다. 이는이 **AppDomain**을 사용 하는 현재 실행 중인 일괄 처리의 수를 반영 합니다. 이 뷰를 실행 하면 **강력한 refcount**가 생성 됩니다. 가 현재 실행 중인 코드가 없는 경우에도 **strong_refcount** 값은 1입니다.|  
|**weak_refcount**|**int**|이 **AppDomain**에 대 한 약한 참조 수입니다. 이는 **AppDomain** 내에서 캐시 되는 개체 수를 나타냅니다. 관리 되는 데이터베이스 개체를 실행 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 나중에 다시 사용할 수 있도록 **AppDomain** 내부에 캐시 합니다. 이렇게 하면 성능이 향상됩니다.|  
|**cost**|**int**|**AppDomain**의 비용입니다. 비용이 높을수록 메모리가 부족 하 여이 **AppDomain** 이 언로드될 가능성이 높아집니다. 비용은 일반적으로이 **AppDomain**을 다시 만드는 데 필요한 메모리 양에 따라 달라 집니다.|  
|**value**|**int**|**AppDomain**의 값입니다. 값이 낮을수록 메모리가 부족 하 여이 **AppDomain** 이 언로드될 가능성이 높습니다. 값은 일반적으로이 **AppDomain**을 사용 하는 연결 또는 일괄 처리의 수에 따라 달라 집니다.|  
|**total_processor_time_ms**|**bigint**|프로세스가 시작된 후 현재 애플리케이션 도메인에서 실행되는 동안 모든 스레드에서 사용되는 총 프로세서 시간(밀리초)입니다. 이는 **MonitoringTotalProcessorTime**에 해당 합니다.|  
|**total_allocated_memory_kb**|**bigint**|애플리케이션 도메인이 만들어진 후 수집된 메모리를 포함하여 해당 도메인에서 할당한 모든 메모리의 총 크기(KB)입니다. 이는 **MonitoringTotalAllocatedMemorySize**에 해당 합니다.|  
|**survived_memory_kb**|**bigint**|마지막 전체 차단 수집 후에도 유지되고 현재 애플리케이션 도메인에서 참조하는 것으로 알려진 KB 수입니다. 이는 **MonitoringSurvivedMemorySize**에 해당 합니다.|  
  
## <a name="remarks"></a>설명  
 **Dm_clr_appdomains appdomain_address** 와 **dm_clr_loaded_assemblies appdomain_address**사이에 일 대 일 관계가 있습니다.  
  
 다음 표에서는 가능한 **상태** 값, 해당 설명 및 **AppDomain** 수명 주기에서 발생 하는 시기를 나열 합니다. 이 정보를 사용 하 여 **appdomain** 의 수명 주기을 따르고 Windows 이벤트 로그를 구문 분석할 필요 없이 언로드 또는 반복적인 **AppDomain** 인스턴스 언로드를 감시할 수 있습니다.  
  
## <a name="appdomain-initialization"></a>AppDomain 초기화  
  
|시스템 상태|설명|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|**AppDomain** 을 만들고 있습니다.|  
  
## <a name="appdomain-usage"></a>AppDomain 사용  
  
|시스템 상태|설명|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|여러 사용자가 런타임 **AppDomain** 을 사용할 준비가 되었습니다.|  
|E_APPDOMAIN_SINGLEUSER|**AppDomain** 은 DDL 작업에서 사용할 준비가 되었습니다. 공유된 AppDomain이 DDL 작업이 아닌 CLR 통합 실행에 사용된다는 점에서 E_APPDOMAIN_SHARED와 다릅니다. 이러한 AppDomain은 동시에 실행되는 다른 작업과 격리됩니다.|  
|E_APPDOMAIN_DOOMED|**AppDomain** 이 언로드되기 위해 예약 되었지만 현재 스레드를 실행 하 고 있습니다.|  
  
## <a name="appdomain-cleanup"></a>AppDomain 정리  
  
|시스템 상태|설명|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 일반적으로 관리 되는 데이터베이스 개체를 포함 하는 어셈블리가 변경 되거나 삭제 되었기 때문에 CLR이 **AppDomain**을 언로드하기 위해 요청 했습니다.|  
|E_APPDOMAIN_UNLOADED|CLR이 **AppDomain**을 언로드 했습니다. 이는 일반적으로 **Threadabort**, **OutOfMemory**또는 사용자 코드의 처리 되지 않은 예외로 인 한 에스컬레이션 프로시저의 결과입니다.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|**AppDomain** 이 CLR에서 언로드 되었으며에 의해 소멸 되도록 설정 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|E_APPDOMAIN_DESTROY|**AppDomain** 이에 의해 소멸 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다.|  
|E_APPDOMAIN_ZOMBIE|**Appdomain** 이에 의해 소멸 되었지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **appdomain** 에 대 한 모든 참조가 정리 되지 않았습니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 지정 된 어셈블리에 대 한 **AppDomain** 의 세부 정보를 보는 방법을 보여 줍니다.  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 다음 예제에서는 지정 된 **AppDomain**의 모든 어셈블리를 보는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [dm_clr_loaded_assemblies &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [공용 언어 런타임 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
