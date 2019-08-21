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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027857"
---
# <a name="parsing-the-results"></a>결과 구문 분석

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 사용자가 모든 쿼리에서 반환 된 결과를 완전 하 게 처리 하는 방법을 SQL Server 설명 합니다.

## <a name="update-counts-and-result-sets"></a>업데이트 개수 및 결과 집합

이 섹션에서는 SQL Server에서 반환 되는 가장 일반적인 두 가지 결과 (Update Count 및 ResultSet)에 대해 설명 합니다. 일반적으로 사용자가 실행 하는 모든 쿼리는 이러한 결과 중 하나를 반환 합니다. 사용자는 결과를 처리할 때 모두 처리 해야 합니다.

다음 코드는 사용자가 서버의 모든 결과를 반복 하는 방법의 예입니다.
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
오류가 발생 하거나 정보 메시지를 발생 시키는 문을 실행 하면 SQL Server 실행 계획을 생성할 수 있는지 여부에 따라 다르게 응답 합니다. 오류 메시지는 문 실행 후 즉시 throw 되거나 별도의 결과 집합이 필요할 수 있습니다. 후자의 경우 응용 프로그램은 예외를 검색 하기 위해 결과 집합을 구문 분석 해야 합니다.

SQL Server에서 실행 계획을 생성할 수 없는 경우 예외가 즉시 throw 됩니다.

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

SQL Server 결과 집합에서 오류 메시지를 반환 하는 경우에는 예외를 검색 하기 위해 결과 집합을 처리 해야 합니다.

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

문 실행이 여러 결과 집합을 생성 하는 경우에는 예외를 포함 하는 하나에 도달할 때까지 각 결과 집합을 처리 해야 합니다.

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

의 `String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`경우 예외는에 `execute()` 즉시 throw 되 고 `SELECT 1` 전혀 실행 되지 않습니다.

SQL Server의 오류가의 `0` `9`심각도 인 경우 정보 메시지로 간주 되 고로 `SQLWarning`반환 됩니다.

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)
