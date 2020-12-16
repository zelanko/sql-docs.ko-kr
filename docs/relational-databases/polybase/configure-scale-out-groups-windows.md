---
title: Windows에서 PolyBase 스케일 아웃 그룹 구성 | Microsoft Docs
description: PolyBase 스케일 아웃 그룹을 설정하여 SQL Server 인스턴스 클러스터를 만듭니다. 이렇게 하면 외부 원본에서 가져온 대량 데이터 세트의 쿼리 성능이 향상됩니다.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: tutorial
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 1592632bdeca9f8c3cdceeb61b06c1bd92550f53
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477924"
---
# <a name="configure-polybase-scale-out-groups-on-windows"></a>Windows에서 PolyBase 스케일 아웃 그룹 구성

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

이 문서에서는 Windows에서 [PolyBase 스케일 아웃 그룹](polybase-scale-out-groups.md)을 설정하는 방법을 설명합니다. 이렇게 하면 SQL Server 인스턴스 클러스터를 만들어 Hadoop 또는 Azure Blob Storage와 같은 외부 데이터 원본에서 쿼리 성능을 향상하기 위해 스케일 아웃 방식으로 대규모 데이터를 처리할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항
  
- 동일한 도메인에 둘 이상의 시스템이 있음  
  
- PolyBase 서비스를 실행하기 위한 도메인 사용자 계정  
  
## <a name="process-overview"></a>프로세스 개요

다음 단계에서는 PolyBase 스케일 아웃 그룹을 만들기 위한 프로세스를 간략하게 설명합니다. 다음 섹션에서는 각 단계의 보다 자세한 연습 과정을 제공합니다.
  
1. N개의 컴퓨터에 PolyBase를 사용하는 동일한 버전의 SQL Server를 설치합니다.
  
2. SQL Server 인스턴스를 헤드 노드로 선택합니다. 
  
3. 나머지 SQL Server 인스턴스를 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)을 사용하여 컴퓨팅 노드로 추가합니다.

4. [sys.dm_exec_compute_nodes&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)를 사용하여 그룹에서 노드를 모니터링합니다.

5. (선택 사항) [sp_polybase_leave_group&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)을 사용하여 컴퓨팅 노드를 제거합니다.

## <a name="example-walk-through"></a>예제 연습

이 예제는 다음을 사용하여 PolyBase 그룹을 구성하는 단계를 보여줍니다.  
  
1. *PQTH4A* 도메인의 시스템 두 대. 시스템 이름:  
  
   - PQTH4A-CMP01  
  
   - PQTH4A-CMP02  
  
2. 도메인 계정: *PQTH4A\PolyBaseUse* r  

## <a name="install-sql-server-with-polybase-on-all-machines"></a>모든 시스템에 PolyBase 사용하는 SQL Server 설치

1. setup.exe를 실행합니다.
  
2. 기능 선택 페이지에서 **외부 데이터용 PolyBase 쿼리 서비스** 를 선택합니다.
  
3. 서버 구성 페이지에서 SQL Server PolyBase 엔진 및 SQL Server PolyBase 데이터 이동 서비스에 대해 PQTH4A\PolyBaseUser **도메인 계정** 을 사용합니다.
  
4. PolyBase 구성 페이지에서 **PolyBase 스케일 아웃 그룹의 일부로 SQL Server 인스턴스 사용** 옵션을 선택합니다. 이 옵션은 PolyBase 서비스로 들어오는 연결을 허용하도록 방화벽을 엽니다. 헤드 노드가 명명된 인스턴스인 경우 헤드 노드의 Windows 방화벽에 SQL Server 포트를 수동으로 추가하고 헤드 노드에서 SQL Browser를 시작해야 합니다.
  
5. 설치가 완료된 후 **services.msc** 를 실행합니다. SQL Server, PolyBase 엔진 및 PolyBase 데이터 이동 서비스가 실행 중인지 확인합니다.
  
   ![PolyBase 서비스](../../relational-databases/polybase/media/polybase-services.png "PolyBase 서비스")  
  
## <a name="select-one-sql-server-as-head-node"></a>헤드 노드로 하나의 SQL Server 선택  
  
설치가 완료 된 후 두 시스템 모두가 PolyBase 그룹 헤드 노드로 작동할 수 있습니다. 이 예제에서는 PQTH4A-CMP01의 "MSSQLSERVER"를 헤드 노드로 선택합니다.
  
## <a name="add-other-sql-server-instances-as-compute-nodes"></a>다른 SQL Server 인스턴스를 컴퓨팅 노드로 추가  
  
1. PQTH4A-CMP02에서 SQL Server에 연결합니다.
  
2. 저장 프로시저 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)을 실행합니다.

   ```sql
   -- Enter head node details:
   -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';
   ```  

3. 컴퓨팅 노드(PQTH4A-CMP02)에서 services.msc를 실행합니다.
  
4. PolyBase 엔진을 종료하고 PolyBase 데이터 이동 서비스를 다시 시작합니다.

> [!NOTE] 
> 헤드 노드에서 Polybase 엔진 서비스를 다시 시작하거나 중지하는 경우, DMS(데이터 이동 서비스) 서비스는 DMS와 DW(Polybase 엔진 서비스) 간의 통신 채널이 닫히는 즉시 중지됩니다. DW 엔진을 두 번 넘게 다시 시작하는 경우, DMS는 90분 대기 기간으로 전환되며 다음에 자동 시작이 시도될 때까지 90분간 기다려야 합니다. 이 경우에는 모든 노드에서 해당 서비스를 수동으로 시작해야 합니다.

## <a name="optional-remove-a-compute-node"></a>선택 사항: 컴퓨팅 노드 제거  
  
1. 컴퓨팅 노드 SQL Server(PQTH4A CMP02)에 연결합니다.
  
2. 저장 프로시저 sp_polybase_leave_group을 실행합니다.
  
    ```sql  
    EXEC sp_polybase_leave_group;  
    ```  
  
3. 제거 중인 컴퓨팅 노드(PQTH4A-CMP02)에서 services.msc를 실행합니다.
  
4. PolyBase 엔진을 시작합니다. PolyBase 데이터 이동 서비스를 다시 시작합니다.
  
5. PQTH4A-CMP01에서 DMV sys.dm_exec_compute_nodes를 실행하여 노드가 제거되었는지 확인합니다. 이제, PQTH4A-CMP02가 독립 실행형 헤드 노드로 작동합니다.  
  
## <a name="next-steps"></a>다음 단계  

문제를 해결하려면 [PolyBase troubleshooting with dynamic management views](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))을(를) 참조하십시오.
  
PolyBase에 대한 자세한 내용은 [PolyBase 개요](../../relational-databases/polybase/polybase-guide.md)를 참조하세요.