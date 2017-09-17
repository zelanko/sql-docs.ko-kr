---
title: "SQLXML을 사용한 프로그래밍 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5737ae7a0356f7697b254e67faa5cf715d2ffaef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="programming-with-sqlxml"></a>SQLXML을 사용한 프로그래밍
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 섹션에서는 사용 하는 방법을 설명는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 으로 관계형 데이터베이스에서 저장 하 고 XML을 검색 하기 위한 API 메서드 문서 **SQLXML** 개체입니다.  
  
 이 섹션에는 또한 SQLXML 개체 유형에 대한 정보 및 SQLXML 개체 사용과 관련된 중요 지침 및 제한 사항 목록이 포함되어 있습니다.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>SQLXML 개체를 사용하여 XML 데이터 읽기 및 쓰기  
 다음 목록에 사용 하는 방법에 설명 된 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API 메서드를 읽고 쓰는 SQLXML 개체를 사용 하 여 XML 데이터:  
  
-   SQLXML 개체를 만들려면 사용는 [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다. 이 메서드는 데이터가 포함되어 있지 않은 SQLXML 개체를 만듭니다. 추가할 **xml** SQLXML 개체에 데이터를 SQLXML 인터페이스에 지정 된 다음 방법 중 하나를 호출:, setBinaryStream, setCharacterStream, setResult 또는 setString 합니다.  
  
-   getSQLXML 메서드를 사용 하 여 SQLXML 개체 자체를 검색 하려면는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다.  
  
-   검색 하는 **xml** SQLXML 개체의 데이터는 SQLXML 인터페이스에 지정 된 다음 방법 중 하나를 사용 합니다: getSource, getCharacterStream, getBinaryStream, 또는 getString 합니다.  
  
-   업데이트 하는 **xml** SQLXML 개체의에서 데이터를 사용 하 여는 [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
-   형식의 데이터베이스 테이블 열에 SQLXML 개체를 저장 하려면 **xml**, setSQLXML 메서드를 사용는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)클래스입니다.  
  
 예제 코드에서는 [SQLXML 데이터 형식 샘플](../../connect/jdbc/sqlxml-data-type-sample.md) 이러한 일반적인 API 태스크를 수행 하는 방법을 보여 줍니다.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>읽기 및 쓰기 가능한 SQLXML 개체  
 다음 표는 JDBC API에서 제공하는 setter, getter 및 updater 메서드에서 지원되는 SQLXML 개체 유형을 보여 줍니다. 표의 각 열은 다음을 가리킵니다.  
  
-   **메서드 이름** 열은 JDBC API에서 지원 되는 getter, setter 및 updater 메서드를 보여 줍니다.  
  
-   **Getter SQLXML 개체** 열 하나를 통해 만들어진는 SQLXML 개체를 나타내며는 [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) 의 메서드는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 또는 [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
-   **Setter SQLXML 개체** 열은 SQLXML 개체를 나타내는으로 만들어진는 [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다. 아래 setter 메서드는에 의해 생성 된 SQLXML 개체만 동의 [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 메서드.  
  
|메서드 이름|Getter SQLXML 개체<br /><br /> (읽기 가능)|Setter SQLXML 개체<br /><br /> (쓰기 가능)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|지원되지 않음|지원됨|  
|CallableStatement.setObject()|지원되지 않음|지원됨|  
|PreparedStatement.setSQLXML()|지원되지 않음|지원됨|  
|PreparedStatement.setObject()|지원되지 않음|지원됨|  
|ResultSet.updateSQLXML()|지원되지 않음|지원됨|  
|ResultSet.updateObject()|지원되지 않음|지원됨|  
|ResultSet.getSQLXML()|지원됨|지원되지 않음|  
|CallableStatement.getSQLXML()|지원됨|지원되지 않음|  
  
 위 표에서 보듯이 setter SQLXML 메서드는 읽기 가능한 SQLXML 개체에 사용할 수 없고 마찬가지로 getter 메서드는 쓰기 가능한 SQLXML 개체에 사용할 수 없습니다.  
  
 SQLXML 개체와 소수 자릿수 또는 길이 매개 변수를 지정 하 여 setObject 메서드를 호출 하는 응용 프로그램, 소수 자릿수 또는 길이 매개 변수는 무시 됩니다.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>SQLXML 개체 사용과 관련된 지침 및 제한 사항  
 응용 프로그램은 SQLXML 개체를 사용하여 데이터베이스에 대한 XML 데이터 읽기 및 쓰기 작업을 수행할 수 있습니다. 다음 목록에서는 SQLXML 개체 사용과 관련된 구체적인 제한 사항 및 지침을 보여 줍니다.  
  
-   SQLXML 개체는 해당 개체가 생성된 트랜잭션 기간 동안에만 유효합니다.  
  
-   getter 메서드로부터 받은 SQLXML 개체는 데이터를 읽는 데만 사용할 수 있습니다.  
  
-   연결 개체에 의해 생성된 SQLXML 개체는 데이터를 쓰는 데만 사용할 수 있습니다.  
  
-   응용 프로그램은 읽기 가능한 SQLXML 개체에서 하나의 getter 메서드만 호출하여 데이터를 읽을 수 있습니다. getter 메서드가 호출되면 동일한 SQLXML 개체에 대한 다른 모든 getter 또는 setter 메서드는 실패합니다.  
  
-   읽거나 쓴 후 응용 프로그램에서 SQLXML 개체에 대해 가능한 메서드만을 호출할 수 있습니다. 그러나 기본 열 또는 매개 변수가 활성 상태인 동안에는 반환된 스트림 또는 원본을 처리할 수 있습니다. 기본 열 또는 매개 변수가 비활성 상태가 되면 해당 SQLXML 개체와 연결된 스트림 또는 원본이 닫힙니다. 기본 열 또는 매개 변수가 더 이상 유효하지 않은 경우 해당 기본 데이터를 Stream, SAX(Simple API for XML) 및 StAX(Streaming API for XML) getter에 사용할 수 없습니다.  
  
-   응용 프로그램은 쓰기 가능한 SQLXML 개체에 대해 하나의 setter 메서드만 호출할 수 있습니다. setter 메서드가 호출되면 동일한 SQLXML 개체에 대한 다른 모든 setter 또는 getter 메서드는 실패합니다.  
  
-   SQLXML 개체에 데이터를 설정하려면 응용 프로그램은 반환된 개체에서 적절한 setter 메서드 및 함수를 사용해야 합니다.  
  
-   getSQLXML 메서드는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 반환 클래스 **null** 데이터 원본 열이 **null**합니다.  
  
-   setter 개체는 해당 개체가 생성된 연결이 유지되는 동안 유효합니다.  
  
-   응용 프로그램 설정할 수 없습니다는 **null** SQLXML 인터페이스가 제공 하는 setter 메서드를 사용 하 여 값입니다. 응용 프로그램은 SQLXML 인터페이스가 제공하는 setter 메서드를 사용하여 빈 문자열("")을 설정할 수 있습니다. 설정 하는 **null** 값, 응용 프로그램 호출 해야 다음 중 하나:  
  
    -   SetNull 메서드는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스입니다.  
  
    -   setObject 메서드에 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스입니다.  
  
    -   SetSQLXML 메서드는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스와 **null** 매개 변수 값입니다.  
  
-   XML 문서 작업을 수행할 때는 성능 문제 때문에 DOM(문서 개체 모델) 파서보다는 SAX(Simple API for XML) 및 StAX(Streaming API for XML) 파서를 사용하는 것이 좋습니다.  
  
 XML 파서는 빈 값을 처리할 수 없습니다. 그러나 SQL Server에서는 응용 프로그램이 XML 데이터 형식의 데이터베이스 열에서 빈 값을 검색하거나 저장할 수 있도록 허용됩니다. 즉 XML 데이터를 구문 분석할 때 기본 값이 비어 있으면 파서에서 예외가 발생합니다. DOM 출력의 경우에는 JDBC 드라이버가 이 예외를 catch한 다음 오류를 발생시킵니다. SAX 및 Stax 출력의 경우에는 파서에서 직접 오류가 발생합니다.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>선택 버퍼링 및 SQLXML 지원  
 SQLXML 개체가 반환하는 이진 및 문자 스트림은 선택 또는 전체 버퍼링 모드를 따르지만 XML 파서가 스트림이 아닌 경우에는 선택 또는 전체 설정을 따르지 않습니다. 선택 버퍼링 하는 방법에 대 한 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 지원](../../connect/jdbc/supporting-xml-data.md)  
  
  
