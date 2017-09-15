---
title: "이해 데이터 형식 변환 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b8a4439d9682435baca0867dfc9d8bd96d0fcd7c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-data-type-conversions"></a>데이터 형식 변환 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 Java 프로그래밍 언어 데이터 형식을 변환 하는 과정을 용이 하 게 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식에는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 는 JDBC 사양에서 필요에 따라 데이터 형식 변환을 제공 합니다. 유연성을 모든 종류는 사이에 변환 될 **개체**, **문자열**, 및 **byte** 데이터 형식입니다.  
  
## <a name="getter-method-conversions"></a>Getter 메서드 변환  
 에 따라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 다음 차트에는 데이터 형식을 포함 get에 대 한 JDBC 드라이버의 변환 맵과\<형식 >의 () 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스 및 지원 되는 변환에 대 한 get\< 형식 >의 메서드는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다.  
  
 ![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")  
  
 다음은 JDBC 드라이버의 getter 메서드에서 지원하는 세 가지 변환 범주입니다.  
  
-   **비손실 (x)**: getter 형식이 동일한 경우에는 변환 하거나 원본 서버 유형과 작은 합니다. 예를 들어 원본 서버 10 진수 열에 getBigDecimal를 호출할 때 변환이 필요 하지 않습니다.  
  
-   **변환된 (y)**: 숫자 서버 유형을 Java 언어 형식 위치는 변환은 일반적 이며 Java 언어 변환 규칙을 따르는 변환 합니다. 이러한 변환의 경우 항상 전체 자릿수가 잘리고(반올림하지 않음) 오버플로는 좀 더 작은 대상 유형의 모듈로 처리합니다. 예를 들어 getInt는 내부에서 호출 **10 진수** "1.9999"를 포함 하는 열은 "1"을 반환 하거나 내부 **10 진수** 값이 "3000000000" 하면 **int** 값 "-1294967296"를 오버플로합니다.  
  
-   **데이터 의존 (z)**: 원본 문자 형식에서 숫자 형식으로 변환 문자 형식 해당 형식으로 변환 될 수 있는 값을 포함 되도록 해야 합니다. 그 외 다른 변환은 수행되지 않습니다. getter 형식에 비해 너무 큰 값은 잘못된 값입니다. 예를 들어 getInt "53"이 들어 있는 varchar (50) 열에서 호출 되는 경우 값이 반환 됩니다로 **int**; 하지만 원본 값이 "xyz" 또는 "3000000000"을 하는 경우 오류가 throw 됩니다.  
  
 GetString에서 호출 되는 **이진**, **varbinary**, **varbinary (max)**, 또는 **이미지** 열 데이터 형식에 값으로 반환 되는 16 진수 문자열 값입니다.  
  
## <a name="updater-method-conversions"></a>Updater 메서드 변환  
 Java 형식 데이터 업데이트에 전달 된\<형식 >의 () 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스, 다음과 같은 변환이 적용 됩니다.  
  
 ![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")  
  
 다음은 JDBC 드라이버의 updater 메서드에서 지원하는 세 가지 변환 범주입니다.  
  
-   **비손실 (x)**: updater 형식이 동일한 경우에는 변환 하거나 원본 서버 유형과 작은 합니다. 예를 들어, 원본 서버 10진수 열에 대해 updateBigDecimal을 호출하는 경우는 변환이 필요하지 않습니다.  
  
-   **변환된 (y)**: 숫자 서버 유형을 Java 언어 형식 위치는 변환은 일반적 이며 Java 언어 변환 규칙을 따르는 변환 합니다. 이러한 변환의 경우 항상 전체 자릿수가 잘리고(반올림하지 않음) 오버플로는 좀 더 작은 대상 유형의 모듈로로 처리됩니다. 예를 들어 updateDecimal는 내부에서 호출 **int** "1.9999"를 포함 하는 열은 "1"을 반환 하거나 내부 **10 진수** 값이 "3000000000" 하면 **int**값이 "-1294967296"를 오버플로 합니다.  
  
-   **데이터 의존 (z)**: 대상 데이터 형식으로 원본 데이터 형식에서 변환 포함된 된 값 대상 형식으로 변환할 수 있어야 합니다. 그 외 다른 변환은 수행되지 않습니다. getter 형식에 비해 너무 큰 값은 잘못된 값입니다. 예를 들어, "53"이 들어있는 int 열에 대해 updateString를 호출하면 업데이트가 성공합니다. 하지만 원본 문자열 값이 "foo" 또는 "3000000000"인 경우에는 오류가 발생합니다.  
  
 updateString를 호출 하는 경우는 **이진**, **varbinary**, **varbinary (max)**, 또는 **이미지** 문자열 값을 처리 열 데이터 형식 16 진수 문자열 값입니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 열 데이터 형식이 **XML**, 데이터 값은 올바른 이어야 합니다 **XML**합니다. UpdateBytes, updateBinaryStream, updateBlob 메서드를 호출할 때 데이터 값은 XML 문자의 16 진수 문자열 표현 이어야 합니다. 예를 들어  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 XML 문자가 특정 문자 인코딩을 사용하는 경우에는 BOM(바이트 순서 표시)이 필요합니다.  
  
## <a name="setter-method-conversions"></a>Setter 메서드 변환  
 Java 형식 데이터 집합에 전달 된\<형식 >의 () 메서드는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스, 다음과 같은 변환이 적용 됩니다.  
  
 ![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")  
  
 서버는 변환을 시도하고 실패하면 오류를 반환합니다.  
  
 경우에 **문자열** 데이터 형식으로 값의 길이 초과 하는 경우 **VARCHAR**, 매핑될 **LONGVARCHAR**합니다. 마찬가지로, **NVARCHAR** 매핑됩니다 **LONGNVARCHAR** 값의 지원 되는 길이 초과 하는 경우 **NVARCHAR**합니다. 같은 기준이 **byte**합니다. 보다 긴 값 **VARBINARY** 될 **LONGVARBINARY**합니다.  
  
 다음은 JDBC 드라이버의 setter 메서드에서 지원하는 두 가지 변환 범주입니다.  
  
-   **비손실 (x)**: setter 형식이 동일한 경우의 숫자에 대 한 변환 하거나 원본 서버 유형과 작은 합니다. 예를 들어, 원본 서버에서 setBigDecimal를 호출할 때 **10 진수** 열 변환이 필요 하지 않습니다. Java 문자 경우에는 숫자에 대 한 **숫자** 데이터 형식을 변환할는 **문자열**합니다. 예를 들어 varchar (50) 열에 값이 "53" 인 setDouble 호출 해당 대상 열에 문자 값 "53"를 생성 합니다.  
  
-   **변환된 (y)**: Java **숫자** 원본 서버 형식 **숫자** 작은 형식입니다. 이 변환은 일반적 이며 뒤에 오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변환 규칙입니다. 또한 전체 자릿수는 항상 잘리고(반올림되지 않음) 오버플로가 발생하면 지원되지 않는 변환 오류가 발생합니다. 예를 들어 updateDecimal에 "1.9999"에서 원본 정수 열 대상 열에 "1"의 값을 사용 하지만 "3000000000"을 전달 하면 드라이버에서 오류가 발생 합니다.  
  
-   **데이터 의존 (z)**: Java **문자열** 내부에 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식은 다음 조건에 따라 다릅니다.: 드라이버 보냅니다는 **문자열** 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 필요할 경우, 변환을 수행 합니다. SendStringParametersAsUnicode true이 고 내부로 설정 되어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식이 **이미지**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로 변환을 허용 하지 않는 **nvarchar** 를 **이미지** sqlserverexception이 발생 하 고 있습니다. SendStringParametersAsUnicode가 false로 설정 되며 기본 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식이 **이미지**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 변환을 허용 **varchar** 를 **이미지**하며 예외를 throw 하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]변환을 수행 하 고 문제가 있는 경우 JDBC 드라이버에 오류를 전달 합니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 열 데이터 형식이 **XML**, 데이터 값은 올바른 이어야 합니다 **XML**합니다. UpdateBytes, updateBinaryStream, updateBlob 메서드를 호출할 때 데이터 값은 XML 문자의 16 진수 문자열 표현 이어야 합니다. 예를 들어  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 XML 문자가 특정 문자 인코딩을 사용하는 경우에는 BOM(바이트 순서 표시)이 필요합니다.  
  
## <a name="conversions-on-setobject"></a>setObject에서의 변환  
  
> [!NOTE]  
>  Microsoft JDBC Driver 4.2 (이상) SQL Server는 JDBC 4.1 및 4.2 지원에 대 한 합니다. 4.1 및 4.2 데이터 형식 매핑 및 변환에 대 한 자세한 내용은 참조 [JDBC 드라이버에 대 한 JDBC 4.1 준수](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) 및 [JDBC 드라이버의 JDBC 4.2 준수](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), 아래 정보 외에도 합니다.  
  
 Java 형식 데이터의 setObject에 전달 된 (\<유형 >)의 메서드는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스, 다음과 같은 변환이 적용 됩니다.  
  
 ![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")  
  
 지정 된 대상 형식이 없는 setObject 메서드는 기본 매핑을 사용 합니다. 경우에 **문자열** 데이터 형식으로 값의 길이 초과 하는 경우 **VARCHAR**, 매핑될 **LONGVARCHAR**합니다. 마찬가지로, **NVARCHAR** 매핑됩니다 **LONGNVARCHAR** 값의 지원 되는 길이 초과 하는 경우 **NVARCHAR**합니다. 같은 기준이 **byte**합니다. 보다 긴 값 **VARBINARY** 될 **LONGVARBINARY**합니다.  
  
 다음은 JDBC 드라이버의 setObject 메서드에서 지원하는 세 가지 변환 범주입니다.  
  
-   **비손실 (x)**: setter 형식이 동일한 경우의 숫자에 대 한 변환 하거나 원본 서버 유형과 작은 합니다. 예를 들어, 원본 서버에서 setBigDecimal를 호출할 때 **10 진수** 열 변환이 필요 하지 않습니다. Java 문자 경우에는 숫자에 대 한 **숫자** 데이터 형식을 변환할는 **문자열**합니다. 예를 들어 varchar (50) 열에 값이 "53" 인 setDouble 호출 해당 대상 열에 문자 값 "53" 생성 됩니다.  
  
-   **변환된 (y)**: Java **숫자** 원본 서버 형식 **숫자** 작은 형식입니다. 이 변환은 일반적 이며 뒤에 오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변환 규칙입니다. 또한 전체 자릿수는 항상 잘리고(반올림되지 않음) 오버플로로 인해 지원되지 않는 변환 오류가 발생합니다. 예를 들어 updateDecimal에 "1.9999"에서 원본 정수 열 대상 열에 "1"의 값을 사용 하지만 "3000000000"을 전달 하면 드라이버에서 오류가 발생 합니다.  
  
-   **데이터 의존 (z)**: Java **문자열** 내부에 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식은 다음 조건에 따라 다릅니다.: 드라이버 보냅니다는 **문자열** 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 필요할 경우, 변환을 수행 합니다. SendStringParametersAsUnicode 연결 속성이 true이 고 내부로 설정 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식이 **이미지**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로 변환을 허용 하지 않는 **nvarchar** 를**이미지** sqlserverexception이 발생 하 고 있습니다. SendStringParametersAsUnicode가 false로 설정 되며 기본 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식이 **이미지**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 변환을 허용 **varchar** 를 **이미지**하며 예외를 throw 하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]대량 설정 변환을 수행 하 고 문제가 있는 경우 JDBC 드라이버에 오류를 전달 합니다. 클라이언트 쪽 변환은 예외 이며만의 경우에 수행 **날짜**, **시간**, **타임 스탬프**, **부울**, 및 ** 문자열** 값입니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 열 데이터 형식이 **XML**, 데이터 값은 올바른 이어야 합니다 **XML**합니다. setObject(byte[], SQLXML), setObject(inputStream, SQLXML) 또는 setObject(Blob, SQLXML) 메서드를 호출하는 경우 데이터 값은 XML 문자의 16진수 문자열 표현이어야 합니다. 예를 들어  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 XML 문자가 특정 문자 인코딩을 사용하는 경우에는 BOM(바이트 순서 표시)이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
