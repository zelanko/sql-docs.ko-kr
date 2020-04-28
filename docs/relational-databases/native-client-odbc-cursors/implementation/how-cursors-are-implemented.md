---
title: 커서 구현 방법 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6109930aee68ff982020b3752bd8a1af64debd55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305459"
---
# <a name="how-cursors-are-implemented"></a>커서 구현 방법
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 애플리케이션은 SQL 문을 실행하기 전에 문 특성을 하나 이상 설정하여 커서의 동작을 제어합니다. ODBC에는 커서의 특징을 지정하는 다음 두 가지 방법이 있습니다.  
  
-   커서 유형  
  
     커서 유형은 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)의 SQL_ATTR_CURSOR_TYPE 특성을 사용 하 여 설정 됩니다. ODBC 커서 유형은 정방향 전용, 정적, 키 집합, 혼합 및 동적입니다. 커서 유형 설정은 ODBC에서 커서를 지정하는 원래 방법이었습니다.  
  
-   커서 동작  
  
     커서 동작은 **SQLSetStmtAttr**의 SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY 특성을 사용 하 여 설정 됩니다. 이러한 특성은 ISO 표준에서 DECLARE CURSOR에 대해 정의된 SCROLL 및 SENSITIVE 키워드를 기반으로 모델링됩니다. 이 두 개의 ISO 옵션은 ODBC 버전 3.0에서 도입되었습니다.  
  
 ODBC 커서의 특징은 두 방법 중 하나를 사용하여 지정해야 하며, ODBC 커서 유형을 사용하는 것이 좋습니다.  
  
 커서 유형을 설정하는 것 외에도 ODBC 애플리케이션은 각 인출에서 반환된 행 수, 동시 옵션 및 트랜잭션 격리 수준과 같은 다른 옵션을 설정합니다. ODBC 스타일 커서(정방향 전용, 정적, 키 집합, 혼합 및 동적) 또는 ISO 스타일 커서(스크롤 가능 여부 및 민감도)에 대해 이러한 옵션을 설정할 수 있습니다.  
  
 Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client ODBC 드라이버는 다양 한 유형의 커서를 물리적으로 구현 하는 여러 가지 방법을 지원 합니다. 이 드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 결과 집합을 사용하여 일부 커서 유형을 구현합니다. 다른 커서는 서버 커서로 구현하거나 ODBC 커서 라이브러리를 사용하여 구현합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 기본 결과 집합 사용](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
-   [서버 커서 사용](../../../relational-databases/native-client-odbc-cursors/implementation/using-server-cursors.md)  
  
-   [ODBC 커서 라이브러리](../../../relational-databases/native-client-odbc-cursors/implementation/odbc-cursor-library.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 사용](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
