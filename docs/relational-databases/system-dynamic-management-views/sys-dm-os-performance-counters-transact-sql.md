---
title: sys. dm_os_performance_counters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c7b4d78f73af003e93bc662f10f1f95acda2b6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265708"
---
# <a name="sysdm_os_performance_counters-transact-sql"></a>sys.dm_os_performance_counters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  서버에서 유지되는 각 성능 카운터에 대해 행을 반환합니다. 각 성능 카운터에 대 한 자세한 내용은 [SQL Server 개체 사용](../../relational-databases/performance-monitor/use-sql-server-objects.md)을 참조 하세요.  
  
> [!NOTE]  
>  또는 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 이름 **sys. dm_pdw_nodes_os_performance_counters**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar (128)**|이 카운터가 속한 범주입니다.|  
|**counter_name**|**nchar (128)**|카운터의 이름입니다. 카운터에 대 한 자세한 정보를 얻기 위해 사용 중인 카운터 목록에서 선택할 항목의 이름 [SQL Server 개체](../../relational-databases/performance-monitor/use-sql-server-objects.md)입니다. |  
|**instance_name**|**nchar (128)**|카운터의 특정 항목 이름입니다. 대개 데이터베이스 이름이 포함됩니다.|  
|**cntr_value**|**bigint**|카운터의 현재 값입니다.<br /><br /> **참고:** 초 단위 카운터의 경우이 값은 누적 됩니다. 따라서 특정한 시간 간격으로 값을 샘플링하여 비율 값을 계산해야 합니다. 임의의 연속된 두 샘플 값 간의 차이는 사용된 시간 간격에 대한 비율과 동일합니다.|  
|**cntr_type**|**int**|Windows 성능 아키텍처가 정의한 카운터의 유형입니다. 성능 카운터 유형에 대 한 자세한 내용은 문서 또는 Windows Server 설명서의 [WMI 성능 카운터 형식](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-performance-counter-types) 을 참조 하세요.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 설치 인스턴스가 Windows 운영 체제의 성능 카운터를 표시하지 못하면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 성능 카운터가 사용할 수 없도록 설정되었는지 확인합니다.  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 0개의 행이 반환되면 성능 카운터가 사용할 수 없도록 설정된 것입니다. 이 경우 설치 로그에서 오류 3409 "이 인스턴스의 sqlctr.ini를 다시 설치하고, 인스턴스 로그인 계정에 올바른 레지스트리 사용 권한이 있는지 확인하십시오."가 있는지 확인합니다.  이 오류는 성능 카운터가 사용할 수 있도록 설정되지 않았음을 나타냅니다. 3409 오류 바로 앞에 있는 오류는 성능 카운터를 사용할 수 있도록 설정하지 못한 근본 원인을 나타내야 합니다. 설치 로그 파일에 대 한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조 하세요.  
  
## <a name="permission"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
 
## <a name="examples"></a>예  
 다음 예제에서는 성능 카운터 값을 반환합니다.  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>참고 항목  
  [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


