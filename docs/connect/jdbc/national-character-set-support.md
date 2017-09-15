---
title: "국가별 문자 집합 지원 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f143d37911a1375a1eebe9de04c8b509817575ec
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="national-character-set-support"></a>국가별 문자 집합 지원
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서는 이제 JDBC 4.0 API를 지원하며 새로운 국가별 문자 집합 변환 API 메서드를 제공합니다. 이 지원에 대 한 새로운 setter, getter 및 updater 메서드를 포함 **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, 및 **NCLOB** JDBC 형식입니다.  
  
 다음은 국가별 문자 집합 변환을 지원하는 새로운 getter, setter 및 updater 메서드 목록입니다.  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)합니다.  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)합니다.  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)합니다.  
  
> [!NOTE]  
>  응용 프로그램에서 이러한 메서드를 사용하려면 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다.  
  
 문자열 매개 변수를 서버에 유니코드 형식으로 보내려면 응용 프로그램은 새 JDBC 4.0 국가별 문자 메서드를 사용 하거나 해야 설정 또는 **sendStringParametersAsUnicode** 연결 속성을 "**true**" 비 국가별 문자 메서드를 사용 하는 경우. 가능한 한 새 JDBC 4.0 국가별 문자 메서드를 사용하는 것이 좋습니다. 에 대 한 자세한 내용은 **sendStringParametersAsUnicode** 연결 속성 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
