---
description: SQLXML을 사용한 프로그래밍
title: SQLXML을 사용한 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67766bb505750a4fbaaa1081dcf1d0441a44166e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438325"
---
# <a name="programming-with-sqlxml"></a>SQLXML을 사용한 프로그래밍
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 섹션에서는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API 메서드를 사용하여 **SQLXML** 개체를 통해 관계형 데이터베이스에 XML 문서를 저장하고 관계형 데이터베이스에서 검색하는 방법에 대해 설명합니다.  
  
 이 섹션에는 또한 SQLXML 개체 유형에 대한 정보 및 SQLXML 개체 사용과 관련된 중요 지침 및 제한 사항 목록이 포함되어 있습니다.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>SQLXML 개체를 사용하여 XML 데이터 읽기 및 쓰기  
 다음 목록은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API 메서드를 사용하여 SQLXML 개체를 통해 XML 데이터를 읽고 쓰는 방법에 대해 설명합니다.  
  
-   SQLXML 개체를 만들려면 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 메서드를 사용합니다. 이 메서드는 데이터가 포함되어 있지 않은 SQLXML 개체를 만듭니다. SQLXML 개체에 **xml** 데이터를 추가하려면 SQLXML 인터페이스에 지정된 메서드 setResult, setCharacterStream, setBinaryStream 또는 setString 중 하나를 호출합니다.  
  
-   SQLXML 개체 자체를 검색하려면 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 getSQLXML 메서드를 사용합니다.  
  
-   SQLXML 개체에서 **xml** 데이터를 검색하려면 SQLXML 인터페이스에 지정된 메서드 getSource, getCharacterStream, getBinaryStream 또는 getString중 하나를 사용합니다.  
  
-   SQLXML 개체의 **xml** 데이터를 업데이트하려면 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) 메서드를 사용합니다.  
  
-   **xml** 유형의 데이터베이스 테이블 열에 SQLXML 개체를 저장하려면 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 setSQLXML 메서드를 사용합니다.  
  
 [SQLXML 데이터 형식 샘플](../../connect/jdbc/sqlxml-data-type-sample.md)의 예제 코드는 이러한 일반적인 API 태스크를 수행하는 방법을 보여 줍니다.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>읽기 및 쓰기 가능한 SQLXML 개체  
 다음 표는 JDBC API에서 제공하는 setter, getter 및 updater 메서드에서 지원되는 SQLXML 개체 유형을 보여 줍니다. 표의 각 열은 다음을 가리킵니다.  
  
-   **메서드 이름** 열은 JDBC API에서 지원하는 getter, setter 및 updater 메서드를 나타냅니다.  
  
-   **Getter SQLXML 개체** 열은 SQLXML 개체를 나타내는데, 이 개체는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) 메서드 또는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) 메서드에 의해 생성됩니다.  
  
-   **Setter SQLXML 개체** 열은 SQLXML 개체를 나타내는데, 이 개체는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 메서드에 의해 생성됩니다. 아래 setter 메서드는 [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 메서드에 의해 생성된 SQLXML 개체만 사용합니다.  
  
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
  
 애플리케이션이 SQLXML 개체와 함께 소수 자릿수 또는 길이 매개 변수를 지정하여 setObject 메서드를 호출하면 해당 소수 자릿수 또는 길이 매개 변수는 무시됩니다.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>SQLXML 개체 사용과 관련된 지침 및 제한 사항  
 애플리케이션은 SQLXML 개체를 사용하여 데이터베이스에 대한 XML 데이터 읽기 및 쓰기 작업을 수행할 수 있습니다. 다음 목록에서는 SQLXML 개체 사용과 관련된 구체적인 제한 사항 및 지침을 보여 줍니다.  
  
-   SQLXML 개체는 해당 개체가 생성된 트랜잭션 기간 동안에만 유효합니다.  
  
-   getter 메서드로부터 받은 SQLXML 개체는 데이터를 읽는 데만 사용할 수 있습니다.  
  
-   연결 개체에 의해 생성된 SQLXML 개체는 데이터를 쓰는 데만 사용할 수 있습니다.  
  
-   애플리케이션은 읽기 가능한 SQLXML 개체에서 하나의 getter 메서드만 호출하여 데이터를 읽을 수 있습니다. getter 메서드가 호출되면 동일한 SQLXML 개체에 대한 다른 모든 getter 또는 setter 메서드는 실패합니다.  
  
-   애플리케이션은 SQLXML 개체를 읽거나 쓴 후 해당 개체에서 free 메서드만 호출할 수 있습니다. 그러나 기본 열 또는 매개 변수가 활성 상태인 동안에는 반환된 스트림 또는 원본을 처리할 수 있습니다. 기본 열 또는 매개 변수가 비활성 상태가 되면 해당 SQLXML 개체와 연결된 스트림 또는 원본이 닫힙니다. 기본 열 또는 매개 변수가 더 이상 유효하지 않은 경우 해당 기본 데이터를 Stream, SAX(Simple API for XML) 및 StAX(Streaming API for XML) getter에 사용할 수 없습니다.  
  
-   애플리케이션은 쓰기 가능한 SQLXML 개체에 대해 하나의 setter 메서드만 호출할 수 있습니다. setter 메서드가 호출되면 동일한 SQLXML 개체에 대한 다른 모든 setter 또는 getter 메서드는 실패합니다.  
  
-   SQLXML 개체에 데이터를 설정하려면 애플리케이션은 반환된 개체에서 적절한 setter 메서드 및 함수를 사용해야 합니다.  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 getSQLXML 메서드는 기본 열이 **null**인 경우 **null** 데이터를 반환합니다.  
  
-   setter 개체는 해당 개체가 생성된 연결이 유지되는 동안 유효합니다.  
  
-   애플리케이션은 SQLXML 인터페이스가 제공하는 setter 메서드를 사용하여 **null** 값을 설정할 수 없습니다. 애플리케이션은 SQLXML 인터페이스가 제공하는 setter 메서드를 사용하여 빈 문자열(&quot;&quot;)을 설정할 수 있습니다. **null** 값을 설정하려면 애플리케이션은 다음 중 하나를 호출해야 합니다.  
  
    -   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스의 setNull 메서드  
  
    -   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스의 setObject 메서드  
  
    -   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스의 setSQLXML 메서드(**null** 매개 변수 값 사용)  
  
-   XML 문서 작업을 수행할 때는 성능 문제 때문에 DOM(문서 개체 모델) 파서보다는 SAX(Simple API for XML) 및 StAX(Streaming API for XML) 파서를 사용하는 것이 좋습니다.  
  
 XML 파서는 빈 값을 처리할 수 없습니다. 그러나 SQL Server에서는 애플리케이션이 XML 데이터 형식의 데이터베이스 열에서 빈 값을 검색하거나 저장할 수 있도록 허용됩니다. 즉 XML 데이터를 구문 분석할 때 기본 값이 비어 있으면 파서에서 예외가 발생합니다. DOM 출력의 경우에는 JDBC 드라이버가 이 예외를 catch한 다음 오류를 발생시킵니다. SAX 및 Stax 출력의 경우에는 파서에서 직접 오류가 발생합니다.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>적응 버퍼링 및 SQLXML 지원  
 SQLXML 개체가 반환하는 이진 및 문자 스트림은 선택 또는 전체 버퍼링 모드를 따르지만 XML 파서가 스트림이 아닌 경우에는 선택 또는 전체 설정을 따르지 않습니다. 적응 버퍼링 사용에 대한 자세한 내용은 [적응 버퍼링 사용](../../connect/jdbc/using-adaptive-buffering.md)을 참조하세요.  
  
## <a name="see-also"></a>참조  
 [XML 데이터 지원](../../connect/jdbc/supporting-xml-data.md)  
  
  
