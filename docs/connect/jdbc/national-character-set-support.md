---
title: 국가별 문자 집합 지원 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ceb2d12ba3d062b3ba592eb6baa93fe93223907
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80912219"
---
# <a name="national-character-set-support"></a>국가별 문자 집합 지원
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서는 이제 JDBC 4.0 API를 지원하며 새로운 국가별 문자 집합 변환 API 메서드를 제공합니다. 이 지원에는 **NCHAR**, **NVARCHAR**, **LONGNVARCHAR** 및 **NCLOB** JDBC 형식의 새로운 setter, getter 및 updater 메서드가 포함됩니다.  
  
 다음은 국가별 문자 집합 변환을 지원하는 새로운 getter, setter 및 updater 메서드 목록입니다.  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)  
  
> [!NOTE]  
>  애플리케이션에서 이러한 메서드를 사용하려면 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다.  
  
 문자열 매개 변수를 유니코드 형식으로 서버에 보내기 위해 애플리케이션은 새 JDBC 4.0 국가별 문자 메서드를 사용하거나 국가별 문자 메서드 이외의 메서드를 사용하는 경우 **sendStringParametersAsUnicode** 연결 속성을 "**true**"로 설정해야 합니다. 가능한 한 새 JDBC 4.0 국가별 문자 메서드를 사용하는 것이 좋습니다. **sendStringParametersAsUnicode** 연결 속성에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
