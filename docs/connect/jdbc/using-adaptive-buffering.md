---
title: 적응 버퍼링 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 07a7a67addb10d91b011f821f5b85ed03981d055
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916461"
---
# <a name="using-adaptive-buffering"></a>선택 버퍼링 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

선택 버퍼링은 서버 커서 오버헤드 없이 모든 종류의 큰 값 데이터를 검색할 수 있는 기능입니다. 애플리케이션은 드라이버가 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 버전에서 선택 버퍼링 기능을 사용할 수 있습니다.

일반적으로 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 쿼리를 실행할 때 모든 결과를 서버에서 검색하여 애플리케이션 메모리에 넣습니다. 이 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 리소스 소비를 최소화하지만 매우 큰 결과를 생성하는 쿼리의 경우 JDBC 애플리케이션에서 OutOfMemoryError가 throw될 수 있습니다.

애플리케이션에서 매우 큰 결과를 처리할 수 있도록 하기 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 선택 버퍼링을 제공합니다. 선택 버퍼링을 사용하면 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 명령문 실행 결과를 한 번에 모두 검색하는 것이 아니라 애플리케이션에 필요할 때 검색합니다. 또한 응용 프로그램에서 더 이상 액세스할 수 없는 결과를 즉시 삭제합니다. 다음은 선택 버퍼링을 유용하게 사용할 수 있는 몇 가지 예입니다.

- **쿼리로 매우 큰 결과 집합이 생성되는 경우**: 메모리에 저장할 수 있는 행보다 더 많은 행을 생성하는 SELECT 문을 애플리케이션에서 실행하는 경우가 있습니다. 이전 릴리스에서는 OutOfMemoryError를 방지하기 위해 애플리케이션에서 서버 커서를 사용해야 했습니다. 선택 버퍼링을 사용하면 서버 커서 없이도 임의의 큰 결과 집합을 정방향 읽기 전용으로 처리할 수 있습니다.

- **쿼리가 너무 큰**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**열 또는**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**출력 매개 변수 값을 생성합니다.** 애플리케이션이 너무 커서 애플리케이션 메모리에 한 번에 저장할 수 없는 큰 단일 값(열 또는 출력 매개 변수)을 검색할 수 있습니다. 적응 버퍼링을 사용 하면 클라이언트 응용 프로그램에서 getAsciiStream, getBinaryStream 또는 getCharacterStream 메서드를 사용 하 여 이러한 값을 스트림으로 검색할 수 있습니다. 애플리케이션은 스트림에서 읽으면서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 값을 검색합니다.

> [!NOTE]  
> 선택 버퍼링을 사용하면 JDBC 드라이버는 필요한 양의 데이터만 버퍼링합니다. 드라이버는 버퍼 크기를 제어 또는 제한하는 공용 메서드를 제공하지 않습니다.

## <a name="setting-adaptive-buffering"></a>선택 버퍼링 설정

JDBC 드라이버 버전 2.0부터, 이 드라이버의 기본 동작은 "**선택**"입니다. 즉 선택 버퍼링을 사용하기 위해 애플리케이션에서 명시적으로 선택 동작을 요청할 필요가 없습니다. 그러나 버전 1.2 릴리스에서는 버퍼링 모드가 기본적으로 "**전체**"이므로 애플리케이션에서 명시적으로 선택 버퍼링 모드를 요청해야 했습니다.

다음은 응용 프로그램에서 문 실행 시 선택 버퍼링을 사용하도록 요청할 수 있는 세 가지 방법입니다.

- 응용 프로그램은 **Responsebuffering** 연결 속성을 "adaptive"로 설정할 수 있습니다. 연결 속성을 설정 하는 방법에 대 한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조 하세요.

- 애플리케이션에서 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체의 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) 메서드를 사용하여 해당 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체를 통해 생성된 모든 연결에 대해 응답 버퍼링 모드를 설정할 수 있습니다.

- 애플리케이션에서 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하여 특정 문 개체에 대해 응답 버퍼링 모드를 설정할 수 있습니다.

JDBC 드라이버 버전 1.2를 사용하는 경우 애플리케이션에서 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하여 명령문 개체를 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스로 캐스팅해야 했습니다. [Large Data 샘플 읽기](../../connect/jdbc/reading-large-data-sample.md) 및 [저장 프로시저를 사용 하 여 Large data 읽기 샘플](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) 의 코드 예제는 이전 사용법을 보여 줍니다.

그러나 JDBC 드라이버 버전 2.0에서는 애플리케이션에서 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 메서드 및 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 메서드를 사용하여 구현 클래스의 계층 구조에 관계없이 공급업체별 기능에 액세스할 수 있습니다. 예제 코드는 [대량 데이터 업데이트 샘플](../../connect/jdbc/updating-large-data-sample.md) 항목을 참조 하세요.

## <a name="retrieving-large-data-with-adaptive-buffering"></a>선택 버퍼링을 사용하여 큰 데이터 검색

get\<Type&gt;Stream 메서드를 사용하여 큰 값을 한 번 읽은 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 반환하는 순서로 ResultSet 열과 CallableStatement 출력 매개 변수에 액세스하면 결과를 처리할 때 선택 버퍼링이 애플리케이션 메모리 사용량을 최소화합니다. 선택 버퍼링을 사용하면 다음과 같은 결과를 얻을 수 있습니다.

- [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스에 정의된 get\<Type&gt;Stream 메서드는 애플리케이션에서 표시하는 경우 스트림을 재설정할 수 있다 하더라도 기본적으로 한 번 읽기 스트림을 반환합니다. 애플리케이션에서 스트림 `reset`을 원할 경우 먼저 해당 스트림에서 `mark` 메서드를 호출해야 합니다.

- [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) 및 [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) 클래스에 정의된 get\<Type>Stream 메서드는 `mark` 메서드를 호출하지 않고 항상 스트림의 시작 위치로 변경될 수 있는 스트림을 반환합니다.

애플리케이션에서 선택 버퍼링을 사용하는 경우 get\<Type&gt;Stream 메서드에 의해 검색된 값은 한 번만 검색될 수 있습니다. 같은 개체의 get\<Type>Stream 메서드를 호출한 후 같은 열이나 매개 변수에서 get\<Type> 메서드를 호출하려고 하면 "데이터에 액세스되었으나 이 열이나 매개 변수에는 사용할 수 없습니다."라는 메시지와 함께 예외가 발생합니다.

> [!NOTE]
> 결과 집합을 처리 하는 중에 ResultSet. close ()를 호출 하면 나머지 모든 패킷을 읽고 삭제 하기 위해 SQL Server Microsoft JDBC Driver가 필요 합니다. 쿼리가 큰 데이터 집합을 반환 하 고 특히 네트워크 연결이 느려지는 경우 시간이 오래 걸릴 수 있습니다.

## <a name="guidelines-for-using-adaptive-buffering"></a>선택 버퍼링 사용에 대한 지침

응용 프로그램의 메모리 사용량을 최소화하기 위해 개발자들이 따라야 할 중요한 지침은 다음과 같습니다.

- 애플리케이션에서 매우 큰 결과 집합을 처리할 수 있도록 연결 문자열 속성 **selectMethod=cursor**를 사용하지 않도록 합니다. 선택 버퍼링 기능은 응용 프로그램이 서버 커서를 사용하지 않고도 매우 큰 정방향 전용의 읽기 전용 결과 집합을 처리할 수 있도록 합니다. **selectMethod=cursor**를 설정하면 해당 연결에서 생성한 모든 정방향 읽기 전용 결과 집합이 영향을 받습니다. 즉, 애플리케이션에서 행 수가 적은 간단한 결과 집합을 자주 처리하는 경우 각 결과 집합에 대한 서버 커서를 만들고 읽고 닫는 작업을 할 때 **selectMethod**가 **cursor**로 설정되지 않은 경우보다 클라이언트 쪽 및 서버측 모두에서 리소스를 더 많이 사용합니다.

- GetBlob 또는 getClob 메서드 대신 getAsciiStream, getBinaryStream 또는 getCharacterStream 메서드를 사용 하 여 많은 텍스트 또는 이진 값을 스트림으로 읽습니다. 버전 1.2 릴리스 이상에서는 이러한 작업을 위해 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스에 새로운 get\<Type>Stream 메서드가 제공됩니다.

- SELECT 문에서 잠재적으로 큰 값을 갖는 열이 열 목록의 마지막에 배치되도록 하고 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)의 get\<Type>Stream 메서드를 사용하여 해당 메서드가 선택된 순서로 해당 열에 액세스하도록 합니다.

- [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 생성에 사용된 SQL에서 잠재적으로 큰 값을 갖는 출력 매개 변수가 매개 변수 목록의 마지막에 선언되도록 합니다. 또한 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)의 get\<Type>Stream 메서드를 사용하여 해당 메서드가 선언된 순서로 출력 매개 변수에 액세스하도록 합니다.

- 둘 이상의 문이 같은 연결에서 동시에 실행되지 않도록 합니다. 이전 문의 결과를 처리하기 전에 다른 문을 실행하면 처리되지 않은 결과가 응용 프로그램 메모리에 버퍼링될 수 있습니다.

- 다음과 같이 **Responsebuffering = 적응** 대신 **selectMethod = cursor** 를 사용 하는 것이 더 유용 합니다.

  - 응용 프로그램이 사용자 입력 후에 각 행을 읽는 것과 같이 앞 으로만 이동 가능한 읽기 전용 결과 집합을 천천히 처리 하는 경우 **Responsebuffering = 적응형** 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **selectMethod = cursor** 를 사용 하 여 리소스 사용량을 줄일 수 있습니다. .

  - 애플리케이션이 동일한 연결에서 동시에 둘 이상의 정방향 읽기 전용 결과 집합을 처리하는 경우 **responseBuffering=adaptive** 대신 **selectMethod=cursor**를 사용하면 이러한 결과 집합을 처리하는 동안 드라이버에 필요한 메모리를 줄일 수 있습니다.

  두 경우 모두 서버 커서를 만들고 읽고 닫을 때 발생하는 오버헤드를 고려해야 합니다.

또한 다음 목록에서는 스크롤 및 업데이트가 가능한 정방향 전용 결과 집합에 대한 권장 사항에 대해 설명합니다.

- 스크롤 가능한 결과 집합의 경우 행 블록을 인출할 때 드라이버는 선택 버퍼링이 설정된 경우에도 항상 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 메서드가 나타내는 행 수를 메모리로 읽어들입니다. 스크롤로 인해 OutOfMemoryError가 발생하는 경우 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 메서드를 호출하여 인출 크기를 더 적은 행 수(필요한 경우 1도 가능)로 설정함으로써 인출되는 행 수를 줄일 수 있습니다. 이렇게 해도 OutOfMemoryError가 발생하는 경우에는 스크롤 가능한 결과 집합에 아주 큰 열을 포함하지 마십시오.

- 업데이트 가능한 정방향 결과 집합의 경우 행 블록을 인출할 때 드라이버는 해당 연결에 대해 선택 버퍼링이 설정된 경우에도 일반적으로 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 메서드가 나타내는 행 수를 메모리로 읽어들입니다. [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) 메서드를 호출하여 OutOfMemoryError가 발생하는 경우 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 메서드를 호출하여 인출 크기를 더 적은 행 수(필요한 경우 1도 가능)로 설정함으로써 인출되는 행 수를 줄일 수 있습니다. 또한 명령문을 실행하기 전에 "**adaptive**" 매개 변수를 사용하여 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 호출하여 드라이버가 행을 버퍼링하지 않도록 지시할 수 있습니다. 결과 집합을 스크롤할 수 없으므로 애플리케이션이 get\<Type&gt;Stream 메서드 중 하나를 사용하여 큰 열 값에 액세스하는 경우 드라이버는 정방향 읽기 전용 결과 집합을 처리할 때와 마찬가지로 애플리케이션이 값을 읽는 즉시 해당 값을 삭제합니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
