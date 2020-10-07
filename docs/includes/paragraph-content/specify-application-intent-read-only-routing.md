---
title: 포함 파일
description: 포함 파일
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: a443b615a6a04b588ed6dc84c6a8a4f6ed12e2f0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726762"
---
## <a name="specifying-application-intent"></a>애플리케이션 의도 지정

**ApplicationIntent** 키워드를 연결 문자열에 지정할 수 있습니다. 할당 가능한 값은 **ReadWrite** 또는 **ReadOnly**입니다. 기본값은 **ReadWrite**입니다.

**ApplicationIntent=ReadOnly**이면 클라이언트는 연결할 때 읽기 워크로드를 요청합니다. 서버는 연결 시 그리고 **USE** 데이터베이스 문 실행 중에 의도를 강제 적용합니다.

**ApplicationIntent** 키워드는 레거시 읽기 전용 데이터베이스에 적용되지 않습니다.  


#### <a name="targets-of-readonly"></a>ReadOnly의 대상

연결이 **ReadOnly**를 선택하면 데이터베이스에 대해 존재할 수 있는 다음 특수 구성 중 하나에 연결이 할당됩니다.

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 데이터베이스는 대상 Always On 데이터베이스에 대한 읽기 워크로드를 허용하거나 허용하지 않을 수 있습니다. 이 선택은 **PRIMARY_ROLE**의 **ALLOW_CONNECTIONS** 절과 **SECONDARY_ROLE** Transact-SQL 문을 사용하여 제어됩니다.

- [지역에서 복제](/azure/sql-database/sql-database-geo-replication-overview)

- [읽기 확장](/azure/sql-database/sql-database-read-scale-out)

이러한 특수 대상을 사용할 수 없는 경우 일반 데이터베이스를 읽습니다.

&nbsp;

**ApplicationIntent** 키워드는 *읽기 전용 라우팅*을 사용하도록 설정하는 데 사용됩니다.


## <a name="read-only-routing"></a>읽기 전용 라우팅

읽기 전용 라우팅은 데이터베이스의 읽기 전용 복제 가용성을 보장할 수 있는 기능입니다. 읽기 전용 라우팅을 사용하도록 설정하려면 다음 모두를 적용해야 합니다.

- AlwaysOn 가용성 그룹의 가용성 그룹 수신기에 연결해야 합니다.

- **ApplicationIntent** 연결 문자열 키워드는 **ReadOnly**로 설정해야 합니다.

- 읽기 전용 라우팅을 설정하려면 데이터베이스 관리자가 가용성 그룹을 구성해야 합니다.

읽기 전용 라우팅을 사용하는 여러 연결 중 일부가 동일한 읽기 전용 복제본에 연결되지 않을 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청이 동일한 읽기 전용 복제본에 연결되도록 할 수 있습니다. 가용성 그룹 수신기를 **서버** 연결 문자열 키워드에 전달하지 *않음*으로써 이 동일성을 확인합니다. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.

읽기 전용 라우팅은 주 복제본에 연결하는 것보다 시간이 더 오래 걸릴 수 있습니다. 대기 시간이 긴 이유는 읽기 전용 라우팅은 먼저 주 복제본에 연결한 다음, 가장 잘 읽을 수 있는 보조 복제본을 찾기 때문입니다. 이러한 여러 단계 때문에 로그인 제한 시간을 30초 이상으로 늘려야 합니다.