---
title: Data Migration Assistant에 대 한 설정 구성
description: 구성 파일에서 값을 업데이트 하 여 Data Migration Assistant에 대 한 설정을 구성 하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: fc280fa541e2a6b5ea984086d694ffdd3f7c39a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056538"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Data Migration Assistant에 대 한 설정 구성

Dma .exe .config 파일에서 구성 값을 설정 하 여 Data Migration Assistant의 특정 동작을 미세 조정할 수 있습니다. 이 문서에서는 키 구성 값에 대해 설명 합니다.

컴퓨터의 다음 폴더에서 Data Migration Assistant 데스크톱 응용 프로그램 및 명령줄 유틸리티에 대 한 dma .exe .config 파일을 찾을 수 있습니다.

- 데스크톱 응용 프로그램

  % ProgramFiles%\\Microsoft Data Migration Assistant\\ping.exe .config

- 명령줄 유틸리티

  % ProgramFiles%\\Microsoft Data Migration Assistant\\ 

변경 하기 전에 원래 구성 파일의 복사본을 저장 해야 합니다. 변경 후 새 구성 값을 적용 하려면 Data Migration Assistant을 다시 시작 합니다.

## <a name="number-of-databases-to-assess-in-parallel"></a>병렬로 평가할 데이터베이스 수

Data Migration Assistant는 여러 데이터베이스를 병렬로 평가 합니다. 평가 하는 동안 데이터베이스 스키마를 이해 하기 위해 dacpac (데이터 계층 응용 프로그램)를 추출 Data Migration Assistant 합니다.동일한 서버에 있는 여러 데이터베이스를 병렬로 평가 하는 경우이 작업의 시간이 초과 될 수 있습니다. 

Data Migration Assistant v2.0부터 parallelDatabases 구성 값을 설정 하 여이를 제어할 수 있습니다. 기본값은 8입니다.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>병렬로 마이그레이션할 데이터베이스 수

Data Migration Assistant는 로그인을 마이그레이션하기 전에 여러 데이터베이스를 병렬로 마이그레이션합니다. 마이그레이션 중에는 원본 데이터베이스의 백업을 수행 하 고, 필요에 따라 백업을 복사한 다음 대상 서버에서 복원 Data Migration Assistant 합니다. 마이그레이션을 위해 여러 데이터베이스를 선택 하면 시간 초과 오류가 발생할 수 있습니다. 

Data Migration Assistant v2.0부터이 문제가 발생 하는 경우 parallelDatabases 구성 값을 줄일 수 있습니다. 전체 마이그레이션 시간을 줄이기 위해 값을 늘릴 수 있습니다.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 설정

평가 하는 동안 데이터베이스 스키마를 이해 하기 위해 dacpac (데이터 계층 응용 프로그램)를 추출 Data Migration Assistant 합니다. 매우 큰 데이터베이스에 대 한 제한 시간이 초과 되거나 서버가 로드 중이면이 작업에 실패할 수 있습니다. Data Migration v1.0부터 다음 구성 값을 수정 하 여 오류를 방지할 수 있습니다. 

> [!NOTE]
> 전체 &lt;dacfx&gt; 항목은 기본적으로 주석 처리 됩니다. 주석을 제거한 다음 필요에 따라 값을 수정 합니다.

- commandTimeout

   이 매개 변수는 IDbCommand CommandTimeout 속성을 *초*단위로 설정 합니다.(기본값 = 60)

- databaseLockTimeout

   이 매개 변수는 [잠금\_제한 시간 제한\_기간](../t-sql/statements/set-lock-timeout-transact-sql.md) *(밀리초)* 을 설정 하는 것과 같습니다.(기본값 = 5000)

- maxDataReaderDegreeOfParallelism

  이 매개 변수는 사용할 SQL 연결 풀 연결 수를 설정 합니다.(기본값 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: 권장 사항 임계값

[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)를 사용 하면 Microsoft SQL Server 2016에서 Azure로 웜 및 콜드 트랜잭션 데이터를 동적으로 확장할 수 있습니다. Stretch Database은 많은 양의 콜드 데이터를 포함 하는 트랜잭션 데이터베이스를 대상으로 합니다. Stretch Database 권장 사항은 저장소 기능 권장 사항에서 먼저이 기능을 사용 하는 것으로 간주 되는 테이블을 식별 한 다음이 기능에 대해 테이블을 사용 하도록 설정 하기 위해 수행 해야 하는 변경 내용을 식별 합니다.

Data Migration Assistant v2.0부터 recommendedNumberOfRows 구성 값을 사용 하 여 Stretch Database 기능을 사용할 수 있도록 테이블에 대해이 임계값을 제어할 수 있습니다. 기본값은 10만 행입니다. 더 작은 테이블에 대 한 스트레치 기능을 분석 하려면 적절 한 값을 낮춥니다.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 연결 제한 시간

연결 제한 시간 값을 지정 된 시간 (초)으로 설정 하 여 평가 또는 마이그레이션을 실행 하는 동안 원본 및 대상 인스턴스의 [SQL 연결 시간 제한을](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) 제어할 수 있습니다. 기본값은 15초입니다.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>오류 코드 무시

각 규칙의 제목에는 오류 코드가 있습니다. 규칙이 필요 하지 않고 무시 하려면 ignoreErrorCodes 속성을 사용 합니다. 단일 오류 또는 여러 오류를 무시 하도록 지정할 수 있습니다. 여러 오류를 무시 하려면 세미콜론 (예: ignoreErrorCodes = "46010; 71501")을 사용 합니다. 기본값은 71501입니다 .이 값은 개체가 프로시저, 뷰 등의 시스템 개체를 참조할 때 식별 되는 확인 되지 않은 참조와 연결 되어 있습니다.

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>참고 항목

[다운로드 Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)
