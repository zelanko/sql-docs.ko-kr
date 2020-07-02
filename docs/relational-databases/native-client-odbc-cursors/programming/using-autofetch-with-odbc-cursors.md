---
title: ODBC 커서와 함께 자동 인출 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee4731c9666e47500620e540d1095b4ddb9214bc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760705"
---
# <a name="using-autofetch-with-odbc-cursors"></a>ODBC 커서로 자동 인출 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  인스턴스에 연결 된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버는 서버 커서 유형을 사용할 때 자동 인출 옵션을 지원 합니다. 자동 인출를 사용 하면 커서를 여는 **Sqlexecute** 또는 **sqlexecdirect** 함수에도 암시적 [sqlfetchscroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 함수가 있습니다. 문 실행의 일부로 첫 번째 행 집합을 구성하는 행이 바인딩된 애플리케이션 변수에 반환되므로 네트워크를 통해 다시 서버로 왕복할 필요가 없습니다. 자동 인출 옵션을 사용 하는 경우 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 는 지원 되지 않습니다. 결과 집합 열은 프로그램 변수에 바인딩되어야 합니다.  
  
 애플리케이션은 드라이버별 SQL_SOPT_SS_CURSOR_OPTIONS 문 특성을 SQL_CO_AF로 설정하여 자동 인출을 요청합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 프로그래밍 정보](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
