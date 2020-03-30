---
title: 확장성 아키텍처
description: 이 문서에서는 SQL Server에서 R 또는 Python과 같은 외부 스크립트를 실행하기 위한 확장성 프레임워크의 아키텍처에 대해 설명합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb92f92ffb8239a6cf20b0f39dfb8f546b521a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727684"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 확장성 아키텍처 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server에는 서버에서 R 또는 Python과 같은 외부 스크립트를 실행하기 위한 확장성 프레임워크가 있습니다. 이 스크립트는 언어 런타임 환경에서 핵심 데이터베이스 엔진에 대한 확장으로 실행됩니다.

## <a name="background"></a>배경

확장성 프레임워크는 R 런타임을 지원하기 위해 SQL Server 2016에 도입되었습니다. SQL Server 2017 이상에서는 Python을 지원합니다.

확장성 프레임워크의 목적은 SQL Server와 데이터 과학 언어(예: R 및 Python) 간에 인터페이스를 제공하는 것입니다. 목표는 데이터 과학 솔루션을 프로덕션으로 이동할 때 마찰을 줄이고 개발 프로세스 중에 노출되는 데이터를 보호하는 것입니다. 데이터베이스 관리자는 SQL Server에서 관리하는 보안 프레임워크 내에서 신뢰할 수 있는 스크립팅 언어를 실행하여 데이터 과학자가 엔터프라이즈 데이터에 액세스할 수 있도록 허용하는 동시에 보안을 유지할 수 있습니다.

다음 다이어그램에서는 확장 가능한 아키텍처의 기회와 이점을 시각적으로 설명합니다.

  ![SQL Server와의 통합 목표](../media/ml-service-value-add.png "Machine Learning Services 값 추가")

저장 프로시저를 호출하여 외부 스크립트를 실행할 수 있으며, 결과는 테이블 형식으로 SQL Server에 직접 반환됩니다. 이렇게 하면 SQL 쿼리를 보내고 결과를 처리할 수 있는 모든 애플리케이션에서 기계 학습을 생성하거나 사용할 수 있습니다.

+ 외부 스크립트 실행에는 SQL Server 데이터 보안이 적용됩니다. 외부 스크립트를 실행하는 사용자는 SQL 쿼리에서 동일하게 사용할 수 있는 데이터에만 액세스할 수 있습니다. 권한 부족으로 인해 쿼리가 실패하면 동일한 사용자가 실행한 스크립트도 같은 이유로 실패합니다. SQL Server 보안은 테이블, 데이터베이스 및 인스턴스 수준에서 적용됩니다. 데이터베이스 관리자는 사용자 액세스, 외부 스크립트에서 사용하는 리소스 및 서버에 추가된 외부 코드 라이브러리를 관리할 수 있습니다.  

+ 크기 조정 및 최적화 기회에는 데이터베이스 플랫폼(ColumnStore 인덱스, [리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md))을 통한 이득과 확장 관련 이득(예: R 및 Python용 Microsoft 라이브러리가 데이터 과학 모델에 사용되는 경우)이라는 두 가지 근거가 있습니다. R은 단일 스레드이지만, RevoScaleR 함수는 다중 스레드이며 워크로드를 여러 코어에 분산시킬 수 있습니다.

+ 배포는 SQL Server 방법론을 사용합니다. 이러한 방법론은 PREDICT와 같은 함수를 호출하는 외부 스크립트, 기본 제공 SQL 또는 T-SQL 쿼리를 래핑하여 서버에 유지되는 예측 모델의 결과를 반환하는 저장 프로시저일 수 있습니다.

+ 특정 도구 및 IDE에 입증된 기술을 보유한 개발자는 이러한 도구에서 코드를 작성한 다음, 해당 코드를 SQL Server에 이식할 수 있습니다.

## <a name="architecture-diagram"></a>아키텍처 다이어그램

이 아키텍처는 외부 스크립트가 SQL Server와는 별도의 프로세스에서 실행되도록 설계되었지만, SQL Server에서 데이터와 작업에 대한 요청 체인을 내부적으로 관리하는 구성 요소를 사용합니다. SQL Server 버전에 따라 지원되는 언어 확장에는 [R](extension-r.md), [Python](extension-python.md) 및 Java 및 .NET과 같은 타사 언어가 포함됩니다.

  ***Windows의 구성 요소 아키텍처:***
  
  ![Windows 구성 요소 아키텍처](../media/generic-architecture-windows.png "구성 요소 아키텍처")
  
  ***Linux의 구성 요소 아키텍처:***

  ![Linux 구성 요소 아키텍처](../media/generic-architecture-linux.png "구성 요소 아키텍처")
  
구성 요소에는 외부 런타임과 라이브러리 관련 논리를 호출하여 인터프리터와 라이브러리를 로드하는 데 사용되는 **실행 패드** 서비스가 포함됩니다. 시작 관리자는 언어 런타임과 모든 독점 모듈을 로드합니다. 예를 들어 코드에 RevoScaleR 함수가 포함된 경우 RevoScaleR 인터프리터가 로드됩니다. **BxlServer** 및 **SQL Satellite**는 SQL Server와의 통신 및 데이터 전송을 관리합니다. 

Linux에서 SQL은 **실행 패드** 서비스를 사용하여 각 사용자에 대한 별도의 실행 패드 프로세스와 통신합니다.

<a name="launchpad"></a>

## <a name="launchpad"></a>실행 패드

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 전체 텍스트 인덱싱 및 쿼리 서비스에서 전체 텍스트 쿼리를 처리하기 위해 별도의 호스트를 시작하는 것과 비슷한 방식으로 외부 스크립트를 관리하고 실행하는 서비스입니다. 실행 패드 서비스는 Microsoft에서 게시하거나 Microsoft에서 성능 및 리소스 관리 요구 사항을 충족시키는 것으로 인증한 신뢰할 수 있는 시작 관리자만 시작할 수 있습니다.

| 신뢰할 수 있는 시작 관리자 | 내선 번호 | SQL Server 버전 |
|-------------------|-----------|---------------------|
| Windows용 R 언어에 대한 RLauncher.dll | [R 확장](extension-r.md) | SQL Server 2016 이상 |
| Windows용 Python 3.5에 대한 Pythonlauncher.dll | [Python 확장](extension-python.md) | SQL Server 2017 이상 |
| Linux용 R 언어에 대한 RLauncher.so | [R 확장](extension-r.md) | SQL Server 2019 이상 |
| Linux용 Python 3.5에 대한 Pythonlauncher.so | [Python 확장](extension-python.md) | SQL Server 2019 이상 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 자체 사용자 계정으로 실행됩니다. 실행 패드를 실행하는 계정을 변경하는 경우 SQL Server 구성 관리자를 사용하여 변경 내용이 관련 파일에 기록되도록 해야 합니다.

Windows에서는 SQL Server Machine Learning Services를 추가한 각 데이터베이스 엔진 인스턴스마다 별도의 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스가 만들어집니다. 각 데이터베이스 엔진 인스턴스마다 하나의 실행 패드 서비스가 있으므로 외부 스크립트를 지원하는 여러 인스턴스가 있는 경우 각 인스턴스에 대한 실행 패드 서비스가 제공됩니다. 데이터베이스 엔진 인스턴스는 해당 인스턴스에 대해 만들어진 실행 패드 서비스에 바인딩됩니다. 저장 프로시저 또는 T-SQL에서 외부 스크립트를 호출할 때마다 SQL Server 서비스에서 동일한 인스턴스에 대해 만들어진 실행 패드 서비스를 호출합니다.

작업을 지원되는 특정 언어로 실행하기 위해 실행 패드는 풀에서 보안 작업자 계정을 가져오고, 외부 런타임을 관리하는 위성 프로세스를 시작합니다. 각 위성 프로세스는 실행 패드의 사용자 계정을 상속하고, 스크립트 실행 기간 동안 해당 작업자 계정을 사용합니다. 스크립트에서 병렬 프로세스를 사용하는 경우 동일한 단일 작업자 계정에서 만들어집니다.

Linux에서는 하나의 데이터베이스 엔진 인스턴스만 지원되며, 이 인스턴스에 바인딩되는 하나의 실행 패드 서비스가 있습니다. 스크립트가 실행되면 실행 패드 서비스에서 권한이 낮은 **mssql_satellite** 사용자 계정을 사용하여 별도의 실행 패드 프로세스를 시작합니다. 각 위성 프로세스는 실행 패드의 mssql_satellite 사용자 계정을 상속하고, 스크립트 실행 기간 동안 해당 계정을 사용합니다.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 및 SQL Satellite

**BxlServer**는 Microsoft에서 제공하고 SQL Server와 언어 런타임 간의 통신을 관리하는 실행 파일입니다. 외부 스크립트 세션을 포함하는 데 사용되는 Windows용 Windows 작업 개체 또는 Linux용 네임스페이스를 만듭니다. 또한 각 외부 스크립트 작업에 대한 보안 작업 폴더를 프로비저닝하고, SQL Satellite를 사용하여 외부 런타임과 SQL Server 간의 데이터 전송을 관리합니다. 작업이 실행되는 동안 [프로세스 탐색기](https://technet.microsoft.com/sysinternals/processexplorer.aspx)를 실행하는 경우 하나 이상의 BxlServer 인스턴스가 표시될 수 있습니다.

실제로 BxlServer는 SQL Server에서 작동하여 데이터를 전송하고 작업을 관리하는 언어 런타임 환경의 도우미입니다. BXL은 이진 교환 언어의 약자이며, SQL Server와 외부 프로세스 간에 데이터를 효율적으로 이동하는 데 사용되는 데이터 형식을 나타냅니다. BxlServer는 Microsoft R Client 및 Microsoft R Server와 같은 관련 제품의 중요한 부분이기도 합니다.

**SQL Satellite**는 데이터베이스 엔진에 포함된 확장성 API이며, C 또는 C++를 사용하여 구현된 외부 코드 또는 외부 런타임을 지원합니다.

BxlServer는 SQL Satellite를 사용하여 다음 작업을 수행합니다.

+ 입력 데이터 읽기
+ 출력 데이터 쓰기
+ 입력 인수 가져오기
+ 출력 인수 쓰기
+ 오류 처리
+ STDOUT 및 STDERR을 클라이언트에 다시 쓰기

SQL Satellite는 SQL Server와 외부 스크립트 언어 간의 빠른 데이터 전송에 최적화된 사용자 지정 데이터 형식을 사용합니다. SQL Server와 외부 스크립트 런타임 간의 통신 중에 형식 변환을 수행하고 입력 및 출력 데이터 세트의 스키마를 정의합니다.

SQL Satellite는 Windows 확장 이벤트(xEvents)를 사용하여 모니터링할 수 있습니다. 자세한 내용은 [R용 확장 이벤트](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) 및 [Python용 확장 이벤트](../../advanced-analytics/python/extended-events-for-python.md)를 참조하세요.

## <a name="communication-channels-between-components"></a>구성 요소 간 통신 채널

이 섹션에서는 구성 요소 및 데이터 플랫폼 간의 통신 프로토콜에 대해 설명합니다.

+ **TCP/IP**

  SQL Server와 SQL Satellite 간의 내부 통신에서는 기본적으로 TCP/IP를 사용합니다.

+ **명명된 파이프**

  SQL Satellite를 통한 BxlServer와 SQL Server 간의 내부 데이터 전송은 독점적인 압축 데이터 형식을 사용하여 성능을 향상시킵니다. 데이터가 명명된 파이프를 사용하여 언어 실행 시간과 BxlServer 간에 BXL 형식으로 교환됩니다.

+ **ODBC**

  외부 데이터 과학 클라이언트와 원격 SQL Server 인스턴스 간의 통신에서는 ODBC를 사용합니다. 스크립트 작업을 SQL Server로 보내는 계정에는 인스턴스에 연결하고 외부 스크립트를 실행할 수 있는 두 가지 권한이 모두 있어야 합니다.

  또한 작업에 따라 계정에 필요할 수 있는 권한은 다음과 같습니다.

  + 작업에서 사용하는 데이터 읽기
  + 테이블에 데이터 쓰기: 예를 들어 결과를 테이블에 저장하는 경우
  + 데이터베이스 개체 만들기: 예를 들어 외부 스크립트를 새 저장 프로시저의 일부로 저장하는 경우

  SQL Server가 원격 클라이언트에서 실행되는 스크립트의 컴퓨팅 컨텍스트로 사용되고 실행 파일이 외부 원본에서 데이터를 검색해야 하는 경우 ODBC가 쓰기 저장에 사용됩니다. SQL Server에서 원격 명령을 실행하는 사용자의 ID를 현재 인스턴스의 사용자 ID에 매핑하고, 해당 사용자의 자격 증명을 사용하여 ODBC 명령을 실행합니다. 이 ODBC 호출을 수행하는 데 필요한 연결 문자열은 클라이언트 코드에서 가져옵니다.

+ **RODBC(R 전용)** 

  **RODBC**를 사용하여 스크립트 내에서 추가 ODBC 호출을 수행할 수 있습니다. RODBC는 관계형 데이터베이스의 데이터에 액세스하는 데 사용되는 인기 있는 R 패키지입니다. 그러나 성능은 일반적으로 SQL Server에서 사용하는 비슷한 공급자보다 느립니다. 많은 R 스크립트는 RODBC에 대해 포함된 호출을 사용하여 분석에 사용할 "보조" 데이터 세트를 검색합니다. 예를 들어 모델을 학습시키는 저장 프로시저는 SQL 쿼리를 정의하여 모델 교육을 위한 데이터를 얻지만, 포함된 RODBC 호출을 사용하여 추가 요소를 얻거나 조회를 수행하거나 텍스트 파일 또는 Excel과 같은 외부 소스에서 새 데이터를 가져올 수 있습니다.

  다음 코드는 R 스크립트에 포함된 RODBC 호출을 보여 줍니다.

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **기타 프로토콜**

  "청크"로 작업하거나 데이터를 원격 클라이언트에 다시 전송해야 하는 프로세스도 [XDF 파일 형식](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)을 사용할 수 있습니다. 실제 데이터는 인코딩된 Blob을 통해 전송됩니다.

## <a name="see-also"></a>참고 항목

+ [SQL Server의 R 확장](extension-r.md)
+ [SQL Server의 Python 확장](extension-python.md)