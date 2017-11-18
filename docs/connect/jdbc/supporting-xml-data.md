---
title: "XML 데이터 지원 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f561c72cda30a9f62e202cbd612725d02b7f408
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="supporting-xml-data"></a>XML 데이터 지원
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]제공 된 **xml** 데이터 형식 및 XML 문서를 저장할 수 있습니다에 조각의입니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. **xml** 데이터의 기본 제공 데이터 형식이 며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]와 같은 몇 가지 다른 기본 제공 유형과 비슷합니다는 **int** 및 **varchar**합니다. 다른 기본 제공 유형과 마찬가지로 사용할 수 있습니다는 **xml** 데이터 형식을으로: 변수 유형, 매개 변수 형식, 함수 반환 유형 또는 열 이거나 테이블을 만들 때 입력 [!INCLUDE[tsql](../../includes/tsql_md.md)] CAST 및 CONVERT 함수입니다. JDBC 드라이버에서는 **xml** 데이터 형식은 문자열, 바이트 배열, 스트림, CLOB, BLOB 또는 SQLXML 개체로 매핑될 수 있습니다. 기본 매핑은 문자열입니다.  
  
 JDBC 드라이버에서는 SQLXML 인터페이스를 소개하는 JDBC 4.0 API가 지원됩니다. SQLXML 인터페이스는 XML 데이터에 대한 상호 작용 및 조작을 수행하는 메서드를 정의합니다. **SQLXML** JDBC 4.0 데이터 형식이 며 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** 데이터 형식입니다. 따라서 응용 프로그램에서 SQLXML 데이터 형식을 사용하려면 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 응용 프로그램에서 SQLXML 개체 및 해당 메서드에 액세스할 때 sqljdbc3.jar를 사용하려고 시도하면 예외가 발생합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]데이터베이스 열에 저장 하기 전에 XML 데이터를 항상 확인 합니다. 응용 프로그램 צ ְ ײ **SQLXML** JDBC 드라이버에 매핑되기 때문에 데이터 형식에서 **xml** 데이터 형식이 자동으로 합니다. **SQLXML** 은 sqljdbc4.jar에서 지원 합니다. 참조 [JDBC 드라이버에 대 한 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) 에서 지 원하는 JRE 버전 목록은 여 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]합니다.  
  
 이 단원의 항목에서는 SQLXML 인터페이스는 및에 대해 프로그래밍 하는 방법에 설명 된 **SQLXML** JDBC API 메서드를 사용 하 여 데이터 형식입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SQLXML 인터페이스](../../connect/jdbc/sqlxml-interface.md)|SQLXML 인터페이스 및 해당 메서드에 대해 설명합니다.|  
|[SQLXML을 사용한 프로그래밍](../../connect/jdbc/programming-with-sqlxml.md)|사용 하는 방법에 설명 된 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 저장 하 고으로 관계형 데이터베이스에서의 XML 데이터 검색 API 메서드는 **SQLXML** Java 데이터 형식입니다. 또한 SQLXML 개체 유형에 대한 정보 및 SQLXML 개체 사용과 관련된 중요한 지침 및 제한 사항이 포함되어 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

