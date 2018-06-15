---
title: 구성 설정 (SQL Server 데이터 Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 4b42f816755b312f95609bd25ac6122b8fbf321c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32867208"
---
# <a name="configuration-settings-for-data-migration-assistant"></a>데이터 마이그레이션 길잡이 대 한 구성 설정

데이터 마이그레이션 길잡이 dma.exe.config 파일에서 구성 값을 사용 하 여의 특정 동작을 미세 조정할 수 있습니다. 이 문서에서는 키 구성 값을 설명 합니다.

컴퓨터에 다음 폴더에는 데이터 마이그레이션 길잡이 데스크톱 응용 프로그램 및 명령줄 유틸리티 dma.exe.config 파일을 찾을 수 있습니다.

- 데스크톱 응용 프로그램

  % ProgramFiles %\\Microsoft 데이터 마이그레이션 길잡이\\dma.exe.config

- 명령줄 유틸리티

  % ProgramFiles %\\Microsoft 데이터 마이그레이션 길잡이\\dmacmd.exe.config 

수정 하기 전에 원래 구성 파일의 복사본을 저장 해야 합니다. 변경한 후 데이터 마이그레이션 길잡이 새 구성 값에 대 한 내용을 적용 하려면 다시 시작 합니다.

## <a name="number-of-databases-to-assess-in-parallel"></a>동시에 평가 하는 데이터베이스 수

데이터 마이그레이션 길잡이 동시에 여러 데이터베이스를 평가합니다. 평가 중 데이터 Migration Assistant 추출 데이터 계층 응용 프로그램 데이터베이스 스키마를 이해 하려면 (dacpac) 합니다. 이 작업을 동시에 동일한 서버에 여러 데이터베이스를 평가 하는 경우 제한 시간을 수 있습니다. 

데이터 마이그레이션 길잡이 v 2.0을 시작 하면 제어가는 parallelDatabases 구성 값을 설정 하 여 됩니다. 기본값은 8입니다.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>병렬로 마이그레이션할 데이터베이스의 수

데이터 마이그레이션 길잡이 마이그레이션합니다 병렬로, 여러 데이터베이스 전에 마이그레이션 로그인 합니다. 마이그레이션하는 동안 데이터 Migration Assistant 원본 데이터베이스의 백업을 만들, 필요에 따라, 백업 복사한 다음 대상 서버에 복원 합니다. 마이그레이션에 대 한 여러 데이터베이스를 선택 하면 시간 초과 오류가 발생할 수 있습니다. 

이 문제가 발생 하면 데이터 마이그레이션 길잡이 v 2.0 부터는 parallelDatabases 구성 값을 줄일 수 있습니다. 전체 마이그레이션 시간을 줄이기 위해 값을 늘릴 수 있습니다.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 설정

평가 하는 동안 데이터 Migration Assistant 추출 데이터 계층 응용 프로그램 데이터베이스 스키마를 이해 하려면 (dacpac) 합니다. 매우 큰 데이터베이스에 대 한 시간 제한이 있는이 작업이 실패할 수 있습니다 또는 부하 상태에서 서버 없는 경우. 데이터 마이그레이션 v1.0 부터는 오류를 방지 하려면 다음과 같은 구성 값을 수정할 수 있습니다. 

> [!NOTE]
> 전체 &lt;dacfx&gt; 항목은 기본적으로 주석 처리 합니다. 메모를 제거 하 고 필요에 따라 다음 값을 수정 합니다.

- CommandTimeout

   이 옵션 IDbCommand.CommandTimeout 속성의 설정 *초*합니다. (기본값 = 60)

- databaseLockTimeout

   이에 해당 하는 [잠금 설정\_시간 제한 시간 초과\_기간 ](../t-sql/statements/set-lock-timeout-transact-sql.md) 에 *밀리초*합니다. (기본값 = 5000)

- maxDataReaderDegreeOfParallelism

   사용 하도록 SQL 연결 풀 연결의 수입니다. (기본값 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>스트레치 데이터베이스: 권장 임계값

와 [SQL Server 스트레치 데이터베이스](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), 웜 및 콜드 트랜잭션 데이터 Microsoft SQL Server 2016에서 Azure로 동적으로 늘릴 수 있습니다. 스트레치 데이터베이스 트랜잭션 데이터베이스 많은 양의 콜드 데이터를 대상으로 합니다. 저장소 기능 권장 구성에서 스트레치 데이터베이스 권장 사항에는 먼저 테이블 식별에서이 기능을 사용할 것으로 확인 하 고이 기능에 대 한 테이블을 사용 하도록 설정 하려면 수행 하는 변경 내용을 식별 합니다.

데이터 마이그레이션 길잡이 v 2.0 부터는 recommendedNumberOfRows 구성 값을 사용 하 여 스트레치 데이터베이스 기능을 받으려면 테이블에 대 한이 임계값을 제어할 수 있습니다. 기본값은 100, 000 행입니다. 더 작은 테이블에 대 한 스트레치 능력을 분석 하려는 경우 다음 값 보다 작으면 적절 하 게 합니다.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 연결 제한 시간

제어할 수 있습니다는 [SQL 연결 제한 시간](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) 시간 (초) 지정 된 수의 연결 제한 시간 값을 설정 하 여 평가 또는 마이그레이션을 실행 하는 동안 소스 및 대상 인스턴스에 대 한 합니다. 기본값은 15초입니다.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>참고 항목

[데이터 마이그레이션 길잡이 다운로드](https://www.microsoft.com/download/details.aspx?id=53595)
