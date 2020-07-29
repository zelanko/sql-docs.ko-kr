---
title: 샘플 JDBC 드라이버 애플리케이션
description: SQL Server 샘플 애플리케이션용 JDBC 드라이버는 JDBC 드라이버를 사용할 때 수행할 수 있는 다양한 기능 및 좋은 프로그래밍 사례를 보여 줍니다.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17479d32cd752650b4bfb1d03f5bc36ab52d8ca4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915919"
---
# <a name="sample-jdbc-driver-applications"></a>샘플 JDBC 드라이버 애플리케이션

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션은 JDBC 드라이버의 다양한 기능을 보여줍니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 함께 JDBC 드라이버를 사용할 때 참고할 수 있는 바람직한 프로그래밍 방식도 보여줍니다.

모든 샘플 애플리케이션은 로컬 컴퓨터에서 컴파일 및 실행된 *.java 코드 파일 형식으로 포함되며 다음 위치에 있는 여러 하위 폴더에 들어 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples
```

이 섹션의 항목에서는 샘플 애플리케이션을 구성 및 실행하는 방법과 함께 샘플 애플리케이션이 소개하는 내용에 대해 설명합니다.

## <a name="in-this-section"></a>섹션 내용

| 항목                                                                            | Description                                                                                                                                                                                                                                                             |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [데이터 연결 및 검색](connecting-and-retrieving-data.md)              | 이 샘플 애플리케이션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 방법을 보여줍니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 검색하는 다양한 방법도 보여줍니다. |
| [데이터 형식 작업 &#40;JDBC&#41;](working-with-data-types-jdbc.md)        | 이 샘플 애플리케이션은 JDBC 드라이버 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터로 작업하는 방법을 보여줍니다.                                                                                           |
| [결과 집합 작업](working-with-result-sets.md)                          | 이 샘플 애플리케이션은 결과 집합을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 포함된 데이터를 처리하는 방법을 소개합니다.                                                                                                         |
| [대규모 데이터 작업](working-with-large-data.md)                            | 이러한 샘플 애플리케이션은 선택 버퍼링을 사용하여 서버 커서 오버헤드 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 큰 값 데이터를 검색하는 방법에 대해 설명합니다.                                                      |
| [SQL 데이터 검색 및 분류](data-discovery-classification-sample.md) | 이 샘플 애플리케이션은 JDBC 드라이버를 사용하여 ResultSet 개체에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 포함된 데이터 검색 및 분류 정보를 검색하는 방법을 보여 줍니다.                                         |

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](overview-of-the-jdbc-driver.md)
