---
title: 큰 데이터 업데이트 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc64e76d59b2d6957685c40c09d64e2c1a3d0dec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="updating-large-data-sample"></a>큰 데이터 업데이트 샘플
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램 데이터베이스의 큰 열을 업데이트 하는 방법을 보여 줍니다.  
  
 이 샘플의 코드 파일 이름은 updateLargeData.java이며 다음 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\adaptive  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행 하려면에 대 한 액세스 해야 합니다는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 또한 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc4.jar 파일에 대한 항목이 없으면 샘플 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 클래스 라이브러리 파일을 사용 하 여 기본 Java Runtime Environment (JRE) 설정에 따라 제공 합니다. 이 샘플에서는 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 및 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 드라이버 관련 응답 버퍼링 메서드에 액세스 하려면 JDBC 4.0 API를 소개 하는 방법입니다. 이 샘플을 컴파일하고 실행하려면 JDBC 4.0을 지원하는 sqljdbc4.jar 클래스 라이브러리가 있어야 합니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 샘플 코드에서는 연결에는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 데이터베이스입니다. 그런 다음 샘플 코드에서 Statement 개체를 만들고 사용 하 여 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 문 개체가 지정 된에 대 한 래퍼 인지 여부를 확인 하는 메서드 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다. [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 메서드는 드라이버 관련 응답 버퍼링 메서드에 액세스 하는 데 사용 됩니다.  
  
 샘플 코드에서는 응답 버퍼링 모드를 설정 하는 다음으로, "**적응**"를 사용 하 여는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스도 선택 버퍼링 모드를 가져오는 방법을 보여 줍니다.  
  
 그런 다음 SQL 문을 실행 하 고는 업데이트 가능한에 반환 하는 데이터 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
 마지막으로 결과 집합에 포함된 데이터 행을 반복합니다. 조합을 사용 하 여 빈 문서를 지정 하지 않고 요약 찾으면 [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 및 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 데이터의 행을 업데이트 하 고 다시 데이터베이스에 유지 하는 메서드. 사용 하 여 이미 있는 경우 데이터를는 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 메서드를 일부 포함 된 데이터를 표시 합니다.  
  
 드라이버의 기본 동작은 "**적응.**" 그러나 정방향 전용 업데이트 가능 결과 집합 및 결과 집합의 데이터를 응용 프로그램 메모리 보다 큰 경우에 대 한 응용 프로그램에 사용 하 여 명시적으로 선택 버퍼링 모드를 설정 하는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다.  
  
 [!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [대규모 데이터 작업](../../connect/jdbc/working-with-large-data.md)  
  
  
