---
title: "큰 데이터 읽기 샘플 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25042ab3719067654e801ca936d99af1a49a1e47
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="reading-large-data-sample"></a>큰 데이터 읽기 샘플
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램에서 큰 단일 열 값을 검색 하는 방법을 보여 줍니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 사용 하 여 데이터베이스의 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 메서드.  
  
 이 샘플의 코드 파일 이름은 readLargeData.java이며 다음 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\adaptive  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행 하려면에 대 한 액세스 해야 합니다는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 또한 sqljdbc.jar 파일 또는 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc.jar 또는 sqljdbc4.jar에 대한 항목이 없으면 샘플 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여](../../../connect/jdbc/using-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sqljdbc.jar 및 sqljdbc4.jar 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용 수를 제공 합니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 샘플 코드에서는 연결에는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 데이터베이스입니다. 그런 다음 샘플 데이터를 만들고 매개 변수가 있는 쿼리를 사용하여 Production.Document 테이블을 업데이트합니다.  
  
 샘플 코드를 사용 하 여 선택 버퍼링 모드를 얻는 방법을 설명 하는 또한는 [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다. JDBC 드라이버 버전 2.0 릴리스 이상에서는 기본적으로 responseBuffering 연결 속성이 "adaptive"로 설정됩니다.  
  
 다음을 포함 하는 SQL 문을 사용 하는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 샘플 코드는 SQL 문을 실행 하 고에 반환 하는 데이터 개체는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
 마지막으로 샘플 코드에서 결과 집합에 포함 된 데이터의 행 반복 사용 하는 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 메서드 일부 포함 된 데이터에 액세스할 수 있습니다.  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [대규모 데이터 작업](../../../connect/jdbc/working-with-large-data.md)  
  
  

