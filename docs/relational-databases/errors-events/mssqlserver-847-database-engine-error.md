---
title: MSSQLSERVER_847 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 847 (Database Engine error)
ms.assetid: 67208b7c-bd8d-48a1-9f70-a6488e0f5f9b
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d639c8e451ef71fd5e52c7bc3ae4d3f33336775
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326944"
---
# <a name="mssqlserver847"></a>MSSQLSERVER_847
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|847|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|해당 사항 없음|  
|메시지 텍스트|래치를 기다리는 동안 시간이 초과되었습니다. 클래스 '%ls', ID %p, 유형 %d, 태스크 0x%p : %d, 대기 시간 %d, 플래그 0x%I64x, 소유 태스크 0x%p. 계속 대기합니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 버퍼 래치 오류를 쓸 때 컴퓨터가 응답하지 않거나(중지), 시간이 초과되거나, 일반 작업의 다른 장애가 발생할 수 있습니다.  
  
메시지의 상태 필드에 값 0x04가 설정되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 I/O 작업을 기다리고 있는 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 [MSSQLSERVER_833](~/relational-databases/errors-events/mssqlserver-833-database-engine-error.md) 메시지가 표시될 수도 있습니다.  
  
메시지의 상태 필드에 값 0x04가 해제되어 있는 경우 페이지에 경합 문제가 있는 것입니다. 개체가 데이터 페이지인 경우 이 오류는 비효율적인 코드 디자인으로 인해 발생할 수 있습니다. 페이지가 데이터가 아닌 경우에는 부족한 하드웨어 리소스 등으로 인해 서버 병목 현상이 일어나 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 문제를 해결하려면 사용자 환경에 따라 다음 단계 중 하나 이상을 수행하여 오류 메시지를 줄이거나 오류 메시지가 표시되지 않도록 하십시오.  
  
-   하드웨어에 병목 상태가 있는지 확인합니다. 필요한 경우 사용자 환경의 구성, 쿼리 및 부하 요구 사항을 지원할 수 있도록 하드웨어를 업그레이드합니다. 병목 상태에 대한 자세한 내용은 [병목 상태 식별](~/relational-databases/performance/identify-bottlenecks.md)을 참조하세요.  
  
-   기록된 오류를 확인하고 하드웨어 공급업체에서 제공받은 진단 프로그램을 실행합니다.  
  
-   디스크 드라이브가 압축되어 있지 않은지 확인합니다. 압축된 드라이브에는 데이터 또는 로그 파일을 저장할 수 없습니다. 물리적 파일에 대한 자세한 내용은 [데이터베이스 파일 및 파일 그룹](~/relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.  
  
-   다음 옵션 설정을 해제하는 경우 오류 메시지가 사라지는지 확인합니다.  
  
    -   SQL Server priority boost 구성 옵션  
  
    -   lightweight pooling(파이버 모드) 옵션  
  
    -   set working set size 옵션  
  
    > [!NOTE]  
    > 기본 설정인 OFF에서 다른 값으로 변경하면 이전 설정의 성능이 저하될 수 있습니다. 설정에 대한 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)을 참조하세요.  
  
-   쿼리를 튜닝하여 시스템에 사용되는 리소스를 줄입니다. 성능을 튜닝하면 시스템의 스트레스가 줄어들고 개별 쿼리에 대한 응답 시간이 개선됩니다.  
  
-   AUTO_SHRINK 옵션을 OFF로 설정하여 데이터베이스 크기 변경으로 인한 오버헤드를 줄입니다.  
  
-   FILEGROWTH 옵션을 파일 증가가 자주 발생하지 않을 증가값으로 설정합니다. 또한 데이터베이스에서 사용 가능한 공간을 확인하는 작업을 예약한 다음 사용률이 낮은 시간에 데이터베이스 크기를 늘립니다.  
  
