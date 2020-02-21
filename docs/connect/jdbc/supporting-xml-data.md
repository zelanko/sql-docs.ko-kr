---
title: XML 데이터 지원 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 799b22cfac669846c606456f1911e27353a9ba9f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027710"
---
# <a name="supporting-xml-data"></a>XML 데이터 지원
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 XML 문서와 조각을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있도록 하는 **xml** 데이터 형식을 제공합니다. **xml** 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 제공 데이터 형식이며 **int** 및 **varchar**와 같은 다른 기본 제공 형식과 비슷합니다. 다른 기본 제공 유형과 마찬가지로 **xml** 데이터 형식을 변수 유형, 매개 변수 유형, 함수 반환 유형 또는 테이블을 만들 때 열 유형으로 사용하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 및 CONVERT 함수에서 사용할 수 있습니다. JDBC 드라이버에서 **xml** 데이터 형식은 문자열, 바이트 배열, 스트림, CLOB, BLOB 또는 SQLXML 개체로 매핑될 수 있습니다. 기본 매핑은 문자열입니다.  
  
 JDBC 드라이버에서는 SQLXML 인터페이스를 소개하는 JDBC 4.0 API가 지원됩니다. SQLXML 인터페이스는 XML 데이터에 대한 상호 작용 및 조작을 수행하는 메서드를 정의합니다. **SQLXML**은 JDBC 4.0 데이터 형식이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** 데이터 형식에 매핑됩니다. 따라서 애플리케이션에서 SQLXML 데이터 형식을 사용하려면 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 애플리케이션에서 SQLXML 개체 및 해당 메서드에 액세스할 때 sqljdbc3.jar를 사용하려고 시도하면 예외가 발생합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 XML 데이터를 데이터베이스 열에 저장하기 전에 항상 해당 데이터의 유효성을 검사합니다. 애플리케이션은 **SQLXML** 데이터 형식을 사용할 수 있는데 그 이유는 JDBC 드라이버에서 이 데이터 형식을 자동으로 **xml** 데이터 형식에 매핑하기 때문입니다. **SQLXML**은 sqljdbc4.jar에서 지원됩니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 지원되는 JRE 버전 목록은 [JDBC 드라이버 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)을 참조하세요.  
  
 이 섹션의 항목에서는 SQLXML 인터페이스에 대해 설명하고, JDBC API 메서드를 사용하여 **SQLXML** 데이터 형식에 대한 프로그램을 작성하는 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SQLXML 인터페이스](../../connect/jdbc/sqlxml-interface.md)|SQLXML 인터페이스 및 해당 메서드에 대해 설명합니다.|  
|[SQLXML을 사용한 프로그래밍](../../connect/jdbc/programming-with-sqlxml.md)|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API 메서드를 사용하여 **SQLXML** Java 데이터 유형이 있는 관계형 데이터베이스에 XML 데이터를 저장하고 검색하는 방법을 설명합니다. 또한 SQLXML 개체 유형에 대한 정보 및 SQLXML 개체 사용과 관련된 중요한 지침 및 제한 사항이 포함되어 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
