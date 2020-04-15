---
title: 바운드 대 언바운드 텍스트 및 이미지 열 | 마이크로 소프트 문서
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
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cfa05f7019342d63ab6f3092c3b6df5ae6e8daa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297743"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  서버 커서를 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 **SQLFetch가** 수행될 때 언바운드 **텍스트,** **ntext**또는 **이미지** 열에 대한 데이터를 전송하지 않도록 최적화됩니다. 응용 프로그램이 열에 [대해 SQLGetData를](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 발행할 때까지 **텍스트,** **ntext**또는 **이미지** 데이터는 서버에서 실제로 검색되지 않습니다.  
  
 사용자가 커서에서 위아래로 스크롤하는 동안 **텍스트,** **ntext**또는 **이미지** 데이터가 표시되지 않도록 많은 응용 프로그램을 작성할 수 있습니다. 사용자가 자세한 내용을 얻기 위해 행을 선택하면 응용 프로그램은 **SQLGetData를** 호출하여 **텍스트,** **ntext**또는 **이미지** 데이터를 검색할 수 있습니다. 이렇게 하면 사용자가 선택하지 않은 행에 대한 **텍스트,** **ntext**또는 **이미지** 데이터가 전송되지 않으므로 매우 많은 양의 데이터가 전송되는 것을 방지할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [텍스트 및 이미지 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [커서 동작](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
