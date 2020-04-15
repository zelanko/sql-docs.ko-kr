---
title: SQLGetCursorName | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9d81199840f59ec7ac4b9c94b0d58c86b9eab52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302158"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  애플리케이션이 커서 이름을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 커서를 생성할 때 애플리케이션의 커서 이름을 생성합니다. 애플리케이션은 **SQLGetCursorName** 을 사용하여 위치 지정 UPDATE 및 DELETE 문에 대해 드라이버에서 정의된 커서 이름을 검색할 수 있습니다. 애플리케이션에서 위치 지정 데이터 조작 문을 이용하기 위해 **SQLSetCursorName** 을 호출할 필요는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetCursorName 함수](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
