---
title: 바인딩된 Text 및 Image 열과 Text 및 Image 열에 바인딩되지 않은 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fe1f055392698cac5554eff5a158e9dbe604a781
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128948"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  서버 커서를 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 바인딩되지 않은 대 한 데이터를 전송 하지 않도록 최적화 되어 **텍스트**를 **ntext**, 또는 **이미지** 열에는 시간 **SQLFetch** 수행 됩니다. **텍스트**, **ntext**, 또는 **이미지** 데이터는 검색 되지 않습니다 서버에서 응용 프로그램 문제까지 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 에 열입니다.  
  
 대부분의 응용 프로그램을 작성할 수 있습니다 있도록 없습니다 **텍스트**를 **ntext**, 또는 **이미지** 커서에서 사용자 위나 아래로 스크롤 하기만 하는 동안 데이터가 표시 됩니다. 사용자가 자세한 내용을 보려면 행을 선택 하면 응용 프로그램이 호출할 수 있습니다 **SQLGetData** 를 검색 하는 **텍스트**합니다 **ntext**, 또는 **이미지** 데이터입니다. 전송 하는 것이 그러면 합니다 **텍스트**를 **ntext**, 또는 **이미지** 사용자를 선택 하지 않으며 따라서 수 행에 대 한 데이터의 매우 큰 전송을 방지 데이터의 총액입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Text 및 Image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [커서 동작](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
