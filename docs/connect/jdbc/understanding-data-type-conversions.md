---
title: 데이터 형식 변환 이해 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ed91f1b38f68715cd174a96cb2f0364fc060482
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027480"
---
# <a name="understanding-data-type-conversions"></a>데이터 형식 변환 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java 프로그래밍 언어 데이터 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 손쉽게 변환하기 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 JDBC 사양에서 요구하는 데이터 형식 변환 기능을 제공합니다. 유연성을 강화하기 위해 모든 형식은 **Object**, **String** 및 **byte[]** 데이터 형식 간에 변환할 수 있습니다.

## <a name="getter-method-conversions"></a>Getter 메서드 변환

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 기반으로 하는 다음 차트에는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 get\<Type>() 메서드에 대한 JDBC 드라이버의 변환 맵과 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 get\<Type> 메서드에서 지원되는 변환 등이 나와 있습니다.

![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

다음은 JDBC 드라이버의 getter 메서드에서 지원하는 세 가지 변환 범주입니다.

- **비손실(x)** : getter 형식이 원본 서버 유형과 동일하거나 작은 경우의 변환입니다. 예를 들어, 원본 서버 10진수 열에 대해 getBigDecimal을 호출하는 경우는 변환이 필요하지 않습니다.

- **변환(y)** : 변환이 일반적이고 Java 언어 변환 규칙을 따르는 경우 숫자 서버 유형을 Java 언어 형식으로 변환하는 것입니다. 이러한 변환의 경우 항상 전체 자릿수가 잘리고(반올림하지 않음) 오버플로는 좀 더 작은 대상 유형의 모듈로 처리합니다. 예를 들어 "1.9999"를 포함하는 기본 **decimal** 열에서 getInt를 호출하면 "1"이 반환되고, 기본 **decimal** 값이 "3000000000"이면 **int** 값이 "-1294967296"으로 오버플로됩니다.

- **데이터 의존(z)** : 원본 문자 형식에서 숫자 형식으로 변환하려면 문자 형식에 해당 형식으로 변환할 수 있는 값이 있어야 합니다. 그 외 다른 변환은 수행되지 않습니다. getter 형식에 비해 너무 큰 값은 잘못된 값입니다. 예를 들어, getInt가 "53"이 들어있는 varchar(50) 열에서 호출되면 값은 **int**로 반환됩니다. 하지만 원본 값이 "xyz" 또는 "3000000000"인 경우에는 오류가 발생합니다.

**binary**, **varbinary**, **varbinary(max)** 또는 **image** 열 데이터 형식에 대해 getString이 호출되는 경우 해당 값은 16진수 문자열 값으로 반환됩니다.

## <a name="updater-method-conversions"></a>Updater 메서드 변환

[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 update\<Type>() 메서드에 전달되는 Java 형식 데이터의 경우 다음 변환이 적용됩니다.

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

다음은 JDBC 드라이버의 updater 메서드에서 지원하는 세 가지 변환 범주입니다.

- **비손실(x)** : updater 형식이 원본 서버 유형과 동일하거나 작은 경우의 변환입니다. 예를 들어, 원본 서버 10진수 열에 대해 updateBigDecimal을 호출하는 경우는 변환이 필요하지 않습니다.

- **변환(y)** : 변환이 일반적이고 Java 언어 변환 규칙을 따르는 경우 숫자 서버 유형을 Java 언어 형식으로 변환하는 것입니다. 이러한 변환의 경우 항상 전체 자릿수가 잘리고(반올림하지 않음) 오버플로는 좀 더 작은 대상 유형의 모듈로로 처리됩니다. 예를 들어 "1.9999"를 포함하는 기본 **int** 열에서 updateDecimal을 호출하면 "1"이 반환되고, 기본 **decimal** 값이 "3000000000"이면 **int** 값이 "-1294967296"으로 오버플로됩니다.

- **데이터 의존(z)** : 원본 데이터 형식에서 대상 데이터 형식으로 변환하려면 포함된 값을 대상 형식으로 변환할 수 있어야 합니다. 그 외 다른 변환은 수행되지 않습니다. getter 형식에 비해 너무 큰 값은 잘못된 값입니다. 예를 들어, "53"이 들어있는 int 열에 대해 updateString를 호출하면 업데이트가 성공합니다. 하지만 원본 문자열 값이 "foo" 또는 "3000000000"인 경우에는 오류가 발생합니다.

**binary**, **varbinary**, **varbinary(max)** 또는 **image** 열 데이터 형식에 대해 updateString이 호출되는 경우 문자열 값이 16진수 문자열 값으로 처리됩니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 데이터 형식이 **XML**인 경우 데이터 값은 올바른 **XML**이어야 합니다. updateBytes, updateBinaryStream 또는 updateBlob 메서드를 호출하는 경우 데이터 값이 XML 문자의 16진수 문자열 표현이어야 합니다. 다음은 그 예입니다.

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

XML 문자가 특정 문자 인코딩을 사용하는 경우에는 BOM(바이트 순서 표시)이 필요합니다.

## <a name="setter-method-conversions"></a>Setter 메서드 변환

[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 set\<Type>() 메서드에 전달되는 Java 형식 데이터에 대해서는 다음과 같은 변환이 적용됩니다.

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

서버는 변환을 시도하고 실패하면 오류를 반환합니다.

**문자열** 데이터 형식의 경우 값이 **VARCHAR**의 길이를 초과 하는 경우에는이 값이 값이 **LONGVARCHAR** (가) (으)로 매핑됩니다. 마찬가지로 **NVARCHAR**는 값이 지원되는 **NVARCHAR** 길이를 초과하는 경우 **LONGNVARCHAR**에 매핑됩니다. **byte[]** 의 경우도 마찬가지입니다. **VARBINARY** 보다 긴 값은 **LONGVARBINARY** 고가 됩니다.

다음은 JDBC 드라이버의 setter 메서드에서 지원하는 두 가지 변환 범주입니다.

- **비손실(x)** : setter 형식이 원본 서버 유형과 동일하거나 작은 경우의 숫자 변환입니다. 예를 들어, 원본 서버 **10진수** 열에 대해 setBigDecimal을 호출하는 경우는 변환이 필요하지 않습니다. 숫자에서 문자로 변환하는 경우에는 Java **숫자** 데이터 형식이 **문자열**로 변환됩니다. 예를 들어 varchar(50) 열에 값 "53"으로 setDouble을 호출하면 해당 대상 열에 문자 값 "53"이 생성됩니다.

- **변환(y)** : Java **숫자** 형식을 보다 작은 원본 서버 **숫자** 형식으로 변환하는 것입니다. 이 변환은 일반적이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 규칙을 따릅니다. 또한 전체 자릿수는 항상 잘리고(반올림되지 않음) 오버플로가 발생하면 지원되지 않는 변환 오류가 발생합니다. 예를 들어, 원본 정수 열에 대해 "1.9999" 값으로 updateDecimal을 사용하면 대상 열 값이 "1"이 됩니다. 하지만 "3000000000"을 전달하면 드라이버에서 오류가 발생합니다.

- **데이터 의존(z)** : Java **문자열** 유형을 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환하려면 먼저 드라이버에서 **문자열** 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 전달하고 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 변환을 수행해야 합니다. sendStringParametersAsUnicode가 true로 설정되어 있고 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식이 **이미지**인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **nvarchar**에서 **이미지**로의 변환을 허용하지 않으며 SQLServerException이 발생합니다. sendStringParametersAsUnicode가 false로 설정되어 있고 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식이 **이미지**인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **varchar**에서 **이미지**로의 변환을 허용하며 예외가 발생하지 않습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 변환을 수행하고 문제가 발생하면 JDBC 드라이버에 오류를 전달합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 데이터 형식이 **XML**인 경우 데이터 값은 올바른 **XML**이어야 합니다. updateBytes, updateBinaryStream 또는 updateBlob 메서드를 호출하는 경우 데이터 값이 XML 문자의 16진수 문자열 표현이어야 합니다. 다음은 그 예입니다.

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

XML 문자가 특정 문자 인코딩을 사용하는 경우에는 BOM(바이트 순서 표시)이 필요합니다.

## <a name="conversions-on-setobject"></a>setObject에서의 변환

> [!NOTE]  
> Microsoft JDBC Driver 4.2 for SQL Server 이상에서는 JDBC 4.1 및 4.2를 지원합니다. 4\.1 및 4.2 데이터 형식 매핑 및 변환에 대한 자세한 내용은 아래 정보 이외에도 [JDBC 드라이버의 JDBC 4.1 준수](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) 및 [JDBC 드라이버의 JDBC 4.2 준수](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)를 참조하세요.

[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스의 setObject(\<Type>) 메서드에 전달되는 Java 형식 데이터에 대해서는 다음과 같은 변환이 적용됩니다.

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

대상 유형을 지정하지 않은 setObject 메서드는 기본 매핑을 사용합니다. **문자열** 데이터 형식의 경우 값이 **VARCHAR**의 길이를 초과 하는 경우에는이 값이 값이 **LONGVARCHAR** (가) (으)로 매핑됩니다. 마찬가지로 **NVARCHAR**는 값이 지원되는 **NVARCHAR** 길이를 초과하는 경우 **LONGNVARCHAR**에 매핑됩니다. **byte[]** 의 경우도 마찬가지입니다. **VARBINARY** 보다 긴 값은 **LONGVARBINARY** 고가 됩니다.

다음은 JDBC 드라이버의 setObject 메서드에서 지원하는 세 가지 변환 범주입니다.

- **비손실(x)** : setter 형식이 원본 서버 유형과 동일하거나 작은 경우의 숫자 변환입니다. 예를 들어, 원본 서버 **10진수** 열에 대해 setBigDecimal을 호출하는 경우는 변환이 필요하지 않습니다. 숫자에서 문자로 변환하는 경우에는 Java **숫자** 데이터 형식이 **문자열**로 변환됩니다. 예를 들어, 값이 "53"인 varchar(50) 열에 setDouble을 호출하면 해당 대상 열에 문자 값 "53"이 생성됩니다.

- **변환(y)** : Java **숫자** 형식을 보다 작은 원본 서버 **숫자** 형식으로 변환하는 것입니다. 이 변환은 일반적이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 규칙을 따릅니다. 전체 자릿수는 항상 잘리고(반올림되지 않음) 오버플로는 지원되지 않는 변환 오류를 throw합니다. 예를 들어, 원본 정수 열에 대해 "1.9999" 값으로 updateDecimal을 사용하면 대상 열 값이 "1"이 됩니다. 하지만 "3000000000"을 전달하면 드라이버에서 오류가 발생합니다.

- **데이터 의존(z)** : Java **문자열** 유형을 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환하려면 먼저 드라이버에서 **문자열** 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 전달하고 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 변환을 수행해야 합니다. sendStringParametersAsUnicode 연결 속성이 true로 설정되어 있고 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식이 **이미지**인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **nvarchar**에서 **이미지**로의 변환을 허용하지 않으며 SQLServerException이 발생합니다. sendStringParametersAsUnicode가 false로 설정되어 있고 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식이 **이미지**인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **varchar**에서 **이미지**로의 변환을 허용하며 예외가 발생하지 않습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 대량 설정 변환을 수행하고 문제가 발생하면 JDBC 드라이버에 오류를 전달합니다. 클라이언트 쪽 변환은 예외이며 **date**, **time**, **timestamp**, **Boolean**, **String** 값의 경우에만 수행됩니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 데이터 형식이 **XML**인 경우 데이터 값은 올바른 **XML**이어야 합니다. setObject(byte[], SQLXML), setObject(inputStream, SQLXML) 또는 setObject(Blob, SQLXML) 메서드를 호출하는 경우 데이터 값은 XML 문자의 16진수 문자열 표현이어야 합니다. 다음은 그 예입니다.

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

XML 문자가 특정 문자 인코딩을 사용하는 경우에는 BOM(바이트 순서 표시)이 필요합니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
