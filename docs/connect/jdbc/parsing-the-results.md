---
title: 결과 구문 분석 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 127c97ec155ef1e19df4103b12a6e10b8b67fe74
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027857"
---
# <a name="parsing-the-results"></a>결과 구문 분석

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 SQL Server에서 사용자가 쿼리에서 반환된 결과를 완전히 처리하는 방법을 설명합니다.

## <a name="update-counts-and-result-sets"></a>업데이트 개수 및 결과 집합

이 섹션에서는 SQL Server에서 반환되는 가장 일반적인 두 가지 결과인 Update Count 및 ResultSet에 대해 설명합니다. 일반적으로 사용자가 실행하는 모든 쿼리는 이러한 결과 중 하나를 반환합니다. 사용자는 결과를 처리할 때 둘 다 다루어야 합니다.

다음 코드는 사용자가 서버의 모든 결과를 반복하는 방법의 예입니다.
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>예외
문을 실행하여 오류 또는 정보 메시지가 발생하는 경우 SQL Server가 실행 계획을 생성할 수 있는지 여부에 따라 다르게 응답합니다. 오류 메시지는 문 실행 후 즉시 throw되거나 별도의 결과 집합이 필요할 수 있습니다. 후자의 경우 애플리케이션은 예외를 검색하기 위해 결과 집합을 구문 분석해야 합니다.

SQL Server에서 실행 계획을 생성할 수 없는 경우 예외가 즉시 throw됩니다.

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

SQL Server 결과 집합에서 오류 메시지를 반환하는 경우에는 예외를 검색하기 위해 결과 집합을 처리해야 합니다.

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

문 실행이 여러 결과 집합을 생성하는 경우에는 예외를 포함하는 결과 집합 도달할 때까지 각각을 처리해야 합니다.

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

`String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`의 경우 `execute()`에서 예외가 즉시 throw되고 `SELECT 1`은 실행되지 않습니다.

SQL Server 오류의 심각도가 `0`-`9`인 경우 해당 오류는 정보 메시지로 간주되고 `SQLWarning`으로 반환됩니다.

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)
