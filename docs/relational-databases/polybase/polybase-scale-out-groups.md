---
title: PolyBase 스케일 아웃 그룹 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: polybase
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
caps.latest.revision: 20
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3fd249645266a7d9477e2dc098817138d8f722d0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="polybase-scale-out-groups"></a>PolyBase 스케일 아웃 그룹
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  PolyBase를 사용하는 독립 실행형 SQL Server 인스턴스는 Hadoop 또는 Azure Blob 저장소에서 대규모 데이터 집합을 처리하는 경우 성능상의 병목 지점이 될 수 있습니다. PolyBase 그룹 기능을 사용하면 SQL Server 인스턴스 클러스터를 만들어 Hadoop 또는 Azure Blob 저장소와 같은 외부 데이터 원본에서 쿼리 성능을 향상하기 위해 스케일 아웃 방식으로 대규모 데이터를 처리할 수 있습니다.  
  
 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md) 및 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)를 참조하세요.  
  
 ![PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase 스케일 아웃 그룹")  
  
## <a name="overview"></a>개요  
  
### <a name="head-node"></a>헤드 노드  
 헤드 노드는 PolyBase 쿼리가 제출되는 SQL Server 인스턴스를 포함합니다. 각 PolyBase 그룹은 헤드 노드를 하나만 가질 수 있습니다. 헤드 노드는 SQL Server 인스턴스에 있는 SQL 데이터베이스 엔진, PolyBase 엔진 및 PolyBase 데이터 이동 서비스의 논리적 그룹입니다.  
  
### <a name="compute-node"></a>계산 노드  
 계산 노드는 외부 데이터에서 확장 쿼리를 지원하는 SQL Server 인스턴스를 포함합니다. 계산 노드는 SQL Server 인스턴스에 있는 SQL Server 및 PolyBase 데이터 이동 서비스의 논리적 그룹입니다. PolyBase 그룹은 여러 계산 노드를 가질 수 있습니다.  헤드 노드와 계산 노드는 동일한 SQL Server 버전을 실행해야 합니다.
  
### <a name="distributed-query-processing"></a>분산형 쿼리 처리  
 PolyBase 쿼리는 헤드 노드에서 SQL Server로 전송됩니다. 외부 테이블을 참조하는 쿼리 부분은 PolyBase 엔진으로 분배됩니다.  
  
 PolyBase 엔진은 PolyBase 쿼리 뒤에 있는 주요 구성 요소입니다. 외부 데이터에 대한 쿼리 구문을 분석하고 쿼리 계획을 생성하며 작업을 계산 노드의 데이터 이동 서비스로 분배해 실행합니다. 작업이 완료되면 계산 노드에서 결과를 수신한 후 SQL Server로 전송하여 처리하고 클라이언트로 반환합니다.  
  
 PolyBase 데이터 이동 서비스는 PolyBase 엔진에서 지침을 수신하고 헤드 및 계산 노드의 SQL Server 인스터스 사이 및 HDFS 와 SQL Server 사이에서 데이터를 전송합니다.  
  
### <a name="editions-availability"></a>버전 가용성  
 SQL Server를 설치한 후에 인스턴스가 헤드 노드 또는 계산 노드로 지정될 수 있습니다.  실행 중인 SQL Server PolyBase의 버전에 따라 선택이 달라질 수 있습니다. Enterprise Edition 설치 시 인스턴스는 헤드 노드 또는 계산 노드로 지정될 수 있습니다. Standard Edition에서 인스턴스는 계산 노드로만 지정될 수 있습니다.  
  
## <a name="to-configure-a-polybase-group"></a>PolyBase 그룹을 구성하려면  
  
### <a name="prerequisites"></a>사전 요구 사항  
  
-   동일 도메인에 위치하는 N개의 시스템  
  
-   PolyBase 서비스를 실행하기 위한 도메인 사용자 계정  
  
### <a name="steps"></a>단계  
  
1.  N개의 컴퓨터에 PolyBase를 사용하는 동일한 버전의 SQL Server를 설치합니다.  
  
2.  SQL Server 인스턴스를 헤드 노드로 선택합니다. 헤드 노드는 SQL Server Enterprise를 실행하는 인스턴스에만 지정될 수 있습니다.  
  
3.  나머지 SQL Server 인스턴스를 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)을 사용하여 계산 노드로 추가합니다.  
  
4.  [sys.dm_exec_compute_nodes&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)를 사용하여 그룹에서 노드를 모니터링합니다.  
  
5.  (선택 사항) [sp_polybase_leave_group&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)을 사용하여 계산 노드를 제거합니다.  
  
## <a name="example-walk-through"></a>예제 연습  
 이 예제는 다음을 사용하여 PolyBase 그룹을 구성하는 단계를 보여줍니다.  
  
1.  	*PQTH4A* 도메인의 시스템 두 대. 시스템 이름:  
  
    -   PQTH4A-CMP01  
  
    -   PQTH4A-CMP02  
  
2.  도메인 계정: *PQTH4A\PolybaseUse*r  
  
#### <a name="step-1-install-sql-server-with-polybase-on-all-machines"></a>1단계: 모든 시스템에 PolyBase 사용하는 SQL Server 설치  
  
1.  setup.exe를 실행합니다.  
  
2.  기능 선택 페이지에서 **외부 데이터용 PolyBase 쿼리 서비스**를 선택합니다.  
  
3.  서버 구성 페이지에서 SQL Server PolyBase에 대한 **도메인 계정** PQTH4A\PolybaseUser 및 SQL Server PolyBase 데이터 이동 서비스를 사용합니다.  
  
4.  PolyBase 구성 페이지에서 **PolyBase 스케일 아웃 그룹의 일부로 SQL Server 인스턴스 사용**옵션을 선택합니다. 이 옵션은 PolyBase 서비스로 들어오는 연결을 허용하도록 방화벽을 엽니다.  
  
5.  설치가 완료된 후 **services.msc**를 실행합니다. SQL Server, PolyBase 엔진 및 PolyBase 데이터 이동 서비스가 실행 중인지 확인합니다.  
  
     ![PolyBase 서비스](../../relational-databases/polybase/media/polybase-services.png "PolyBase services")  
  
#### <a name="step-2-select-one-sql-server-as-head-node"></a>2단계: 헤드 노드로 하나의 SQL Server 선택  
  
-   설치가 완료 된 후 두 시스템 모두가 PolyBase 그룹 헤드 노드로 작동할 수 있습니다. 이 예제에서는 PQTH4A-CMP01의 “MSSQLSERVER”를 헤드 노드로 선택합니다.  
  
#### <a name="step-3-add-other-sql-server-instances-as-compute-nodes"></a>3단계: 다른 SQL Server 인스턴스를 계산 노드로 추가  
  
1.  PQTH4A-CMP02에서 SQL Server에 연결합니다.  
  
2.  저장 프로시저 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)을 실행합니다.  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
3.  계산 노드(PQTH4A-CMP02)에서 services.msc를 실행합니다.  
  
4.  PolyBase 엔진을 종료하고 PolyBase 데이터 이동 서비스를 다시 시작합니다.  
  
#### <a name="optional-remove-a-compute-node"></a>선택 사항: 계산 노드 제거  
  
1.  계산 노드 SQL Server(PQTH4A CMP02)에 연결합니다.  
  
2.  저장 프로시저 sp_polybase_leave_group을 실행합니다.  
  
    ```  
    EXEC sp_polybase_leave_group;  
    ```  
  
3.  제거 중인 계산 노드(PQTH4A-CMP02)에서 services.msc를 실행합니다.  
  
4.  PolyBase 엔진을 시작합니다. PolyBase 데이터 이동 서비스를 다시 시작합니다.  
  
5.  PQTH4A-CMP01에서 DMV sys.dm_exec_compute_nodes를 실행하여 노드가 제거되었는지 확인합니다. 이제, PQTH4A-CMP02가 독립 실행형 헤드 노드로 작동합니다.  
  
## <a name="next-steps"></a>다음 단계  
 문제를 해결하려면 [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)을(를) 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)   
 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase Connectivity Configuration&#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)  
  
  
