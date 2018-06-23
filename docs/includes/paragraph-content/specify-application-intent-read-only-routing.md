---
title: 파일 포함
description: 파일 포함
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 842a7377bcd6bdcb649a78b2f31eb66de95bc5a3
ms.sourcegitcommit: a98ed7872afc055c65aa9697d571f8b300f6eeb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313399"
---
## <a name="specifying-application-intent"></a>응용 프로그램 의도 지정

키워드 **ApplicationIntent** 연결 문자열에 지정할 수 있습니다. 할당 가능한 값은 **ReadWrite** 또는 **ReadOnly**합니다. 기본값은 **ReadWrite**합니다.

때 **ApplicationIntent = ReadOnly**, 클라이언트가 연결할 때 읽기 작업을 요청 합니다. 서버 연결 시 및 시 의도 적용 한 **사용** 문을 데이터베이스입니다.

**ApplicationIntent** 키워드는 레거시 읽기 전용 데이터베이스와 함께 작동 하지 않습니다.  


#### <a name="targets-of-readonly"></a>읽기 전용의 대상

연결을 선택 하는 경우 **읽기 전용**, 연결에는 데이터베이스에 대 한 존재할 수 있는 다음과 같은 특별 한 구성 중 하나에 할당 됩니다.

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 데이터베이스 허용 하거나 차단할 수는 대상된 Alwayson 데이터베이스에 대 한 읽기 작업입니다. 여기에서이 선택한을 사용 하 여 제어 되는 **ALLOW_CONNECTIONS** 절은 **PRIMARY_ROLE** 및 **SECONDARY_ROLE** Transact SQL 문입니다.

- [지리적 복제](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [읽기 확장](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

사용할 수 있는 특별 한 대상의 항목이 없으면 일반 데이터베이스에서 읽습니다.

&nbsp;

**ApplicationIntent** 키워드를 사용 하면 *읽기 전용 라우팅*합니다.


## <a name="read-only-routing"></a>읽기 전용 라우팅

읽기 전용 라우팅은 데이터베이스의 읽기 전용 복제 가용성을 보장할 수 있는 기능입니다. 읽기 전용 라우팅을 사용 하도록 설정 하려면 다음의 모든 적용:

- AlwaysOn 가용성 그룹의 가용성 그룹 수신기에 연결해야 합니다.

- **ApplicationIntent** 연결 문자열 키워드는 **ReadOnly**로 설정해야 합니다.

- 읽기 전용 라우팅을 설정하려면 데이터베이스 관리자가 가용성 그룹을 구성해야 합니다.

다중 연결 사용 하 여 읽기 전용 라우팅을 모두 동일한 읽기 전용 복제본에 연결할 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청을 동일한 읽기 전용 복제본에 연결을 확인할 수 있습니다. 확인 하 여이 sameness *하지* 가용성 그룹 수신기에 전달 된 **서버** 연결 문자열 키워드입니다. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.

읽기 전용 라우팅 주 데이터베이스에 연결할 때 보다 더 오래 걸릴 수 있습니다. 긴 대기 읽기 전용 라우팅은 먼저 주 서버에 연결 하기 때문 이며 가장 읽기 가능한 보조를 찾습니다. 이러한 여러 staps 인해 30 초 이상 사용자 로그인 제한 시간을 늘려야 합니다.

