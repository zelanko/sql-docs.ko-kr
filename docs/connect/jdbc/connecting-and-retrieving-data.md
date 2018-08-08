---
title: 데이터 연결 및 검색 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6171d4f25efff9f3a09da21bf0ffafefb66cee4
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453137"
---
# <a name="connecting-and-retrieving-data"></a>데이터 연결 및 검색

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하는 경우 두 가지 기본 방법을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스에 연결을 설정할 수 있습니다. 그 중 하나가 연결 URL에 연결 속성을 설정한 다음 DriverManager 클래스의 getConnection 메서드를 호출하여 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 반환하는 것입니다.  
  
> [!NOTE]  
> JDBC 드라이버에서 지 원하는 연결 속성 목록은 참조 하세요 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
두 번째 방법은 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스의 setter 메서드를 사용하여 연결 속성을 설정한 다음 [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 메서드를 호출하여 SQLServerConnection 개체를 반환하는 것입니다.  
  
이 섹션의 항목에서는 이와 같이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스에 연결할 수 있는 서로 다른 방법을 설명하고, 데이터 검색에 대한 기술 차이를 보여 줍니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
| 항목                                                                | 설명                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [연결 URL 샘플](../../connect/jdbc/connection-url-sample.md) | 연결 URL을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에 연결한 후 SQL 문을 사용하여 데이터를 검색하는 방법을 설명합니다. |
| [데이터 원본 샘플](../../connect/jdbc/data-source-sample.md)       | 데이터 원본을 사용하여 SQL Server에 연결한 후 저장 프로시저를 사용하여 데이터를 검색하는 방법을 설명합니다.                                                 |
  
## <a name="see-also"></a>참고 항목

[샘플 JDBC 드라이버 응용 프로그램](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  