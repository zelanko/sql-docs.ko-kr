---
description: 서버 커서 사용
title: 서버 커서 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6585a9ac0805ec3b730b66bbba8b3694c34133a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438634"
---
# <a name="using-server-cursors"></a>서버 커서 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Odbc 응용 프로그램에서 ODBC 커서 특성을 기본값 이외의 값으로 설정 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 동일한 유형의 API 서버 커서를 구현 하도록 서버에 요청 합니다. API 서버 커서가 사용되면 클라이언트의 메모리가 확보되고 클라이언트와 서버 간의 네트워크 트래픽이 줄어들 수 있습니다.  
  
 API 서버 커서의 단점은 현재 모든 SQL 문을 지원하지 않는다는 것입니다. API 서버 커서는 다음을 실행하는 데 사용할 수 없습니다.  
  
-   여러 결과 집합을 반환하는 일괄 처리 또는 저장 프로시저  
  
-   COMPUTE, COMPUTE BY, FOR BROWSE 또는 INTO 절을 포함하는 SELECT 문  
  
-   원격 저장 프로시저를 참조하는 EXECUTE 문  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결된 경우 서버 커서를 사용하는 이러한 특징이 있는 문을 실행하면 커서가 기본 결과 집합으로 변환됩니다. 그러나 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결된 경우에는 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 구현 방법](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
