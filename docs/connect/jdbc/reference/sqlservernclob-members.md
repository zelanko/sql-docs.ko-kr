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
manager: jroth
ms.openlocfilehash: 8386d896391405777648ee3ec27b188b313c737c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66788956"
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
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|검색을 **NCLOB** 값으로 지정 합니다 **java.sql.NClob** 을 ASCII 스트림으로 개체.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|검색을 **NCLOB** 값으로 지정 합니다 **java.sql.NClob** 개체.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|지정된 된 부분 문자열의 복사본을 검색 합니다 **NCLOB** 로 지정 된 값을 **java.sql.NClob** 개체입니다.|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|문자 수를 검색 합니다 **NCLOB** 값으로 지정 합니다 **java.sql.NClob** 개체.|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|지정된 시작 위치에 따라 지정된 **java.sql.NClob** 개체 또는 해당 **java.sql.NClob**에 있는 부분 문자열의 문자 위치를 검색합니다.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|지정된 위치에서부터 ASCII 문자를 이 **java.sql.NClob** 개체가 나타내는 **NCLOB** 값에 쓰는 데 사용할 스트림을 검색합니다.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|지정된 위치에서부터 유니코드 문자의 스트림을 이 **java.sql.NClob** 개체가 나타내는 **NCLOB** 값에 쓰는 데 사용할 스트림을 검색합니다.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|지정 된 기록 **문자열** 에 **NCLOB** 지정된 된 위치에서 시작 합니다.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|**NCLOB**값을 지정된 길이로 자릅니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
