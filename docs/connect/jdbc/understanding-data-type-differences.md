---
title: 데이터 형식 차이 이해
description: Java 프로그래밍 언어 데이터 형식과 SQL Server 데이터 형식 간의 차이점 및 JDBC Driver for SQL Server를 사용하여 변환하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16eea906570c9ec19e83246df5073f6ac72e2403
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728370"
---
# <a name="understanding-data-type-differences"></a>데이터 형식 차이 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java 프로그래밍 언어 데이터 형식과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 간에는 많은 차이가 있습니다. 그러나 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 다양한 형식 변환 기능을 통해 이러한 차이를 손쉽게 극복합니다.  

## <a name="character-types"></a>문자 형식

JDBC 문자열 데이터 형식은 **CHAR**, **VARCHAR**및 **longvarchar**입니다. JDBC 드라이버는 JDBC 4.0 API를 지원합니다. JDBC 4.0에서 JDBC 문자열 데이터 형식은 **NCHAR**, **NVARCHAR** 및 **LONGNVARCHAR**일 수도 있습니다. 이러한 새 문자열 형식은 유니코드 형식으로 Java 네이티브 문자 형식을 유지하므로 ANSI와 Unicode 간 변환을 수행할 필요가 없습니다.  
  
| Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 고정 길이    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Char** 및 **nchar** 데이터 형식은 JDBC **CHAR** 및 **NCHAR** 형식에 직접 매핑됩니다. 이는 해당 열에 `SET ANSI_PADDING ON`이 설정된 경우 서버에서 패딩을 제공하는 고정 길이 형식입니다. **nchar**에 대해서는 패딩이 항상 설정되어 있지만 **char**에 대해서는 그렇지 않습니다. 서버 char 열이 패딩되지 않은 경우 JDBC 드라이버에서 패딩을 추가합니다.                                                                                                                                                                                                                                                                                                                                                                                      |
| 가변 길이 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar** 및 **nvarchar** 형식은 각각 JDBC **VARCHAR** 및 **NVARCHAR** 형식에 직접 매핑됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| long            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **text** 및 **ntext** 형식은 각각 JDBC 이상 **LONGVARCHAR** 및 **LONGNVARCHAR** 형식에 매핑됩니다. 이러한 형식은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 더 이상 사용되지 않습니다. 큰 값 형식 **varchar(max)** 또는 **nvarchar(max)** 를 대신 사용해야 합니다.<br /><br /> update\<Numeric Type> 및 [updateObject(int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) 메서드를 사용하면 **text** 및 **ntext** 서버 열에 대해 실패합니다. 그러나 **text** 및 **ntext** 서버 열에 대해 [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 메서드를 지정된 문자 변환 형식과 함께 사용할 수 있습니다. |
  
## <a name="binary-string-types"></a>이진 문자열 형식

JDBC 이진 문자열 형식은 **binary**, **VARBINARY**및 **longvarbinary**입니다.  
  
| Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 고정 길이    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary** 형식은 JDBC **BINARY** 형식에 직접 매핑됩니다. 이는 해당 열에 SET ANSI_PADDING ON이 설정된 경우 서버에서 패딩을 제공하는 고정 길이 형식입니다. 서버 char 열이 패딩되지 않으면 JDBC 드라이버가 패딩을 추가합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** 형식은 고정 길이가 8바이트인 JDBC **BINARY**형식입니다. |
| 가변 길이 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary** 형식은 JDBC **VARBINARY** 형식에 매핑됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 **udt** 형식은 JDBC **VARBINARY** 형식에 매핑됩니다.                                                                                                                                                                                                                                 |
| long            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **image** 형식은 JDBC **LONGVARBINARY** 형식에 매핑됩니다. 이 형식은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 사용되지 않으므로 대신 큰 값 형식인 **varbinary(max)** 를 사용해야 합니다.                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>정확한 숫자 형식

JDBC의 정확한 숫자 형식은 해당되는 SQL Server 형식에 바로 매핑됩니다.  
  
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | JDBC **BIT** 형식은 단일 비트(0 또는 1)를 나타냅니다. 이 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** 형식에 매핑됩니다.                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | JDBC **TINYINT** 형식은 단일 바이트를 나타내며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** 형식에 매핑됩니다.                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | JDBC **SMALLINT** 형식은 부호 있는 16비트 정수를 나타내며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint** 형식에 매핑됩니다.                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | JDBC **INTEGER** 형식은 부호 있는 32비트 정수를 나타내며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** 형식에 매핑됩니다.                                                                                                                                                                                                                                                                                                                                           |
| bigint   | JDBC **BIGINT** 형식은 부호 있는 64비트 정수를 나타내며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint** 형식에 매핑됩니다.                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | JDBC **NUMERIC** 형식은 동일한 전체 자릿수 값을 포함하는 고정 전체 자릿수 소수 값을 나타냅니다. **NUMERIC** 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **numeric** 형식에 매핑됩니다.                                                                                                                                                                                                                                                                   |
| DECIMAL  | JDBC **DECIMAL** 형식은 최소한 지정된 전체 자릿수 값을 포함하는 고정 전체 자릿수 소수 값을 나타냅니다. **DECIMAL** 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimal** 형식에 매핑됩니다.<br /><br /> JDBC **DECIMAL** 형식도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** 및 **smallmoney** 형식에 매핑됩니다. 이 형식은 각각 8바이트와 4바이트로 저장되는 특정 고정 전체 자릿수 10진수 형식입니다. |
  
## <a name="approximate-numeric-types"></a>근사치 형식

JDBC 근사치 형식은 **REAL**, **DOUBLE** 및 **FLOAT**입니다.  
  
| Type   | Description                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | JDBC **REAL** 형식의 전체 자릿수는 7(단정밀도)이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real** 형식에 직접 매핑됩니다.                                                                                                                                     |
| DOUBLE | JDBC **DOUBLE** 형식의 전체 자릿수는 15(배정밀도)이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float** 형식에 매핑됩니다. JDBC **FLOAT** 형식은 **DOUBLE**의 동의어입니다. **FLOAT**와 **DOUBLE** 사이에 혼동이 있을 수 있으므로 **DOUBLE**이 선호됩니다. |
  
## <a name="datetime-types"></a>날짜 및 시간 형식

JDBC **TIMESTAMP** 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 및 **smalldatetime** 형식에 매핑됩니다. **datetime** 형식은 두 개의 4바이트 정수로 저장됩니다. **smalldatetime** 형식은 2바이트 small 정수와 동일한 정보(날짜 및 시간)를 포함하지만 정확도는 떨어집니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** 형식은 고정 길이 이진 문자열 형식입니다. JDBC 시간 형식 **DATE**, **TIME** 또는 **TIMESTAMP**에는 매핑되지 않습니다.  
  
## <a name="custom-type-mapping"></a>사용자 지정 형식 매핑

JDBC 고급 형식(UDT, Struct 등)에 대해 SQLData 인터페이스를 사용하는 JDBC의 사용자 지정 형식 매핑 기능이며 JDBC 드라이버에 구현되어 있지 않습니다.  
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
