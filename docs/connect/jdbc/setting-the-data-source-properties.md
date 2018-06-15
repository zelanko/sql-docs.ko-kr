---
title: 설정의 데이터 원본 속성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13a305b676d43a13ae731bcc98dd3f517a5bf733
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850388"
---
# <a name="setting-the-data-source-properties"></a>데이터 원본 속성 설정
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터 원본은 Java Platform, Enterprise Edition(Java EE) 환경에서 JDBC 연결을 생성하는 기본 메커니즘입니다. 데이터 원본은 연결 속성을 Java 코드에 하드 코딩하지 않고 연결, 풀링된 연결 및 분산 연결을 제공합니다. 모든 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 데이터 원본 설정 또는 적절 한 setter 및 getter 메서드를 각각 사용 하 여 모든 속성의 값을 가져올 수 있습니다.  
  
 일반적으로 응용 프로그램 서버 및 servlet/JSP 엔진과 같은 Java EE 제품을 사용하여 데이터베이스 액세스를 위한 데이터 원본을 구성할 수 있습니다. 에 나열 된 모든 속성은 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md) 항목 구성 속성으로 속성을 입력할 수 있습니다 아무 곳에 나 지정할 수 있습니다 = 값 쌍입니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 원본 참조는 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스입니다. 연결을 만들기 위해 SQLServerDataSource 클래스를 사용 하는 방법의 예는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 참조, 데이터베이스 [데이터 원본 샘플](../../connect/jdbc/data-source-sample.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
