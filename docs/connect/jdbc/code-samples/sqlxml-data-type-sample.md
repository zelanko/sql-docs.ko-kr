---
title: SQLXML 데이터 형식 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac104dac28376dcbda85be60fa996fbc628e3654
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278754"
---
# <a name="sqlxml-data-type-sample"></a>SQLXML 데이터 형식 샘플
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램에서는 XML 데이터를 관계형 데이터베이스에 저장하는 방법, XML 데이터를 데이터베이스에서 검색하는 방법 및 **SQLXML** Java 데이터 형식으로 XML 데이터를 구문 분석하는 방법을 보여 줍니다.  
  
 이 섹션의 코드 예제에서는 SAX(Simple API for XML) 파서를 사용합니다. SAX는 XML 문서의 이벤트 기반 구문 분석을 위해 공개적으로 개발된 표준입니다. SAX는 XML 데이터 작업을 위한 응용 프로그래밍 인터페이스도 제공합니다. 응용 프로그램에서는 DOM(문서 개체 모델) 또는 StAX(Streaming API for XML) 등 다른 XML 파서도 사용할 수 있습니다.  
  
 DOM(문서 개체 모델)은 XML 문서, 조각, 노드 또는 노드 집합의 프로그래밍 방식 표현을 제공합니다. SAX는 XML 데이터 작업을 위한 응용 프로그래밍 인터페이스도 제공합니다. 마찬가지로 StAX(Streaming API for XML)는 끌어오기 방식의 XML 구문 분석용 Java 기반 API입니다.  
  
> [!IMPORTANT]  
>  SAX 파서 API를 사용하려면 javax.xml 패키지에서 표준 SAX 구현을 가져와야 합니다.  
  
 이 샘플의 코드 파일 이름은 SQLXMLExample.java이며 다음 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\datatypes  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행하려면 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc4.jar에 대한 항목이 없으면 샘플 응용 프로그램에서 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버를 사용 하 여](../../../connect/jdbc/using-the-jdbc-driver.md)입니다.  
  
 또한 이 샘플 응용 프로그램을 실행하려면 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다.  
  
## <a name="example"></a>예제  
 다음 예제의 샘플 코드에서는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 데이터베이스에 연결한 다음, createSampleTables 메서드를 호출합니다.  
  
 createSampleTables 메서드는 테스트 테이블인 TestTable1 및 TestTable2를 삭제합니다(있는 경우). 그런 다음 TestTable1에 행 2개를 삽입합니다.  
  
 또한 코드 샘플에는 다음과 같은 세 개의 메서드와 xampleContentHandler라는 클래스도 포함되어 있습니다.  
  
 ExampleContentHandler 클래스는 파서 이벤트에 대한 메서드를 정의하는 사용자 지정 콘텐츠 처리기를 구현합니다.  
  
 showGetters 메서드는 SAX, ContentHandler 및 XMLReader를 사용하여 SQLXML 개체의 데이터를 구문 분석하는 방법을 보여 줍니다. 먼저 코드 샘플에서는 사용자 지정 콘텐츠 처리기의 인스턴스인 ExampleContentHandler를 만듭니다. 다음으로는 TestTable1에서 데이터 집합을 반환하는 SQL 문을 만들고 실행합니다. 그런 다음 SAX 파서를 가져와서 XML 데이터를 구문 분석합니다.  
  
 showSetters 메서드는 SAX, ContentHandler 및 ResultSet을 사용하여 **xml** 열을 설정하는 방법을 보여 줍니다. 먼저 Connection 클래스의 [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 메서드를 사용하여 빈 SQLXML 개체를 만듭니다. 그런 다음 SQLXML 개체에 데이터를 쓰는 데 사용할 콘텐츠 처리기의 인스턴스를 가져옵니다. 그런 다음 TestTable1에 데이터를 씁니다. 마지막으로 샘플 코드는 결과 집합에 있는 데이터 행을 통해 반복하며 [getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) 메서드를 사용하여 XML 데이터를 읽습니다.  
  
 showTransformer 메서드는 SAX 및 Transformer를 사용하여 한 테이블에서 XML 데이터를 가져온 다음 다른 테이블에 삽입하는 방법을 보여 줍니다. 먼저 TestTable1에서 원본 SQLXML 개체를 검색합니다. 그런 다음, Connection 클래스의 [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) 메서드를 사용하여 빈 대상 SQLXML 개체를 만듭니다. 그런 다음 대상 SQLXML 개체를 업데이트하고 TestTable2에 XML 데이터를 씁니다. 마지막으로 샘플 코드는 결과 집합에 있는 데이터 행을 통해 반복하며 [getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) 메서드를 사용하여 TestTable2에서 XML 데이터를 읽습니다.  
  
 [!code[JDBC#UsingSQLXML1](../../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식 작업 &#40;JDBC&#41;](../../../connect/jdbc/working-with-data-types-jdbc.md)  
  
  
