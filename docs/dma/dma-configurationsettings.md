---
title: Data Migration Assistant (SQL Server)에 대 한 설정 구성 | Microsoft Docs
description: 구성 파일의 값을 업데이트 하 여 Data Migration Assistant에 대 한 설정을 구성 하는 방법에 알아봅니다.
ms.custom: ''
ms.date: 08/29/2018
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
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 79d32d9d1ceb60e3cb3433bd5d9d5a06c9976403
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152804"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Data Migration Assistant에 대 한 설정 구성

Dma.exe.config 파일에서 구성 값을 설정 하 여 Data Migration Assistant의 특정 동작을 미세 조정할 수 있습니다. 이 문서에서는 키 구성 값을 설명 합니다.

Data Migration Assistant 데스크톱 응용 프로그램 및 명령줄 유틸리티에 대 한 컴퓨터에서 다음 폴더에 dma.exe.config 파일을 찾을 수 있습니다.

- 데스크톱 응용 프로그램

  % ProgramFiles %\\Microsoft Data Migration Assistant\\dma.exe.config

- 명령줄 유틸리티

  % ProgramFiles %\\Microsoft Data Migration Assistant\\dmacmd.exe.config 

수정 하기 전에 원래 구성 파일의 복사본을 저장 해야 합니다. 구성을 변경한 후 Data Migration Assistant 새 구성 값에 대 한 내용을 적용 하려면 다시 시작 합니다.

## <a name="number-of-databases-to-assess-in-parallel"></a>병렬로 평가 하는 데이터베이스 수

Data Migration Assistant는 동시에 여러 데이터베이스를 평가합니다. 평가 하는 동안 Data Migration Assistant 추출 데이터 계층 응용 프로그램 (dacpac) 데이터베이스 스키마를 이해 합니다. 이 작업 병렬로 동일한 서버의 여러 데이터베이스를 평가 하는 경우 제한 시간을 수 있습니다. 

Data Migration Assistant v2.0부터,이 수 있습니다 제어는 parallelDatabases 구성 값을 설정 하 여 합니다. 기본값은 8입니다.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>병렬로 마이그레이션할 데이터베이스의 수

Data Migration Assistant 마이그레이션합니다 동시에 여러 데이터베이스 전에 마이그레이션 로그인 합니다. 마이그레이션하는 동안 Data Migration Assistant 원본 데이터베이스의 백업을, 필요에 따라 백업 복사 되며 다음 대상 서버에 복원 합니다. 마이그레이션에 대 한 여러 데이터베이스를 선택 하면 시간 제한 오류를 발생할 수 있습니다. 

이 문제가 발생 하는 경우 Data Migration Assistant v2.0부터 parallelDatabases 구성 값을 줄일 수 있습니다. 전체 마이그레이션 시간을 줄이기 위해 값을 늘릴 수 있습니다.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 설정

평가 하는 동안 Data Migration Assistant 추출 데이터 계층 응용 프로그램 (dacpac) 데이터베이스 스키마를 이해 합니다. 매우 큰 데이터베이스에 대 한 제한 시간을 사용 하 여이 작업이 실패할 수 있습니다 또는 서버 부하가 경우. 데이터 마이그레이션 v1.0부터 오류를 방지 하려면 다음 구성 값을 수정할 수 있습니다. 

> [!NOTE]
> 전체 &lt;dacfx&gt; 항목은 기본적으로 주석으로 처리 합니다. 주석을 제거 하 고 필요에 따라 다음 값을 수정 합니다.

- commandTimeout

   IDbCommand.CommandTimeout 속성을 설정 하는이 *초*합니다. (기본값 = 60)

- databaseLockTimeout

   같습니다 [잠금을 설정\_제한 시간 초과\_기간 ](../t-sql/statements/set-lock-timeout-transact-sql.md) 에서 *밀리초*합니다. (기본값 = 5000)

- maxDataReaderDegreeOfParallelism

   사용 하도록 SQL 연결 풀 연결 횟수입니다. (기본값 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: 권장 임계값

사용 하 여 [SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), 웜 및 콜드 트랜잭션 데이터를 Microsoft SQL Server 2016에서 Azure로 동적으로 확장할 수 있습니다. Stretch Database 트랜잭션 데이터베이스를 대용량의 콜드 데이터가 있습니다. 저장소 기능 권장 사항에서 Stretch Database 권장 사항에는 먼저 테이블을 식별 것으로 생각 하는 것이 좋고에서이 기능 및이 기능에 대 한 테이블을 사용 하도록 설정 되어야 하는 변경 내용을 식별 합니다.

Data Migration Assistant v2.0부터 recommendedNumberOfRows 구성 값을 사용 하 여 Stretch Database 기능에 대 한 정하는 데 테이블에 대 한이 임계값을 제어할 수 있습니다. 기본값은 100,000 개 행입니다. 더 작은 테이블에 대 한 확장 기능을 분석 하려는 경우 다음 낮은 값을 적절 하 게 합니다.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 연결 시간 제한

제어할 수 있습니다.는 [SQL 연결 시간 제한](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) 시간 (초) 지정 된 수의 연결 제한 시간 값을 설정 하 여 평가 또는 마이그레이션을 실행 하는 동안 원본 및 대상 인스턴스에 대 한 합니다. 기본값은 15초입니다.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>참고자료

[Data Migration Assistant 다운로드](https://www.microsoft.com/download/details.aspx?id=53595)
