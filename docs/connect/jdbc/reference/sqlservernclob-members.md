---
title: SQLServerNClob 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 303742b8e7b7bf8221565e09cf23d2e18cdca8de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970950"
---
# <a name="sqlservernclob-members"></a>SQLServerNClob 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|속성|설명|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|이 메서드는 **NCLOB** 개체 및 이 개체가 보유한 리소스를 해제합니다.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|**Java. nclob** 개체에 의해 지정 된 **NCLOB** 값을 ASCII 스트림으로 검색 합니다.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|**Java. nclob** 개체에 지정 된 **nclob** 값을 검색 합니다.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|**Java. nclob** 개체에 지정 된 **nclob** 값에서 지정 된 부분 문자열의 복사본을 검색 합니다.|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|**Java. nclob** 개체에 지정 된 **nclob** 값의 문자 수를 검색 합니다.|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|지정된 시작 위치에 따라 지정된 **java.sql.NClob** 개체 또는 해당 **java.sql.NClob**에 있는 부분 문자열의 문자 위치를 검색합니다.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|지정된 위치에서부터 ASCII 문자를 이 **java.sql.NClob** 개체가 나타내는 **NCLOB** 값에 쓰는 데 사용할 스트림을 검색합니다.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|지정된 위치에서부터 유니코드 문자의 스트림을 이 **java.sql.NClob** 개체가 나타내는 **NCLOB** 값에 쓰는 데 사용할 스트림을 검색합니다.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|지정 된 **문자열** 을 지정 된 위치에서 시작 하는 **NCLOB** 에 씁니다.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|**NCLOB**값을 지정된 길이로 자릅니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
