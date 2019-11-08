---
title: SQL Server 언어 확장의 확장성 아키텍처
titleSuffix: SQL Server Language Extensions
description: 관계형 데이터에서 외부 언어를 실행하기 위한 이중 아키텍처를 사용하는 SQL Server 데이터베이스 엔진에 대한 외부 코드 지원
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6cefa617dc6068f07b2cc2b684ce0442d7a438e8
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589087"
---
# <a name="extensibility-architecture-in-sql-server-language-extensions"></a>SQL Server 언어 확장의 확장성 아키텍처

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 언어 확장에는 서버에서 Java와 같은 외부 코드를 실행하기 위한 확장성 프레임워크가 있습니다. 이 코드는 언어 런타임 환경에서 코어 데이터베이스 엔진에 대한 확장으로 실행됩니다.

## <a name="background"></a>배경

확장성 프레임워크의 목적은 SQL Server와 Java 등의 외부 언어 간에 인터페이스를 제공하는 것입니다. 데이터베이스 관리자는 SQL Server로 관리되는 보안 프레임워크 내에서 신뢰할 수 있는 언어를 실행하여 데이터 과학자가 엔터프라이즈 데이터에 액세스하도록 허용하는 동시에 보안을 유지할 수 있습니다.

<!-- We need to get a diagram like the one below.
The following diagram visually describes opportunities and benefits of the extensible architecture.

  ![Goals of integration with SQL Server](../media/ml-service-value-add.png "Machine Learning Services Value Add")
-->

저장 프로시저를 호출하여 지원되는 모든 외부 언어를 실행할 수 있으며 결과는 테이블 형식으로 SQL Server에 직접 반환됩니다. 이렇게 하면 SQL 쿼리를 보내고 결과를 처리할 수 있는 애플리케이션에서 외부 언어를 쉽게 사용할 수 있습니다.

## <a name="architecture-diagrams"></a>아키텍처 다이어그램

이 아키텍처는 외부 코드가 SQL Server와는 별도의 프로세스에서 실행되도록 설계되었지만, 내부적으로 SQL Server 데이터 및 작업에 대한 요청 체인을 관리하는 구성 요소를 사용합니다. 
  
  ***Windows의 구성 요소 아키텍처:***

  ![Windows의 구성 요소 아키텍처](../media/generic-architecture-windows.png "Windows의 구성 요소 아키텍처")
  
  ***Linux의 구성 요소 아키텍처:***
  
  ![Linux의 구성 요소 아키텍처](../media/generic-architecture-linux.png "Linux의 구성 요소 아키텍처")
  
구성 요소에는 외부 런타임(예: Java)을 호출하는 데 사용되는 **실행 패드** 서비스와 인터프리터 및 라이브러리를 로드하기 위한 라이브러리 관련 논리가 포함되어 있습니다.

<a name="launchpad"></a>

## <a name="launchpad"></a>실행 패드

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 스크립트 실행을 담당하는 외부 프로세스의 수명, 리소스 및 보안 경계를 관리하는 서비스입니다. 이는 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리하기 위해 별도의 호스트를 시작하는 방식과 비슷합니다. 실행 패드 서비스는 Microsoft에서 게시하거나 성능 및 리소스 관리 요구 사항을 충족시키는 것으로 Microsoft에서 인증한 신뢰할 수 있는 시작 관리자만 시작할 수 있습니다.

| 신뢰할 수 있는 시작 관리자 | 확장명 | SQL Server 버전 |
|-------------------|-----------|---------------------|
| JavaLauncher.dll for Java | Java 확장 | SQL Server 2019 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 실행 격리를 위해 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)를 사용하는 **SQLRUserGroup**에서 실행됩니다.

SQL Server 컴퓨터 언어 확장을 추가한 각 데이터베이스 엔진 인스턴스에 대해 별도의 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스가 생성됩니다. 각 데이터베이스 엔진 인스턴스마다 하나의 실행 패드 서비스가 있으므로, 외부 스크립트를 지원하는 여러 인스턴스가 있는 경우 각 인스턴스에 대한 실행 패드 서비스가 제공됩니다. 데이터베이스 엔진 인스턴스는 생성된 실행 패드 서비스에 바인딩됩니다. 저장 프로시저 또는 T-SQL에서 외부 스크립트를 호출할 때마다 SQL Server 서비스가 동일한 인스턴스에 대해 만들어진 실행 패드 서비스를 호출합니다.

지원되는 특정 언어로 작업을 실행하기 위해 실행 패드는 풀에서 보안 작업자 계정을 가져오고 외부 런타임을 관리하는 위성 프로세스를 시작합니다. 각 위성 프로세스는 실행 패드의 사용자 계정을 상속하고 스크립트 실행 기간 동안 해당 작업자 계정을 사용합니다. 스크립트가 병렬 프로세스를 사용하는 경우 동일한 단일 작업자 계정에서 만들어집니다.

## <a name="communication-channels-between-components"></a>구성 요소 간의 통신 채널

이 섹션에는 구성 요소 및 데이터 플랫폼 간의 통신 프로토콜이 설명되어 있습니다.

+ **TCP/IP**

  기본적으로 SQL Server와 SQL Satellite 간의 내부 통신은 TCP/IP를 사용합니다.

+ **ODBC**

  외부 데이터 과학 클라이언트와 원격 SQL Server 인스턴스 간의 통신은 ODBC를 사용합니다. 스크립트 작업을 SQL Server로 보내는 계정에는 인스턴스에 연결하고 외부 스크립트를 실행하는 권한이 있어야 합니다.

  또한 작업에 따라 계정에 다음 권한이 필요할 수 있습니다.

  + 작업에서 사용하는 데이터 읽기
  + 테이블에 데이터 쓰기: 예를 들어 테이블에 결과를 저장하는 경우
  + 데이터베이스 개체 만들기: 예를 들어 외부 스크립트를 새 저장 프로시저의 일부로 저장하는 경우.

  SQL Server가 원격 클라이언트에서 실행된 스크립트의 컴퓨팅 컨텍스트로 사용되고 실행 파일이 외부 소스에서 데이터를 검색해야 하는 경우 ODBC가 쓰기 저장용으로 사용됩니다. SQL Server는 원격 명령을 실행하는 사용자의 ID를 현재 인스턴스의 사용자 ID로 매핑하고 해당 사용자의 자격 증명을 사용하여 ODBC 명령을 실행합니다. 이 ODBC 호출을 수행하는 데 필요한 연결 문자열은 클라이언트 코드에서 가져옵니다.

+ **기타 프로토콜**

  "청크"로 작업하거나 원격 클라이언트에 데이터를 다시 전송해야 하는 프로세스는 [XDF 파일 형식](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)을 사용할 수도 있습니다. 실제 데이터는 인코딩된 blob을 통해 전송됩니다.

## <a name="next-steps"></a>다음 단계

+ [언어 확장이란?](../language-extensions-overview.md)
