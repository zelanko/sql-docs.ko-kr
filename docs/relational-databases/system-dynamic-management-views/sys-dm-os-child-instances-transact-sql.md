---
title: sys.dm_os_child_instances (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66f4d8c770cc10c2ba47769576d8f9625edac0cf
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmoschildinstances-transact-sql"></a>sys.dm_os_child_instances(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  부모 서버 인스턴스에서 생성된 각 사용자 인스턴스당 한 개의 행을 반환합니다.  
  
> **중요!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 반환 되는 정보 **sys.dm_os_child_instances** 각 사용자 인스턴스 (heart_beat)의 상태를 확인 하 고 사용자에 대 한 연결을 만드는 데 사용할 수 있는 파이프 이름 (instance_pipe_name)를 사용할 수 있습니다 사용 하 여 인스턴스 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 SQLCmd 합니다. 클라이언트 응용 프로그램과 같은 외부 프로세스에 의해 시작된 다음에만 사용자 인스턴스에 연결할 수 있습니다. SQL 관리 도구에서는 사용자 인스턴스를 시작할 수 없습니다.  
  
> **참고:** 사용자 인스턴스는의 기능 [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] 만 합니다.  
  
> **참고** 로 표현에서 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_child_instances**합니다.  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|이 사용자 인스턴스의 사용자 이름입니다.|  
|owning_principal_sid|nvarchar(256)|이 사용자 인스턴스를 소유하는 보안 주체의 SID(보안 ID)입니다. 이는 Windows SID와 일치합니다.|  
|owning_principal_sid_binary|varbinary(85)|사용자 인스턴스를 소유하는 사용자에 대한 SID 이진 버전입니다.|  
|**instance_name**|**nvarchar(128)**|사용자 인스턴스의 이름입니다.|  
|**instance_pipe_name**|**nvarchar(260)**|사용자 인스턴스를 만들 때 응용 프로그램 연결을 위해 명명된 파이프를 만듭니다. 이 이름은 이 사용자 인스턴스에 연결할 연결 문자열에서 사용할 수 있습니다.|  
|**os_process_id**|**Int**|이 사용자 인스턴스에 대한 Windows 프로세스의 프로세스 번호입니다.|  
|**os_process_creation_date**|**날짜/시간**|이 사용자 인스턴스 프로세스가 마지막으로 시작된 날짜 및 시간입니다.|  
|**heart_beat**|**nvarchar(5)**|이 사용자 인스턴스의 현재 상태(연결 또는 연결 끊김)입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 동적 관리 뷰에 대 한 자세한 내용은 참조 하십시오. [동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목:  
 [비관리자 용 사용자 인스턴스](http://msdn.microsoft.com/en-us/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



