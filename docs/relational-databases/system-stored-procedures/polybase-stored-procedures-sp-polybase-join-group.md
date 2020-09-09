---
description: sp_polybase_join_group (Transact-sql)
title: sp_polybase_join_group | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 53db2ff3554c095832a6fa21accb061f2575c3d6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548390"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  확장 계산을 위해 PolyBase 그룹에 SQL Server 인스턴스를 계산 노드로 추가 합니다.  
  
 SQL Server 인스턴스에  [PolyBase](../../relational-databases/polybase/polybase-guide.md) 기능이 설치 되어 있어야 합니다.  PolyBase를 사용 하면 Hadoop 및 Azure blob storage와 같은 비 SQL Server 데이터 원본을 통합할 수 있습니다. 또한 [sp_polybase_leave_group &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)을 참조 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>인수  
 * \@ head_node_address* = N '*head_node_address*'  
 PolyBase 스케일 아웃 그룹의 SQL Server 헤드 노드를 호스트 하는 컴퓨터의 이름입니다. * \@ head_node_address* 은 nvarchar (255)입니다.  
  
 * \@ dms_control_channel_port* = dms_control_channel_port  
 헤드 노드 PolyBase 데이터 이동 서비스에 대 한 컨트롤 채널이 실행 되는 포트입니다. * \@ dms_control_channel_port* 는 서명 되지 않은 __int16입니다. 기본값은 **16450**입니다.  
  
 * \@ head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 PolyBase 스케일 아웃 그룹의 SQL Server 헤드 노드의 이름입니다. * \@ head_node_sql_server_instance_name* 은 nvarchar (16)입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 저장 프로시저를 실행 한 후 PolyBase 엔진을 종료 하 고 컴퓨터에서 PolyBase 데이터 이동 서비스를 다시 시작 합니다. 헤드 노드에서 실행 하는 다음 DMV를 확인 하려면 **dm_exec_compute_nodes**합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 현재 컴퓨터를 계산 노드로 PolyBase 그룹에 조인 합니다.  헤드 노드의 이름은 **HST01** 이 고 헤드 노드의 SQL Server 인스턴스 이름은 **MSSQLSERVER**입니다.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>관련 항목  
 [PolyBase 시작하기](../../relational-databases/polybase/get-started-with-polybase.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
