---
title: "데이터 연결 및 검색 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 506a577f8a1623a31ccb0901b00a3376b72ef262
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-and-retrieving-data"></a>데이터 연결 및 검색
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  사용 하 여 작업할 때는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에 대 한 연결을 설정 하기 위한 두 가지 기본 방법을 사용 하는 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 연결 URL에 연결 속성을 설정 하 고 다음 반환할 DriverManager 클래스의 getConnection 메서드를 호출 하는 하나는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
> [!NOTE]  
>  JDBC 드라이버에서 지 원하는 연결 속성 목록은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 두 번째 방법은 연결 속성의 setter 메서드를 사용 하 여 설정 된 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스, 한 다음 호출에서 [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 는 SQLServerConnection을 반환 하는 메서드 개체입니다.  
  
 이 섹션의 항목에 연결할 수 있는 다양 한 방법에 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스에 있으며 기술을 보여 줍니다 서로 다른 데이터를 검색 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[연결 URL 샘플](../../connect/jdbc/connection-url-sample.md)|연결 URL에 연결 하는 데 사용 하는 방법을 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 다음 SQL 문을 사용 하 여 데이터를 검색 합니다.|  
|[데이터 원본 샘플](../../connect/jdbc/data-source-sample.md)|데이터 원본을 사용하여 SQL Server에 연결한 후 저장 프로시저를 사용하여 데이터를 검색하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [샘플 JDBC 드라이버 응용 프로그램](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

