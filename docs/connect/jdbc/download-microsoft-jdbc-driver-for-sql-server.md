---
title: Microsoft JDBC Driver for SQL Server 다운로드
description: Microsoft JDBC Driver for SQL Server를 다운로드하여 SQL Server 및 Azure SQL Database에 연결하는 Java 애플리케이션을 개발합니다.
ms.date: 08/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d48c3f0384a805debe13472fae1841515207d160
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042446"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 다운로드

SQL Server용 Microsoft JDBC Driver는 Java 플랫폼에서 사용 가능한 표준 JDBC API(애플리케이션 인터페이스)를 통해 데이터베이스 연결을 제공하는 유형 4 JDBC 드라이버입니다. 모든 사용자는 추가 비용 없이 해당 드라이버를 다운로드하여 Java 애플리케이션, 애플리케이션 서버 또는 Java 사용 애플릿에서 SQL Server에 액세스할 수 있습니다.

## <a name="download"></a>다운로드

버전 8.4는 최신 GA(일반 공급) 버전입니다. 이 버전은 Java 8, 11 및 14를 지원합니다. 이보다 오래된 Java 런타임에서 실행해야 하는 경우, [Java 및 JDBC 사양 지원 매트릭스](microsoft-jdbc-driver-for-sql-server-support-matrix.md#java-and-jdbc-specification-support)를 참고하여 사용할 수 있는 지원되는 드라이버 버전이 있는지 확인하세요. Microsoft는 Java 연결 지원을 지속적으로 개선하고 있습니다. 따라서 최신 버전의 Microsoft JDBC 드라이버를 사용하는 것이 좋습니다.

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 8.4(zip) 다운로드](https://go.microsoft.com/fwlink/?linkid=2137600)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 8.4(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2137502)**  

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 8.4.1
- 릴리스 날짜: 2020년 8월 27일

드라이버를 다운로드할 때 여러 JAR 파일이 있습니다. JAR 파일의 이름은 지원되는 Java 버전을 나타냅니다.

> [!Note]
> 영어가 아닌 언어 버전에서 이 페이지에 액세스하고 최신 콘텐츠를 보려는 경우 [영어 버전 사이트](https://aka.ms/downloadmssqljdbcenglish)를 방문하세요. 영어 버전 사이트에서 [사용 가능한 언어](#available-languages)를 선택하여 다른 언어를 다운로드할 수 있습니다.

## <a name="available-languages"></a>사용 가능한 언어

이 SQL Server용 Microsoft JDBC Driver 릴리스는 다음 언어로 제공됩니다.

SQL Server용 Microsoft JDBC Driver 8.4.1(zip): [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40a)

SQL Server용 Microsoft JDBC Driver 8.4.1(tar.gz): [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40a)

### <a name="release-notes"></a>릴리스 정보

이 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes-for-the-jdbc-driver.md) 및 [시스템 요구 사항](system-requirements-for-the-jdbc-driver.md)을 참조하세요.

### <a name="previous-releases"></a>이전 릴리스

이전 릴리스를 다운로드하려면 [이전 SQL Server용 Microsoft JDBC Driver 릴리스](release-notes-for-the-jdbc-driver.md#previous-releases)를 참조하세요.

## <a name="using-the-jdbc-driver-with-maven-central"></a>Maven Central에서 JDBC 드라이버 사용

POM.xml에서 다음 코드로 JDBC 드라이버를 종속성으로 추가하여 Maven 프로젝트에 JDBC 드라이버를 추가할 수 있습니다.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.4.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>지원되지 않는 드라이버

지원되지 않는 드라이버 버전은 여기에서 다운로드할 수 없습니다. Java 연결 지원을 지속적으로 개선하고 있습니다. 따라서 최신 버전의 Microsoft JDBC 드라이버를 사용하는 것이 좋습니다.  
  
## <a name="next-steps"></a>다음 단계

Microsoft JDBC Driver for SQL Server에 대한 자세한 내용은 [JDBC 드라이버 개요](overview-of-the-jdbc-driver.md) 및 [JDBC 드라이버 GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md)를 참조하세요.
