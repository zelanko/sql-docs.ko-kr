---
title: 데이터 원본 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b3093b87557917655fcbfd6cf7c2ec37151ca44
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027731"
---
# <a name="setting-the-data-source-properties"></a>데이터 원본 속성 설정

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

데이터 원본은 Java Platform, Enterprise Edition(Java EE) 환경에서 JDBC 연결을 생성하는 기본 메커니즘입니다. 데이터 원본은 연결 속성을 Java 코드에 하드 코딩하지 않고 연결, 풀링된 연결 및 분산 연결을 제공합니다. 모든 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 데이터 원본은 각각 적절한 setter 및 getter 메서드를 사용하여 속성 값을 설정하거나 가져올 수 있습니다.

일반적으로 애플리케이션 서버 및 servlet/JSP 엔진과 같은 Java EE 제품을 사용하여 데이터베이스 액세스를 위한 데이터 원본을 구성할 수 있습니다. 구성으로 속성을 속성=값 쌍으로 입력할 수 있는 경우 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md) 항목에 소개한 속성을 지정할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 대한 자세한 내용은 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스를 참조하세요. SQLServerDataSource 클래스를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결 하는 방법에 대 한 예제는 [데이터 원본 샘플](../../connect/jdbc/data-source-sample.md)을 참조 하세요.

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
