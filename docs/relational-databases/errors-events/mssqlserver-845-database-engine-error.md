---
description: MSSQLSERVER_845
title: MSSQLSERVER_845 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b4d474714579397d18e22f2c32cc540ff30d5ac0
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618071"
---
# <a name="mssqlserver_845"></a>MSSQLSERVER_845
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|845|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|BUFLATCH_TIMEOUT|  
|메시지 텍스트|데이터베이스 ID %d, 페이지 %S_PGID에 대한 버퍼 래치 유형 %d을(를) 기다리는 중 시간이 초과되었습니다.|  
  
## <a name="explanation"></a>설명  
프로세스가 래치를 획득하려고 대기했지만, 제한 시간이 초과되어 래치를 획득하지 못했습니다. 이 오류는 일반적으로 시스템 프로세스를 차단하는 다른 태스크로 인해 I/O 작업을 완료하는 데 너무 많은 시간이 소요되는 경우 발생할 수 있습니다. 하드웨어 오류로 인해 이 오류가 발생하는 경우도 있습니다.  
  
## <a name="cause"></a>원인
이 오류 메시지는 시스템의 전체 환경에 따라 다릅니다. 다음 상황에서는 과도한 스트레스를 받는 시스템이 발생할 수 있습니다.

- I/O(입출력) 및 메모리 요구 사항을 충족하지 않는 하드웨어
- 부적절하게 구성되고 테스트된 설정
- 비효율적인 디자인

 시스템 과부하로 인해 워크로드 요구 사항을 충족할 수 없는 경우 845 오류가 발생할 수 있습니다. 스트레스를 받는 환경이 발생하는 가장 일반적인 원인은 다음과 같습니다.

- 하드웨어 문제
- 압축 볼륨
- 기본값이 아닌 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 설정
- 비효율적인 쿼리 또는 인덱스 디자인
- 잦은 데이터베이스 AutoGrow 또는 AutoShrink 작업

## <a name="user-action"></a>사용자 동작  
이 오류가 발생하는 것을 방지하려면 다음을 시도하십시오.  
  
- 하드웨어에 병목 상태가 있는지 확인합니다. 먼저 [Identifying Bottlenecks](../performance/identify-bottlenecks.md)(병목 현상 파악)를 참조하는 것이 좋습니다. 필요한 경우 환경의 구성, 쿼리 및 로드에 대한 요구 사항을 충족할 수 있도록 하드웨어를 업그레이드합니다.

- 모든 하드웨어가 제대로 작동하는지 확인합니다. 기록된 오류를 확인하고 하드웨어 공급업체에서 제공받은 진단 프로그램을 실행합니다. 오류 로그 또는 이벤트 로그에서 관련 I/O 오류를 검사하십시오. I/O 오류는 일반적으로 디스크 오류를 나타냅니다.  
- 디스크 볼륨이 압축되어 있지 않은지 확인합니다. 압축 드라이브에는 데이터 및 로그 파일을 저장할 수 없습니다. [데이터베이스 파일 및 파일 그룹](../databases/database-files-and-filegroups.md)을 참조하세요. 압축 드라이브 지원에 대한 자세한 내용은 [SQL Server Databases Not Supported on Compressed Volumes](https://support.microsoft.com/EN-US/help/231347)(SQL Server 데이터베이스가 압축 볼륨에서 지원되지 않음) 문서를 검토하세요.

- 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 옵션을 모두 끄면 오류 메시지가 사라지는지 확인합니다.
   - [우선 순위 높임 옵션](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)
   - [경량 풀링(파이버 모드) 옵션](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)
   - [작업 집합 크기 설정 옵션](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md)

    자세한 내용은 [HOW TO: Determine Proper SQL Server Configuration Settings](https://support.microsoft.com/EN-US/help/319942)(방법: 적절한 SQL Server 구성 설정 확인)를 참조하세요.

- 쿼리를 튜닝하여 시스템에 사용되는 리소스를 줄입니다. 성능을 튜닝하면 시스템의 스트레스가 줄어들고 개별 쿼리에 대한 응답 시간이 개선됩니다.
- AutoShrink 속성을 OFF로 설정하여 데이터베이스 크기 변경으로 인한 오버헤드를 줄입니다.
- AutoGrow 속성을 자주 발생하지 않을 만큼 큰 증분으로 설정합니다. 데이터베이스에서 사용 가능한 공간을 확인하는 작업을 예약한 다음, 사용량 감소 시 데이터베이스 크기를 늘립니다.
- 잠겨 있는 태스크 및 기타 오류에 대한 오류 로그를 검사하십시오. 이러한 오류는 기본 문제의 근본 원인일 수 있으므로 먼저 해결해야 합니다.
- 어설션과 같은 오류가 자주 발생하면 이 문제를 해결하세요.
- 845 오류 메시지가 자주 발생하지 않으면 오류를 무시해도 됩니다.