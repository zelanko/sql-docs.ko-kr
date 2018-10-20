---
title: SQL Server Machine Learning Services의 확장성 아키텍처 | Microsoft Docs
description: 관계형 데이터에서 R 및 Python 스크립트를 실행 하는 것에 대 한 이중 아키텍처를 사용 하 여 SQL Server 데이터베이스 엔진의 경우 외부 코드 지원 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c2ada06ce41cd9a5faf3237ce2b9bac6fc40291d
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419221"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 확장성 아키텍처 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server에는 확장성 프레임 워크 서버에서 Python 또는 R 등의 외부 스크립트를 실행 하는 것에 대 한 합니다. 스크립트 언어 런타임 환경에서 핵심 데이터베이스 엔진 확장으로 실행 됩니다. 

## <a name="background"></a>배경

확장성 프레임 워크는 R 런타임을 지 원하는 SQL Server 2016에서 도입 되었습니다. SQL Server 2017에 Python에 대 한 지원 추가

SQL Server와 R 및 Python으로 개발 하는 동안 이동 데이터 과학 솔루션 프로덕션 및 보호 데이터에 노출 될 때 마찰을 줄이는 등의 데이터 과학 언어 간의 인터페이스를 제공 하는 확장성 프레임 워크의 목적은 프로세스입니다. SQL Server에서 관리 되는 보안 프레임 워크 내에서 신뢰할 수 있는 스크립트 언어를 실행 하면 데이터베이스 관리자는 데이터 과학자가 엔터프라이즈 데이터에 대 한 액세스를 허용 하는 동안 보안을 유지할 수 있습니다.

다음 다이어그램에는 시각적으로 기회 및 확장 가능한 아키텍처의 장점을 설명합니다.

  ![SQL Server와의 통합 목표](../media/ml-service-value-add.png "Machine Learning Services 값 추가")

저장된 프로시저를 호출 하 여 모든 R 또는 Python 스크립트를 실행할 수 있습니다 및 결과가 반환 됩니다 테이블 형식 결과와 SQL Server에 직접 생성 하거나 SQL 쿼리를 전송 하 고 결과 처리할 수 있는 모든 응용 프로그램에서 machine learning을 사용할 수 있도록.

+ 외부 스크립트 실행 외부 스크립트를 실행 하는 사용자의 SQL 쿼리에서 동일 하 게 사용할 수 있는 데이터만 액세스할 수 있는 SQL Server 데이터 보안에 적용 됩니다. 쿼리 권한 부족으로 인해 실패 하면 동일한 사용자가 실행 되는 스크립트도 이와 같은 이유로 실패 합니다. SQL Server 보안 테이블, 데이터베이스 및 인스턴스 수준에서 적용 됩니다. 데이터베이스 관리자가 사용자 액세스, 외부 스크립트를 사용 하는 리소스 및 서버에 추가 된 외부 코드 라이브러리를 관리할 수 있습니다.  

+ 크기 조정 및 최적화 기회를 이중으로 있는: 데이터베이스 플랫폼을 통해 향상 (ColumnStore 인덱스 [리소스 거 버 넌 스](../../advanced-analytics/r/resource-governance-for-r-services.md)), 및 데이터에 대 한 R 및 Python에 대 한 Microsoft 라이브러리 사용 하는 경우 확장 프로그램별 향상 과학 모델입니다. R은 단일 스레드, RevoScaleR 함수는 다중 스레드, 다중 코어를 통해 워크 로드를 배포할 수입니다.

+ SQL Server 방법론을 사용 하 여 배포: 외부 스크립트를 배치 하는 저장된 프로시저, 포함 된 SQL 또는 T-SQL 쿼리 같은 서버에서 유지 된 예측 모델의 결과 반환 하는 예측 함수를 호출 합니다.

+ R 및 Python 개발자에 게 기술을 특정 도구와 Ide에서 이러한 도구에 코드를 작성 한 다음 코드를 SQL Server 포트를 설정 합니다.

## <a name="architecture-diagram"></a>아키텍처 다이어그램

아키텍처는 SQL Server에서 하지만 내부적으로 SQL Server에서 데이터 및 작업에 대 한 요청 체인을 관리 하는 구성 요소를 사용 하 여 외부 스크립트 별도의 프로세스로 실행 되도록 설계 되었습니다. SQL server 버전에 따라 지원 되는 언어 확장에는 R 및 Python 포함 됩니다. 

  ![구성 요소 아키텍처](../media/generic-architecture.png "구성 요소 아키텍처")

구성 요소에 포함 된 **실행 패드** 언어별 시작 관리자 (R 또는 Python), 언어 및 인터프리터 및 라이브러리를 로드 하기 위한 라이브러리 관련 논리를 호출 하는 데 사용 되는 서비스입니다. 시작 관리자를 실행 하는 언어 시간 및 소유 된 모듈을 로드합니다. 예를 들어 코드에서 RevoScaleR 함수를 포함 하는 경우 RevoScaleR 인터프리터를 로드 합니다. **BxlServer** 하 고 **SQL Satellite** SQL Server를 사용 하 여 통신 및 데이터 전송을 관리 합니다.

<a name="launchpad"></a>

## <a name="launchpad"></a>실행 패드

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 관리 하 고 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리 하는 것에 대 한 별도 호스트를 실행 하는 방식과 유사 하 게 외부 스크립트를 실행 하는 서비스입니다. 실행 패드 서비스는 Microsoft에서 게시 또는 성능 및 리소스 관리에 대 한 요구 사항을 충족으로 Microsoft에 의해 인증 된만 신뢰할 수 있는 시작 관리자를 시작할 수 있습니다.

| 신뢰할 수 있는 시작 관리자 | 확장명 | SQL Server 버전 |
|-------------------|-----------|---------------------|
| R 언어에 대 한 RLauncher.dll | [R 확장](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Python 3.5에 대 한 Pythonlauncher.dll | [Python 확장](extension-python.md) | SQL Server 2017 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 자체 사용자 계정으로 실행됩니다. 실행 패드를 실행 하는 계정을 변경 하면 경우에 관련 파일에 변경 내용이 기록 되도록 되도록 SQL Server 구성 관리자를 사용 하 여 수행 해야 합니다.

별도 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] SQL Server Machine Learning Services를 추가한 각 데이터베이스 엔진 인스턴스에 대 한 서비스가 만들어집니다. 하나의 실행 패드는 실행 패드 서비스 각각에 대 한 외부 스크립트 지원 사용 하 여 여러 인스턴스가 있는 경우 해야 하므로 각 데이터베이스 엔진 인스턴스에 대 한 서비스입니다. 데이터베이스 엔진 인스턴스를 위해 만든 실행 패드 서비스에 바인딩됩니다. 저장된 프로시저의 외부 스크립트의 T-SQL 결과 동일한 인스턴스에 대해 만든 실행 패드 서비스를 호출 합니다. SQL Server 서비스에 대 한 모든 호출 합니다.

지원 되는 특정 언어로 작업을 실행 하려면 실행 패드 보안된 작업자 계정 풀에서 가져옵니다 하 고 외부 런타임에서 관리 하는 위성 프로세스를 시작 합니다. 각 위성 프로세스는 실행 패드의 사용자 계정을 상속 하 고 스크립트 실행 기간에 대 한 해당 작업자 계정을 사용 합니다. 스크립트 병렬 프로세스를 사용 하는 경우 동일한, 단일 작업자 계정으로 생성 됩니다.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 및 SQL 위성

**BxlServer** 는 SQL Server 및 Python 또는 R 간의 통신을 관리 하는 Microsoft에서 제공 하는 실행 파일 외부 스크립트 세션을 각 외부 스크립트 작업에 대 한 보안 작업 폴더를 프로 비전을 포함 하는 데 사용 되는 SQL Satellite를 사용 하 여 외부 런타임 및 SQL Server 간의 데이터 전송을 관리 하는 Windows 작업 개체를 만듭니다. 실행 하는 경우 [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) BxlServer의 하나 또는 여러 인스턴스 작업을 실행 하는 동안 표시 될 수 있습니다.

실제로 BxlServer는 SQL Server 데이터를 전송 하 고 작업을 관리를 사용 하는 시간 환경을 실행 하는 언어와 함께 제공 합니다. BXL 이진 교환 언어 의미 하 고 SQL Server와 외부 프로세스 간에 데이터를 효율적으로 이동 하는 데 데이터 형식을 참조 합니다. BxlServer는 Microsoft R Client 및 Microsoft R Server와 같은 관련된 제품의 중요 한 부분 이기도합니다.

**SQL Satellite** 외부 코드를 지 원하는 SQL Server 2016 부터는 데이터베이스 엔진에 포함 된 확장성 API 또는 C 또는 c + +를 사용 하 여 구현 된 외부 런타임을입니다.

BxlServer는 SQL Satellite를 사용하여 다음 작업을 수행합니다.

+ 입력 데이터 읽기
+ 출력 데이터 쓰기
+ 입력 인수 가져오기
+ 출력 인수 쓰기
+ 오류 처리
+ STDOUT 및 STDERR을 클라이언트에 다시 쓰기

SQL Satellite는 SQL Server와 외부 스크립트 언어 간의 빠른 데이터 전송에 대 한 최적화 된 사용자 지정 데이터 형식을 사용 합니다. 형식 변환을 수행 하 고 SQL Server와 외부 스크립트 런타임 간의 통신 중 입력 및 출력 데이터 집합의 스키마를 정의 합니다.

SQL Satellite는 확장 이벤트 (xEvents) 창을 사용 하 여 모니터링할 수 있습니다. 자세한 내용은 [R에 대 한 확장 이벤트](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) 하 고 [Python 용 확장 이벤트](../../advanced-analytics/python/extended-events-for-python.md)합니다.

## <a name="communication-channels-between-components"></a>구성 요소 간의 통신 채널

구성 요소 및 데이터 플랫폼 간에 통신 프로토콜이이 섹션에 설명 합니다.

+ **TCP/IP**

  기본적으로 SQL Server와 SQL Satellite 간의 내부 통신은 TCP/IP를 사용 합니다.

+ **명명된 파이프**

  BxlServer 및 SQL Satellite를 통한 SQL Server 간의 내부 데이터 전송은 독점적인 압축된 데이터 형식을 사용 하 여 성능 향상. 데이터는 BXL 형식의 명명 된 파이프를 사용 하 여 실행 되는 언어 시간과 BxlServer 간에 교환 됩니다.

+ **ODBC**

  ODBC를 사용 하는 외부 데이터 과학 클라이언트와 원격 SQL Server 인스턴스 간의 통신 합니다. SQL server 스크립트 작업을 전송 하는 계정에는 외부 스크립트를 실행 하는 인스턴스에 연결 하려면 두 권한이 있어야 합니다.

  또한 태스크에 따라 계정이 이러한 권한을 해야 합니다.

  + 작업에서 사용 하는 데이터 읽기
  + 테이블에 데이터를 작성 합니다: 예를 들어 경우 저장 결과 테이블
  + 데이터베이스 개체를 만듭니다: 예를 들어 새 저장된 프로시저의 일부로 외부 스크립트를 저장 합니다.

  SQL Server에서 실행 되는 스크립트에 대 한 계산 컨텍스트로 사용 될 때 실행 파일 및 원격 클라이언트의 경우 외부 원본에서 데이터를 검색 해야, ODBC 쓰기 저장에 사용 됩니다. SQL Server를 현재 인스턴스에서 사용자의 id로 원격 명령을 실행 하는 사용자의 id를 매핑하고 해당 사용자의 자격 증명을 사용 하 여 ODBC 명령을 실행 합니다. 이 ODBC 호출을 수행하는 데 필요한 연결 문자열은 클라이언트 코드에서 가져옵니다.

+ **RODBC (R에만 해당)** 

  **RODBC**를 사용하여 스크립트 내에서 추가 ODBC 호출을 수행할 수 있습니다. RODBC는 관계형 데이터베이스에서 데이터에 액세스 하는 데 사용 하는 인기 있는 R 패키지 그러나 성능이 더 일반적으로 SQL Server에서 사용 하는 비슷한 공급자 보다 느립니다. 많은 R 스크립트는 RODBC에 대해 포함된 호출을 사용하여 분석에 사용할 "보조" 데이터 집합을 검색합니다. 예를 들어 모델을 학습시키는 저장 프로시저는 SQL 쿼리를 정의하여 모델 교육을 위한 데이터를 얻지만, 포함된 RODBC 호출을 사용하여 추가 요소를 얻거나 조회를 수행하거나 텍스트 파일 또는 Excel과 같은 외부 소스에서 새 데이터를 가져올 수 있습니다.

  다음 코드는 R 스크립트에 포함된 RODBC 호출을 보여 줍니다.

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **다른 프로토콜**

  "청크"에서 작업 하거나 원격 클라이언트로 데이터를 전송 해야 할 수 있는 프로세스를 이용할 수 있습니다 합니다 [XDF 파일 형식](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)합니다. 실제 데이터 전송은 인코딩된 blob을 통해 됩니다.

## <a name="see-also"></a>관련 항목

+ [SQL Server에서 R 확장](extension-r.md)
+ [SQL Server의 Python 확장](extension-python.md)