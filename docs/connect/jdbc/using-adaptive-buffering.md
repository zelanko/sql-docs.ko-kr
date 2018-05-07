---
title: 선택 버퍼링을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae4120b567d876556c29254eae65d4471ab63924
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-adaptive-buffering"></a>선택 버퍼링 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  선택 버퍼링은 서버 커서 오버헤드 없이 모든 종류의 큰 값 데이터를 검색할 수 있는 기능입니다. 응용 프로그램의 모든 버전에서 선택 버퍼링 기능을 사용할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 드라이버에서 지 원하는 합니다.  
  
 일반적으로 때는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 쿼리를 실행의 결과 모두 서버에서 검색 하는 응용 프로그램 메모리에 있습니다. 이 방법은에서 리소스 소비를 최소화 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]는 OutOfMemoryError 매우 큰 결과 생성 하는 쿼리의 경우 JDBC 응용 프로그램에서 발생할 수 있습니다.  
  
 응용 프로그램에서 매우 큰 결과 처리할 수 있도록 하기 위해는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 선택 버퍼링을 제공 합니다. 선택 버퍼링을 검색 하 여에서 문 실행 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 응용 프로그램에서 필요할 때 보다는 한 번에 모두 있습니다. 또한 응용 프로그램에서 더 이상 액세스할 수 없는 결과를 즉시 삭제합니다. 다음은 선택 버퍼링을 유용하게 사용할 수 있는 몇 가지 예입니다.  
  
-   **쿼리에서 매우 큰 결과 집합 생성:** 응용 프로그램에는 응용 프로그램 메모리에 저장할 수 있는 보다 많은 행을 생성 하는 SELECT 문을 실행할 수 있습니다. 이전 버전에서는 응용 프로그램 프로그램 OutOfMemoryError를 방지 하기 위해 서버 커서를 사용 해야 했습니다. 선택 버퍼링을 사용하면 서버 커서 없이도 임의의 큰 결과 집합을 정방향 읽기 전용으로 처리할 수 있습니다.  
  
-   **쿼리로 매우 큰**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**열 또는**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**OUT 매개 변수 값:** 응용 프로그램에는 단일 값을 검색할 수 (열 또는 OUT 매개 변수)는이 너무 커서 응용 프로그램 메모리에 저장할 수 있습니다.         선택 버퍼링 클라이언트 응용 프로그램을 getAsciiStream, getBinaryStream, 또는 getCharacterStream 메서드를 사용 하 여 이러한 값을 스트림으로 검색할 수 있습니다. 응용 프로그램에서 값을 검색 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스트림에서 읽으면서 합니다.  
  
> [!NOTE]  
>  선택 버퍼링을 사용하면 JDBC 드라이버는 필요한 양의 데이터만 버퍼링합니다. 드라이버는 버퍼 크기를 제어 또는 제한하는 공용 메서드를 제공하지 않습니다.  
  
## <a name="setting-adaptive-buffering"></a>선택 버퍼링 설정  
 JDBC 드라이버 버전 2.0에서 드라이버의 기본 동작은는 "**적응**"입니다. 즉 선택 버퍼링을 사용하기 위해 응용 프로그램에서 명시적으로 선택 동작을 요청할 필요가 없습니다. 그러나 버퍼링 모드를 버전 1.2 릴리스에서 "**전체**" 하 고 응용 프로그램이 기본적으로 선택 버퍼링 모드를 명시적으로 요청 해야 했습니다.  
  
 다음은 응용 프로그램에서 문 실행 시 선택 버퍼링을 사용하도록 요청할 수 있는 세 가지 방법입니다.  
  
-   연결 속성을 설정할 수도 있습니다 **responseBuffering** "adaptive"로 합니다. 연결 속성 설정에 대 한 자세한 내용은 참조 하십시오. [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
-   응용 프로그램에서 사용할 수는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) 의 메서드는 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 응답 버퍼링 모드를 통해 만든 모든 연결에 대해 설정할 개체 [ SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체입니다.  
  
-   응용 프로그램에서 사용할 수는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 응답 버퍼링 특정 문 개체에 대 한 모드를 설정 하는 클래스입니다.  
  
 JDBC 드라이버 버전 1.2, 문 개체를 캐스팅 하는 데 필요한 응용 프로그램을 사용 하는 경우는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 사용 하는 클래스는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드. 코드 예제는 [읽기 큰 데이터 샘플](../../connect/jdbc/reading-large-data-sample.md) 및 [저장 프로시저 샘플에 큰 데이터를 읽는](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) 이러한 이전 사용법을 보여 줍니다.  
  
 그러나 jdbc 드라이버 버전 2.0에서는 응용 프로그램을 사용할 수는 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 메서드 및 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 관계 없이 공급 업체별 기능에 대 한 액세스 하는 메서드는 클래스 계층 구조를 구현 합니다. 예를 들어 코드, 참조는 [큰 데이터 업데이트 샘플](../../connect/jdbc/updating-large-data-sample.md) 항목입니다.  
  
## <a name="retrieving-large-data-with-adaptive-buffering"></a>선택 버퍼링을 사용하여 큰 데이터 검색  
 큰 값은 get을 사용 하 여 한 번만 읽을 때\<유형 > 스트림 메서드 및 결과 집합 열과 CallableStatement OUT 매개 변수에서 반환 된 순서 대로 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 응용 프로그램을 최소화 선택 버퍼링 결과 처리할 때 메모리 사용량입니다. 선택 버퍼링을 사용하면 다음과 같은 결과를 얻을 수 있습니다.  
  
-   Get\<유형 >에 정의 된 메서드를 스트리밍하는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 하는 경우 스트림을 재설정할 수 있지만 기본적으로 한 번 읽기 스트림을 반환 응용 프로그램으로 표시 합니다. 응용 프로그램에서 하려는 경우 `reset` 호출 하는 스트림에 `mark` 메서드를 스트리밍하려면 먼저 합니다.  
  
-   Get\<유형 >에 정의 된 메서드를 스트리밍하는 [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) 및 [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) 클래스 없이 스트림의 시작 위치로 항상 위치가 변경 될 수 있는 스트림을 반환 호출 된 `mark` 메서드.  
  
 응용 프로그램 선택 버퍼링 사용 하는 경우, get으로 검색 된 값은\<유형 > 스트림 메서드를 한 번만 검색할 수 있습니다. 모든 get 호출 하려고 하면\<형식 > 같은 열 이나 매개 변수는 get를 호출한 후에 메서드\<유형 > 예외가 동일한 개체의 스트림 메서드 메시지와 함께 발생, "데이터에 액세스를 사용할 수 없으면이 열 또는 매개 변수 "입니다.  
  
> [!NOTE]
> 결과 집합을 처리 하는 동안 ResultSet.close()에 대 한 호출을 읽고 모든 나머지 패킷을 무시 하는 SQL Server 용 Microsoft JDBC Driver 필요 합니다. 쿼리에서 큰 데이터 집합을 반환 하 고 특히 네트워크 연결 속도가 느릴 경우 상당한 시간이 걸릴 수 있습니다.     
  
## <a name="guidelines-for-using-adaptive-buffering"></a>선택 버퍼링 사용에 대한 지침  
 응용 프로그램의 메모리 사용량을 최소화하기 위해 개발자들이 따라야 할 중요한 지침은 다음과 같습니다.  
  
-   연결 문자열 속성을 사용 하지 않도록 **selectMethod = cursor** 응용 프로그램에서 매우 큰 결과 처리할 수 있도록 설정 합니다. 선택 버퍼링 기능은 응용 프로그램이 서버 커서를 사용하지 않고도 매우 큰 정방향 전용의 읽기 전용 결과 집합을 처리할 수 있도록 합니다. 설정 하는 경우 유의 **selectMethod = cursor**모든 정방향 전용, 해당 연결에서 생성 하는 읽기 전용 결과 집합이 영향을 받습니다. 즉, 응용 프로그램에 정기적으로 몇 행이 있는 간단한 결과 집합 처리를 하는 경우 만들기, 읽기 및 각 결과 집합은 경우 보다 클라이언트 쪽 및 서버측 모두에서 더 많은 리소스를 사용 하 여 서버 커서를 닫으면 여기서는  **selectMethod** 로 설정 되지 않은 **커서**합니다.  
  
-   개체는 getBlob 또는 getClob 메서드 대신는 getAsciiStream, getBinaryStream, 또는 getCharacterStream 메서드를 사용 하 여 스트림으로 큰 텍스트 또는 이진 값을 읽습니다. 버전 1.2 릴리스 이상는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 제공 새 get\<유형 > Stream이 목적을 위해 메서드.  
  
-   잠재적으로 큰 값을 가진 열에 해당 하며 SELECT 문의 열 목록에서 마지막 배치를 확인 get\<형식 >의 메서드를 스트리밍하는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 해당 열에 액세스 하는 데 사용 되는 순서를 선택 합니다.  
  
-   OUT 잠재적으로 큰 값을 갖는 매개 변수는 마지막에 선언를 만드는 데 사용 되는 SQL에서 매개 변수 목록의 확인는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)합니다. 또한 get 확인\<형식 >의 메서드를 스트리밍하는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 선언 된 순서로 OUT 매개 변수에 액세스 하는 데 사용 됩니다.  
  
-   둘 이상의 문이 같은 연결에서 동시에 실행되지 않도록 합니다. 이전 문의 결과를 처리하기 전에 다른 문을 실행하면 처리되지 않은 결과가 응용 프로그램 메모리에 버퍼링될 수 있습니다.  
  
-   경우에 따라 사용 하 여 **selectMethod = cursor** 대신 **responseBuffering 적응 =** 와 같은 더 많은 이점을 제공할 것:  
  
    -   응용 프로그램에 정방향 전용 처리를 하는 경우 읽기 전용 결과 집합을 천천히를 사용 하 여 일부 사용자를 입력 한 후 각 행을 읽는 등 **selectMethod = cursor** 대신 **responseBuffering 적응 =** 수 리소스 사용량을 줄이는 데 도움이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   응용 프로그램이 두 개를 처리 하거나 동일한 연결에서 동시에 더 정방향 전용, 읽기 전용 결과 집합을 사용 하 여 **selectMethod = cursor** 대신 **responseBuffering 적응 =** 도움이 될 수 있습니다 이러한 결과 집합을 처리 하는 동안 드라이버에 필요한 메모리를 줄입니다.  
  
     두 경우 모두 서버 커서를 만들고 읽고 닫을 때 발생하는 오버헤드를 고려해야 합니다.  
  
 또한 다음 목록에서는 스크롤 및 업데이트가 가능한 정방향 전용 결과 집합에 대한 권장 사항에 대해 설명합니다.  
  
-   스크롤 가능한 결과 집합으로 표시 하는 행 수를 메모리로 읽어들입니다 드라이버의 경우 행 블록을 항상 인출는 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체, 경우에는 선택 버퍼링이 사용 됩니다. OutOfMemoryError 인해 스크롤을 호출 하 여 인출 된 행 수를 줄일 수 있습니다는 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 더 작은 개수의 행을 인출 크기를 설정 하는 개체 1도 가능, 필요한 경우. 이 OutOfMemoryError 해도 경우 스크롤 가능한 결과 집합에 아주 큰 열을 포함 하지 마십시오.  
  
-   정방향 전용 업데이트 가능 결과 집합, 데이터 집합으로 표시 하는 행 수를 메모리로 읽어들입니다 드라이버의 경우 행 블록을 정상적으로 인출 하는 경우는 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 도 선택 버퍼링 활성화 된 경우에 연결 합니다. 호출 하는 경우는 [다음](../../connect/jdbc/reference/next-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 는 OutOfMemoryError에 결과 개체를 호출 하 여 인출 된 행 수를 줄일 수 있습니다는 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 필요한 경우 반입 크기 1도 가능, 행의 더 작은 수로 설정 하는 개체입니다. 드라이버가 호출 하 여 행을 버퍼링 하지 강제할 수도 있습니다는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체 "**적응**" 하기 전에 매개 변수 문을 실행 합니다. 결과 집합 응용 프로그램이 get 중 하나를 사용 하 여 큰 열 값에 액세스 하는 경우 스크롤할 수 없기 때문에\<유형 > 스트림 메서드 드라이버는 값을 삭제와 같이 정방향 전용에 대 한 응용 프로그램 읽고 파일 되는 즉시 읽기 전용 결과 집합입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
