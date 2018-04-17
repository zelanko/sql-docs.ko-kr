---
title: 서버 커서를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 12fdc01d3e5f906acf6d4a7bed350d315556312b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-server-cursors"></a>서버 커서 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 응용 프로그램에서 ODBC 커서 특성 중 하나는 기본값 이외의 값으로 설정 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 동일한 유형의 API 서버 커서를 구현 하는 서버를 요청 합니다. API 서버 커서가 사용되면 클라이언트의 메모리가 확보되고 클라이언트와 서버 간의 네트워크 트래픽이 줄어들 수 있습니다.  
  
 API 서버 커서의 단점은 현재 모든 SQL 문을 지원하지 않는다는 것입니다. API 서버 커서는 다음을 실행하는 데 사용할 수 없습니다.  
  
-   여러 결과 집합을 반환하는 일괄 처리 또는 저장 프로시저  
  
-   COMPUTE, COMPUTE BY, FOR BROWSE 또는 INTO 절을 포함하는 SELECT 문  
  
-   원격 저장 프로시저를 참조하는 EXECUTE 문  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결된 경우 서버 커서를 사용하는 이러한 특징이 있는 문을 실행하면 커서가 기본 결과 집합으로 변환됩니다. 그러나 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결된 경우에는 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 구현 방법](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
