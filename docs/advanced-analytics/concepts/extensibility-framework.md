---
title: R 언어 및 Python 스크립트에 대 한 확장성 아키텍처
description: 관계형 데이터에서 R 및 Python 스크립트를 실행 하기 위한 이중 아키텍처를 사용 하는 SQL Server 데이터베이스 엔진에 대 한 외부 코드 지원
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a5c49172ed23867f95e383878f792092bd762177
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470454"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 확장성 아키텍처 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server에는 서버에서 R 또는 Python과 같은 외부 스크립트를 실행 하기 위한 확장성 프레임 워크가 있습니다. 스크립트는 핵심 데이터베이스 엔진에 대 한 확장으로 언어 런타임 환경에서 실행 됩니다. 

## <a name="background"></a>배경

확장성 프레임 워크는 R 런타임을 지원 하기 위해 SQL Server 2016에서 도입 되었습니다. SQL Server 2017는 Python에 대 한 지원을 추가 합니다.

확장성 프레임 워크의 목적은 R 및 Python과 같은 SQL Server와 데이터 과학 언어 간의 인터페이스를 제공 하 고, 데이터 과학 솔루션을 프로덕션으로 이동 하 고, 개발 중에 노출 되는 데이터를 보호 하는 것입니다. 프로세스. 데이터베이스 관리자는 SQL Server로 관리 되는 보안 프레임 워크 내에서 신뢰할 수 있는 스크립트 언어를 실행 하 여 데이터 과학자 엔터프라이즈 데이터 액세스를 허용 하는 동시에 보안을 유지할 수 있습니다.

다음 다이어그램은 확장 가능한 아키텍처의 기회와 이점을 시각적으로 설명 합니다.

  ![SQL Server와의 통합 목표](../media/ml-service-value-add.png "Machine Learning Services 값 추가")

모든 R 또는 Python 스크립트는 저장 프로시저를 호출 하 여 실행할 수 있으며, 결과는 SQL Server에 대 한 테이블 형식 결과로 반환 되므로 SQL 쿼리를 보내고 결과를 처리할 수 있는 모든 응용 프로그램에서 기계 학습을 쉽게 생성 하거나 사용할 수 있습니다.

+ 외부 스크립트 실행에는 SQL Server 데이터 보안이 적용 됩니다. 외부 스크립트를 실행 하는 사용자는 SQL 쿼리에서 동일 하 게 사용할 수 있는 데이터에만 액세스할 수 있습니다. 권한 부족으로 인해 쿼리가 실패 하면 동일한 사용자가 실행 하는 스크립트도 동일한 이유로 실패 합니다. SQL Server 보안은 테이블, 데이터베이스 및 인스턴스 수준에서 적용 됩니다. 데이터베이스 관리자는 사용자 액세스, 외부 스크립트에서 사용 하는 리소스 및 서버에 추가 된 외부 코드 라이브러리를 관리할 수 있습니다.  

+ 크기 조정 및 최적화 기회에는 이중이 있습니다. 데이터베이스 플랫폼 (ColumnStore 인덱스, [리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)) 및 R 및 Python 용 Microsoft 라이브러리를 사용 하 여 데이터 과학 모델을 사용할 때 확장 별 이득을 얻을 수 있습니다. R은 단일 스레드 이지만 RevoScaleR 함수는 다중 스레드로 작업 부하를 분산할 수 있습니다.

+ 배포는 SQL Server 방법론을 사용 합니다. 저장 프로시저는 PREDICT 같은 함수를 호출 하 여 서버에 유지 되는 예측 모델에서 결과를 반환 하는 외부 스크립트, 포함 된 SQL 또는 T-sql 쿼리를 래핑합니다.

+ 특정 도구 및 Ide에 설정 된 기술이 있는 R 및 Python 개발자는 이러한 도구에서 코드를 작성 한 다음 SQL Server 수 있도록 포트 코드를 작성할 수 있습니다.

## <a name="architecture-diagram"></a>아키텍처 다이어그램

이 아키텍처는 외부 스크립트가 SQL Server와는 별도의 프로세스에서 실행 되도록 설계 되었으며, 내부적으로 SQL Server 데이터 및 작업에 대 한 요청 체인을 관리 하는 구성 요소를 사용 합니다. SQL Server 버전에 따라 지원 되는 언어 확장에는 R 및 Python이 포함 됩니다. 

  ![구성 요소 아키텍처](../media/generic-architecture.png "구성 요소 아키텍처")

구성 요소에는 인터프리터 및 라이브러리를 로드 하기 위한 언어 관련 실행 패드 (R 또는 Python), 언어 및 라이브러리 관련 논리를 호출 하는 데 사용 되는 실행 **패드** 서비스가 포함 됩니다. 시작 관리자는 언어 실행 시간 및 소유 모듈을 로드 합니다. 예를 들어 코드에 RevoScaleR 함수가 포함 된 경우 RevoScaleR 인터프리터가 로드 됩니다. **Bxlserver** 및 **SQL 위성** 은 SQL Server를 사용 하 여 통신 및 데이터 전송을 관리 합니다.

<a name="launchpad"></a>

## <a name="launchpad"></a>실행 패드

는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리 하기 위해 별도의 호스트를 시작 하는 것과 비슷한 방식으로 외부 스크립트를 관리 하 고 실행 하는 서비스입니다. 실행 패드 서비스는 Microsoft에서 게시 하거나 성능 및 리소스 관리에 대 한 요구 사항을 충족 하는 Microsoft의 인증을 받은 신뢰할 수 있는 시작 프로그램만 시작할 수 있습니다.

| 신뢰할 수 있는 관리자 | 확장명 | SQL Server 버전 |
|-------------------|-----------|---------------------|
| R 언어의 RLauncher .dll | [R 확장](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Python 3.5에 대 한 Pythonlauncher | [Python 확장](extension-python.md) | SQL Server 2017 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 자체 사용자 계정으로 실행됩니다. 실행 패드를 실행 하는 계정을 변경 하는 경우 SQL Server 구성 관리자를 사용 하 여 변경 내용을 관련 파일에 쓰도록 해야 합니다.

Machine Learning Services SQL Server [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 추가한 각 데이터베이스 엔진 인스턴스에 대해 별도의 서비스가 만들어집니다. 각 데이터베이스 엔진 인스턴스에 대해 하나의 실행 패드 서비스가 있으므로 외부 스크립트를 지 원하는 여러 인스턴스가 있는 경우 각 인스턴스에 대 한 실행 패드 서비스가 제공 됩니다. 데이터베이스 엔진 인스턴스는 생성 된 실행 패드 서비스에 바인딩됩니다. 저장 프로시저 또는 T-sql에서 외부 스크립트를 호출할 때마다 동일한 인스턴스에 대해 만들어진 실행 패드 서비스를 호출 하는 SQL Server 서비스가 발생 합니다.

지원 되는 특정 언어로 작업을 실행 하기 위해 실행 패드는 풀에서 보안 작업자 계정을 가져오고 외부 런타임을 관리 하는 위성 프로세스를 시작 합니다. 각 위성 프로세스는 실행 패드의 사용자 계정을 상속 하 고 스크립트 실행 기간 동안 해당 작업자 계정을 사용 합니다. 스크립트가 병렬 프로세스를 사용 하는 경우 동일한 단일 작업자 계정으로 만들어집니다.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 및 SQL 위성

**Bxlserver** 는 SQL Server와 Python 또는 R 간의 통신을 관리 하는 Microsoft에서 제공 하는 실행 파일입니다. 외부 스크립트 세션을 포함 하는 데 사용 되는 Windows 작업 개체를 만들고, 각 외부 스크립트 작업에 대 한 보안 작업 폴더를 프로 비전 하며, SQL 위성을 사용 하 여 외부 런타임과 SQL Server 간의 데이터 전송을 관리 합니다. 작업이 실행 되는 동안 [프로세스 탐색기](https://technet.microsoft.com/sysinternals/processexplorer.aspx) 를 실행 하는 경우 BxlServer의 인스턴스를 하나 또는 여러 개 볼 수 있습니다.

실제로 BxlServer는 SQL Server에서 데이터를 전송 하 고 작업을 관리 하는 데 사용할 수 있는 언어 런타임 환경과 함께 사용 됩니다. BXL은 바이너리 교환 언어를 나타내며 SQL Server와 외부 프로세스 간에 데이터를 효율적으로 이동 하는 데 사용 되는 데이터 형식을 나타냅니다. BxlServer는 Microsoft R Client 및 Microsoft R Server와 같은 관련 제품의 중요 한 부분 이기도 합니다.

**SQL 위성** 은 외부 코드 또는 C 또는 C++를 사용 하 여 구현 되는 외부 런타임을 지 원하는 SQL Server 2016부터 데이터베이스 엔진에 포함 된 확장성 API입니다.

BxlServer는 SQL Satellite를 사용하여 다음 작업을 수행합니다.

+ 입력 데이터 읽기
+ 출력 데이터 쓰기
+ 입력 인수 가져오기
+ 출력 인수 쓰기
+ 오류 처리
+ STDOUT 및 STDERR을 클라이언트에 다시 쓰기

SQL 위성은 SQL Server 및 외부 스크립트 언어 간의 빠른 데이터 전송에 최적화 된 사용자 지정 데이터 형식을 사용 합니다. 형식 변환을 수행 하 고 SQL Server와 외부 스크립트 런타임 간의 통신 중에 입력 및 출력 데이터 집합의 스키마를 정의 합니다.

Windows 확장 이벤트 (Xevent)를 사용 하 여 SQL 위성을 모니터링할 수 있습니다. 자세한 내용은 R 및 [Python 용 확장 이벤트](../../advanced-analytics/python/extended-events-for-python.md) [에 대 한 확장 이벤트](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) 를 참조 하세요.

## <a name="communication-channels-between-components"></a>구성 요소 간 통신 채널

구성 요소 및 데이터 플랫폼 간의 통신 프로토콜은이 섹션에 설명 되어 있습니다.

+ **TCP/IP**

  기본적으로 SQL Server와 SQL 위성 간의 내부 통신에서는 TCP/IP를 사용 합니다.

+ **명명된 파이프**

  BxlServer와 SQL 위성을 통한 SQL Server 간의 내부 데이터 전송은 전용 압축 데이터 형식을 사용 하 여 성능을 향상 시킵니다. 데이터는 명명 된 파이프를 사용 하 여 BXL 형식의 언어 실행 시간 및 BxlServer 간에 교환 됩니다.

+ **ODBC**

  외부 데이터 과학 클라이언트와 원격 SQL Server 인스턴스 간의 통신은 ODBC를 사용 합니다. SQL Server 스크립트 작업을 보내는 계정에는 인스턴스에 연결 하 고 외부 스크립트를 실행 하기 위한 두 가지 권한이 모두 있어야 합니다.

  또한 태스크에 따라 계정에 다음 권한이 필요할 수 있습니다.

  + 작업에서 사용 하는 데이터 읽기
  + 테이블에 데이터 쓰기: 예를 들어 테이블에 결과를 저장 하는 경우
  + 예를 들어 외부 스크립트를 새 저장 프로시저의 일부로 저장 하는 경우 데이터베이스 개체를 만듭니다.

  SQL Server를 원격 클라이언트에서 실행 되는 스크립트에 대 한 계산 컨텍스트로 사용 하 고 실행 파일이 외부 원본에서 데이터를 검색 해야 하는 경우 ODBC는 쓰기 저장 (writeback)에 사용 됩니다. SQL Server 원격 명령을 실행 하는 사용자의 id를 현재 인스턴스의 사용자 id에 매핑하고 해당 사용자의 자격 증명을 사용 하 여 ODBC 명령을 실행 합니다. 이 ODBC 호출을 수행하는 데 필요한 연결 문자열은 클라이언트 코드에서 가져옵니다.

+ **RODBC (R 전용)** 

  **RODBC**를 사용하여 스크립트 내에서 추가 ODBC 호출을 수행할 수 있습니다. RODBC는 관계형 데이터베이스의 데이터에 액세스 하는 데 사용 되는 인기 있는 R 패키지입니다. 그러나 해당 성능은 SQL Server에서 사용 하는 비교 가능한 공급자 보다 일반적으로 느립니다. 많은 R 스크립트는 RODBC에 대해 포함된 호출을 사용하여 분석에 사용할 "보조" 데이터 세트를 검색합니다. 예를 들어 모델을 학습시키는 저장 프로시저는 SQL 쿼리를 정의하여 모델 교육을 위한 데이터를 얻지만, 포함된 RODBC 호출을 사용하여 추가 요소를 얻거나 조회를 수행하거나 텍스트 파일 또는 Excel과 같은 외부 소스에서 새 데이터를 가져올 수 있습니다.

  다음 코드는 R 스크립트에 포함된 RODBC 호출을 보여 줍니다.

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **기타 프로토콜**

  "청크"로 작업 하거나 원격 클라이언트에 데이터를 다시 전송 해야 할 수도 있는 프로세스는 [Xdf 파일 형식을](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)사용할 수 있습니다. 실제 데이터 전송은 인코딩된 blob을 통해 전송 됩니다.

## <a name="see-also"></a>관련 항목

+ [SQL Server의 R 확장](extension-r.md)
+ [SQL Server의 Python 확장](extension-python.md)