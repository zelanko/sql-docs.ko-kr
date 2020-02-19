---
title: Microsoft JDBC Driver for SQL Server 다운로드
description: Microsoft JDBC Driver for SQL Server를 다운로드하여 SQL Server에 연결하는 Java 애플리케이션을 개발합니다.
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc273bccf054408f48e7bb2bd0409a31bb18bd18
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "71682000"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 다운로드

이 문서에서는 Microsoft JDBC Driver for SQL Server에 대한 다운로드 링크를 제공합니다. 이 드라이버를 사용하여 SQL Server에 연결하는 Java 애플리케이션을 개발할 수 있습니다.  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>SQL Server용 JDBC Driver의 사용 가능한 다운로드

다음 표의 링크를 사용하여 JRE(Java Runtime Environment)와 일치하는 최신 Microsoft JDBC Driver for SQL Server를 다운로드할 수 있습니다.

| 버전 | 릴리스 날짜 | Java 버전 |
|---|---|---|
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 2019/8/1 | JRE 8, 11, 12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 2019/4/17 | JRE 8, 11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 2018/7/31 | JRE 8, 10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 2018/3/26 | JRE 7, 8, 9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 2018/2/12 | JRE 7, 8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 2018/2/27 | JRE 7, 8 |
| [Microsoft JDBC Driver 4.2](https://go.microsoft.com/fwlink/?linkid=841534) | 2018/2/26 | JRE 7, 8 |
| [Microsoft JDBC Driver 4.1](https://go.microsoft.com/fwlink/?linkid=841533) | 2018/2/27 | JRE 7 |

드라이버를 다운로드할 때 여러 JAR 파일이 있습니다. JAR 파일의 이름은 지원되는 Java 버전을 나타냅니다. 각 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes-for-the-jdbc-driver.md) 및 [시스템 요구 사항](system-requirements-for-the-jdbc-driver.md)을 참조하세요.

## <a name="using-the-jdbc-driver-with-maven-central"></a>Maven Central에서 JDBC 드라이버 사용

POM.xml에서 다음 코드로 JDBC 드라이버를 종속성으로 추가하여 Maven 프로젝트에 JDBC 드라이버를 추가할 수 있습니다.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>지원되지 않는 드라이버

지원되지 않는 드라이버 버전은 여기에서 다운로드할 수 없습니다. Java 연결 지원을 지속적으로 개선하고 있습니다. 따라서 최신 버전의 Microsoft JDBC 드라이버를 사용하는 것이 좋습니다.  
  
## <a name="next-steps"></a>다음 단계

Microsoft JDBC Driver for SQL Server에 대한 자세한 내용은 [JDBC 드라이버 개요](overview-of-the-jdbc-driver.md) 및 [JDBC 드라이버 GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md)를 참조하세요.
