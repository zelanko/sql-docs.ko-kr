---
title: 로그된 대. 로깅되지 않은 수정 사항 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc7fb913bef4083b045a0c1c010bdedbc43135c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297696"
---
# <a name="logged-vs-unlogged-modifications"></a>기록되는 수정 및 기록되지 않는 수정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  응용 프로그램은 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 ODBC 드라이버가 **텍스트,** **ntext**및 **이미지** 수정을 기록하지 않도록 요청할 수 있습니다. 하지만 이 옵션을 사용할 때는 주의해야 합니다. **텍스트,** **ntext**또는 **이미지** 데이터가 중요하지 않고 데이터 소유자가 더 높은 성능을 위해 데이터를 복구할 수 있는 기능을 기꺼이 사용하지 않는 경우에만 사용해야 합니다.  
  
 **텍스트,** **ntext**및 **이미지** 수정의 로깅은 TEXTPTR_LOGGING SQL_SOPT_SS_ 설정된 *특성* 매개 변수를 사용하여 [SQLSetStmtAttr을](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 호출하여 제어하고 *ValuePtr은* SQL_TL_ON 또는 SQL_TL_OFF 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [text 및 image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
