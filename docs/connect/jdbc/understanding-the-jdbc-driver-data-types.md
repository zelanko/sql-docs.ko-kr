---
title: JDBC 드라이버 데이터 형식 이해 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 399037b5f888c767edf28c40c0658d31e8703ddc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982168"
---
# <a name="understanding-the-jdbc-driver-data-types"></a>JDBC 드라이버 데이터 형식 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 데이터베이스로 사용하는 Java 응용 프로그램 내의 JDBC 기본 및 고급 데이터 형식 사용을 지원합니다.  
  
 JDBC 유형 시스템은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식과 Java 언어 형식 및 개체 사이의 변환을 중재합니다. JDBC 형식은 SQL-92 및 SQL-99 형식을 기준으로 합니다. JDBC 드라이버는 JDBC 사양에 따르며 예측 가능성과 융통성 사이의 올바른 균형을 제공하도록 디자인되었습니다.  
  
 이 섹션의 항목에서는 기본 및 고급 데이터 형식을 사용하는 방법 및 데이터 형식을 다른 데이터 형식으로 변환하는 방법을 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[기본 데이터 형식 사용](../../connect/jdbc/using-basic-data-types.md)|JDBC 기본 데이터 형식을 설명합니다. 결과 집합, 매개 변수가 있는 쿼리 및 저장 프로시저로 데이터 형식을 사용하는 방법에 대한 예가 포함되어 있습니다.|  
|[java.sql.Time 값을 서버에 보내는 방식 구성](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)|JDBC 드라이버에서 날짜를 생성하는 방식을 설명합니다.|  
|[고급 데이터 형식 사용](../../connect/jdbc/using-advanced-data-types.md)|JDBC 고급 데이터 형식을 설명합니다.|  
|[데이터 형식 차이 이해](../../connect/jdbc/understanding-data-type-differences.md)|다양한 JDBC 드라이버 데이터 형식 간의 차이점을 설명합니다.|  
|[데이터 형식 변환 이해](../../connect/jdbc/understanding-data-type-conversions.md)|getter 및 setter 메서드를 사용할 경우 데이터 형식 변환이 처리되는 방법에 대해 설명합니다.|  
|[국가별 문자 집합 지원](../../connect/jdbc/national-character-set-support.md)|국가별 문자 집합 형식 지원에 대해 설명합니다.|  
|[XML 데이터 지원](../../connect/jdbc/supporting-xml-data.md)|SQLXML 인터페이스에 대해 설명합니다. **SQLXML** Java 데이터 형식으로 관계형 데이터베이스에 XML 데이터를 읽고 쓰는 방법에 대해서도 설명합니다.|  
|[래퍼 및 인터페이스](../../connect/jdbc/wrappers-and-interfaces.md)|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 관련 메서드와 상수가 있는 인터페이스에 대해 설명합니다. 응용 프로그램 서버는 이 인터페이스를 사용하여 클래스의 프록시를 만들 수 있습니다. 또한 java.sql.Wrapper 인터페이스에 대한 지원에 대해서도 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
