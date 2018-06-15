---
title: sp_polybase_join_group | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 927c07456401bf441e3ad6491111bad6c85e3c19
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33237492"
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  PolyBase 규모 확장 계산에 대 한 그룹에는 계산 노드로만 SQL Server 인스턴스를 추가합니다.  
  
 SQL Server 인스턴스에 있어야는 [PolyBase](../../relational-databases/polybase/polybase-guide.md) 기능이 설치 되어 있습니다.  PolyBase는 Hadoop 및 Azure blob 저장소 등의 SQL Server 이외 데이터 원본에 통합할 수 있습니다. 참고 항목 [sp_polybase_leave_group &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>인수  
 *@head_node_address* = N'*head_node_address*'  
 PolyBase 규모 확장 그룹의 헤드 노드 SQL Server를 호스팅하는 컴퓨터의 이름입니다. *@head_node_address* nvarchar (255)가입니다.  
  
 *@dms_control_channel_port* dms_control_channel_port =  
 헤드 노드에서 PolyBase 데이터 이동 서비스에 대 한 컨트롤 채널 실행 되 고 있는 포트입니다. *@dms_control_channel_port* 부호 없는 __int16이입니다. 기본값은 **16450**합니다.  
  
 *@head_node_sql_server_instance_name* head_node_sql_server_instance_name =  
 PolyBase 확장 그룹의 헤드 노드에 SQL Server 인스턴스의 이름입니다. *@head_node_sql_server_instance_name* nvarchar(16)가입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 저장된 프로시저를 실행 한 후 PolyBase 엔진을 종료 하 고 시스템에 PolyBase 데이터 이동 서비스를 다시 시작 합니다. 확인 하려면 다음 DMV는 헤드 노드에서 실행: **sys.dm_exec_compute_nodes**합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 PolyBase 그룹에는 계산 노드로만 현재 컴퓨터를 조인합니다.  헤드 노드의 이름은 **HST01** 헤드 노드에서 SQL Server 인스턴스의 이름이 **MSSQLSERVER**합니다.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 시작하기](../../relational-databases/polybase/get-started-with-polybase.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
