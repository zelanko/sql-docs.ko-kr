---
title: affinity mask 서버 구성 옵션
description: SQL Server의 선호도 마스크 옵션에 대해 알아봅니다. 프로세서를 특정 스레드에 바인딩하는 데 사용하는 예제를 살펴봅니다.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 94f8406af013bc0720bc16063d1a9881eda94c5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715593"
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask 서버 구성 옵션

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)][ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)을 대신 사용합니다.

멀티태스킹을 수행하기 위해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows는 서로 다른 프로세서 간에 프로세스 스레드를 이동하기도 합니다. 운영 체제 측면에서는 효율적이지만 각 프로세서 캐시에 데이터가 반복적으로 다시 로드되어 시스템 로드가 많은 경우 이 활동으로 인해 SQL Server 성능이 저하될 수 있습니다. 프로세서를 특정 스레드에 할당하면 프로세서를 다시 로드해야 하는 필요성을 없애고 프로세서 간의 스레드 마이그레이션을 줄여 컨텍스트 전환을 줄일 수 있으므로 이러한 상황에서 성능을 향상시킬 수 있습니다. 이러한 스레드와 프로세서 간 연결을 프로세서 선호도라고 합니다.

SQL Server에서는 두 가지 선호도 마스크 옵션인 선호도 마스크(**CPU 선호도 마스크**라고도 함)와 선호도 I/O 마스크를 통해 프로세서 선호도를 지원합니다. 선호도 I/O 마스크 옵션에 대한 자세한 내용은 [선호도 입력-출력 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)을 참조하세요. 33-64개 프로세서가 있는 서버에 대한 CPU 및 I/O 선호도를 지원하려면 [affinity64 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 및 [affinity64 입력-출력 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)을 추가로 사용해야 합니다.

> [!NOTE]  
> 33개에서 64개의 프로세서를 가지는 서버에 대한 선호도 지원은 64비트 운영 체제에서만 가능합니다.

이전 버전의 SQL Server에 있던 선호도 마스크 옵션은 CPU 선호도를 동적으로 제어하는 역할을 했습니다.

SQL Server에서는 SQL Server 인스턴스를 다시 시작하지 않고도 선호도 마스크 옵션을 구성할 수 있습니다. sp_configure를 사용하는 경우 구성 옵션을 설정한 후 RECONFIGURE 또는 RECONFIGURE WITH OVERRIDE를 실행해야 합니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 사용하는 경우 선호도 마스크 옵션을 변경하면 시스템을 다시 시작해야 합니다.

선호도 마스크는 동적으로 변경되므로 SQL Server에서 프로세스 스레드를 바인딩할 CPU 스케줄러를 요청 시 시작 및 종료할 수 있습니다. 이는 서버 조건이 변경될 때 발생합니다. 예를 들어 서버에 SQL Server의 새 인스턴스를 추가하는 경우 선호도 마스크 옵션을 조정하여 프로세서 부하를 다시 분산시켜야 할 수도 있습니다.

선호도 비트마스크를 수정하려면 SQL Server에서 새 CPU 스케줄러를 설정하고 기존 CPU 스케줄러를 해제해야 합니다. 그런 다음 새 스케줄러나 남아 있는 스케줄러에서 새 일괄 처리를 처리할 수 있습니다.

새 CPU 스케줄러를 시작하려면 SQL Server에서 새 스케줄러를 만들어 이 서버의 표준 스케줄러 목록에 추가합니다. 새 스케줄러는 새로 들어오는 일괄 처리에만 사용됩니다. 현재 일괄 처리는 동일한 스케줄러에서 계속 실행됩니다. 작업자가 사용 가능해지거나 새로 생성될 때 새 스케줄러로 마이그레이션됩니다.

스케줄러를 종료하려면 스케줄러에서 모든 일괄 처리 동작을 완료하고 일괄 처리를 종료해야 합니다. 종료된 스케줄러는 새 일괄 처리가 예약되지 않도록 오프라인으로 표시됩니다.

새 스케줄러를 추가하거나 제거해도 모니터 잠금, 검사점, 시스템 태스크 스레드(처리 DTC) 및 신호 처리 같은 영구 시스템 태스크는 서버가 작동하는 동안 스케줄러에서 계속 실행됩니다. 이러한 영구 시스템 태스크는 동적으로 마이그레이션되지 않습니다. 이러한 시스템 태스크의 프로세서 로드를 스케줄러에 다시 배포하려면 SQL Server 인스턴스를 다시 시작해야 합니다. SQL Server에서 영구 시스템 태스크와 연결된 스케줄러를 종료하려 하면 해당 태스크는 오프라인 스케줄러에서 계속 실행됩니다(마이그레이션 없음). 이 스케줄러는 수정된 선호도 마스크로 프로세서에 바인딩되며 변경하기 전에 바인딩된 프로세서로 로드를 할당하지 않습니다. 오프라인 스케줄러를 추가할 경우 시스템 로드에 큰 영향을 주지 않아야 합니다. 그럴 경우 수정된 선호도 마스크로 사용 가능한 스케줄러에서 이러한 작업을 다시 구성하려면 데이터베이스 서버를 다시 부팅해야 합니다.

SQL Server의 '선호도 마스크' 및 '선호도 I/O 마스크' 구성 값을 동일한 CPU를 사용하도록 설정하지 마세요. SQL Server 작업자 스레드 예약 및 I/O 처리 모두를 위해 프로세서를 바인딩하는 경우 성능이 저하될 수 있습니다. 따라서 구성 값이 동일한 프로세서에 대해 설정되지 않았는지 확인해야 합니다. 'affinity64 마스크' 및 'affinity64 I/O 마스크'에도 동일한 권장 사항이 적용됩니다.  선호도 마스크와 선호도 IO 마스크가 겹치지 않도록 하기 위해 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) 명령은 일반 CPU 및 I/O 선호도가 상호 배타적인지 확인합니다. 그렇지 않으면 클라이언트 세션과 SQL Server 오류 로그에 해당 설정이 권장 구성이 아님을 나타내는 오류 메시지가 보고됩니다.

```sql
 Msg 5834, Level 16, State 1, Line 1
 The affinity mask specified conflicts with the IO affinity mask specified. Use the override option to force this configuration
```

RECONFIGURE WITH OVERRIDE 옵션을 실행하면 CPU 및 I/O 선호도를 상호 배타적이지 않게 사용할 수 있습니다.  

I/O 선호도 태스크(예: 지연 기록기 및 로그 작성기)는 I/O 선호도 마스크로부터 직접 영향을 받습니다. 지연 기록기 및 로그 작성기 태스크가 바인딩되지 않으면 잠금 모니터 또는 검사점 같은 다른 영구 태스크에 대해 정의된 규칙을 그대로 따릅니다.
존재하지 않는 CPU로 매핑을 시도하는 선호도 마스크를 지정하면 RECONFIGURE 명령은 클라이언트 세션과 SQL Server 오류 로그에 모두 오류 메시지를 보고합니다. 이 경우 RECONFIGURE WITH OVERRIDE 옵션을 사용해도 영향을 미치지 않으며 동일한 구성 오류가 다시 보고됩니다.

Windows 운영 체제에 의한 특정 워크로드 할당에서 SQL Server 작업을 제외할 수도 있습니다. 프로세서를 나타내는 비트를 1로 설정하면 스레드를 할당하도록 SQL Server 데이터베이스 엔진이 해당 프로세서를 선택합니다. **선호도 마스크**를 0(기본값)으로 설정하면 Microsoft Windows 예약 알고리즘이 스레드의 선호도를 설정합니다. **선호도 마스크**를 0이 아닌 값으로 설정하면 SQL Server 선호도가 선택 가능한 프로세서를 지정하는 비트 마스크로 이 값을 해석합니다.  

특정 프로세서에서 실행되는 SQL Server 스레드를 분리하면 Microsoft Windows에서는 시스템의 Windows 관련 프로세스 처리를 보다 잘 평가할 수 있습니다. 예를 들어 인스턴스 A와 인스턴스 B라는 두 개의 SQL Server 인스턴스를 실행하고 CPU가 8개인 서버에서 시스템 관리자는 선호도 마스크 옵션을 사용하여 CPU 4개로 구성된 첫째 집합을 인스턴스 A에 할당하고 나머지 4개의 둘째 집합을 인스턴스 B에 할당할 수 있습니다. 32개 이상의 프로세서를 구성하려면 선호도 마스크 및 affinity64 마스크를 모두 설정해야 합니다. **선호도 마스크** 의 값은 다음과 같습니다.

- 1바이트 **선호도 마스크** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 8개까지 허용됩니다.

- 2바이트 **선호도 마스크** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 16개까지 허용됩니다.

- 3바이트 **선호도 마스크** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 24개까지 허용됩니다.

- 4바이트 **선호도 마스크** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 32개까지 허용됩니다.

- 32개보다 많은 CPU를 허용하려면 처음 32개 CPU에 대해 4바이트 affinity mask를 구성하고 나머지 CPU에 대해 최대 4바이트 affinity64 mask를 구성합니다.

SQL Server 프로세서 선호도 설정은 특수 작업이므로 필요한 경우에만 사용하는 것이 좋습니다. 대부분의 경우 Microsoft Windows 기본 선호도는 최상의 성능을 제공합니다. 선호도 마스크를 설정할 때 다른 애플리케이션의 CPU 요구 사항을 고려해야 합니다. 자세한 내용은 Windows 운영 체제 설명서를 참조하십시오.

> [!NOTE]
> Windows 시스템 모니터를 사용하여 각 프로세서 사용량을 확인 및 분석할 수 있습니다.

선호도 I/O 마스크 옵션을 지정할 때는 선호도 마스크 구성 옵션과 함께 사용해야 합니다. 그러나 앞서 언급한 대로 **선호도 마스크** 스위치 및 선호도 I/O 마스크 옵션 모두에서 동일한 CPU를 설정하지 마세요. 각 CPU에 해당하는 비트 상태는 다음과 같은 상태 중 하나여야 합니다.

- affinity mask 옵션과 affinity I/O mask 옵션에서 모두 0입니다.

- affinity mask 옵션에서는 1이고 affinity I/O mask 옵션에서는 0입니다.

- affinity mask 옵션에서는 0이고 affinity I/O mask 옵션에서는 1입니다.

> [!CAUTION]
> Windows 운영 체제에서 CPU 선호도를 구성하지 말고 SQL Server에서도 선호도 마스크를 구성하지 마세요. 동일한 결과를 얻기 위해 이렇게 설정하는 경우도 있지만 구성이 일치하지 않는 경우 예상치 못한 결과가 나올 수 있습니다. SQL Server CPU 선호도는 SQL Server의 sp_configure 옵션을 사용하여 구성하는 것이 가장 좋습니다.

## <a name="example"></a>예제

선호도 마스크 옵션 설정의 예로, 비트가 1, 2, 5 위치에서 1로 설정되어 있고 0, 3, 4, 6, 7 위치에서 0으로 설정되어 있는 상태에서 프로세서 1, 2, 5를 선택할 수 있고 16진수 값 0x26 또는 이에 해당하는 10진수 값 38이 지정되었다고 가정해 봅시다. 비트 위치는 오른쪽에서 왼쪽으로 번호가 매겨집니다.

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'affinity mask', 38;
RECONFIGURE;
GO
```

다음은 CPU가 8개인 시스템의 **선호도 마스크** 값입니다.  

|10진수 값|이진수 비트 마스크|프로세서의 SQL Server 스레드 허용|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 및 1|  
|7|00000111|0, 1 및 2|  
|15|00001111|0, 1, 2, 3|  
|31|00011111|0, 1, 2, 3, 4|  
|63|00111111|0, 1, 2, 3, 4, 5|  
|127|01111111|0, 1, 2, 3, 4, 5, 6|  
|255|11111111|0, 1, 2, 3, 4, 5, 6, 7|  

affinity mask는 고급 옵션입니다. sp_configure 시스템 저장 프로시저를 사용하여 설정을 변경하는 경우 **고급 옵션 표시**가 1로 설정되어 있을 때만 **선호도 마스크**를 변경할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 명령을 실행하면 SQL Server 인스턴스를 다시 시작하지 않더라도 새 설정이 즉시 적용됩니다.  

## <a name="non-uniform-memory-access-numa"></a>NUMA(Non-Uniform Memory Access)

하드웨어 기반 NUMA(Non-uniform Memory Access)를 사용하고 선호도 마스크가 설정되어 있으면 노드의 모든 스케줄러가 해당 CPU에 바인딩됩니다. 선호도 마스크가 설정되어 있지 않으면 각 스케줄러는 NUMA 노드 내의 CPU 그룹에 바인딩되고 NUMA 노드 N1로 매핑된 스케줄러에서 노드의 모든 CPU 작업을 예약할 수 있지만 다른 노드와 연결된 CPU 작업은 예약할 수 없습니다.  

단일 NUMA 노드에서 실행되는 모든 작업은 해당 노드의 버퍼 페이지만 사용할 수 있습니다. 작업이 여러 노드의 CPU에서 병렬로 실행되는 경우 관련된 모든 노드의 메모리를 사용할 수 있습니다.  
  
## <a name="licensing-issues"></a>라이선스 문제

동적 선호도는 CPU 라이선스에 의해 엄격한 제약을 받습니다. SQL Server는 라이선스 정책을 위반하는 선호도 마스크 옵션의 구성을 허용하지 않습니다.  

### <a name="startup"></a>시작

지정된 선호도 마스크가 SQL Server 시작 시 또는 데이터베이스 연결 시 라이선스 정책을 위반하면 엔진 계층에서는 시작 프로세스나 데이터베이스 연결/복원 작업을 완료한 후에 선호도 마스크의 sp_configure 실행 값을 0으로 되돌리므로 SQL Server 오류 로그에 오류 메시지가 보고됩니다.  
  
### <a name="reconfigure"></a>다시 구

[!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 명령을 실행할 때 지정된 선호도 마스크가 라이선스 정책을 위반하면 클라이언트 세션과 SQL Server 오류 로그에 오류 메시지가 보고되므로 데이터베이스 관리자는 해당 선호도 마스크를 다시 구성해야 합니다. 이 경우 RECONFIGURE WITH OVERRIDE 명령은 사용할 수 없습니다.  

## <a name="next-steps"></a>다음 단계

- [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
- [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
- [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)
