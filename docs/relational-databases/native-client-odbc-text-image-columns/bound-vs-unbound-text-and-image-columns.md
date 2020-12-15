---
description: 바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열
title: Bound 및 언바운드 텍스트 및 이미지 열 | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6784e70d84927721eeab15d715221c519bdb1ae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473484"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  서버 커서를 사용할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 **sqlfetch** 가 수행 될 때 바인딩되지 않은 **text**, **ntext** 또는 **image** 열에 대 한 데이터를 전송 하지 않도록 최적화 되어 있습니다. **Text**, **ntext** 또는 **image** 데이터는 응용 프로그램이 열에 대해 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 를 발급할 때까지 서버에서 실제로 검색 되지 않습니다.  
  
 사용자가 커서에서 위나 아래로 스크롤 하는 동안 **text**, **ntext** 또는 **image** 데이터가 표시 되지 않도록 많은 응용 프로그램을 작성할 수 있습니다. 사용자가 행을 선택 하 여 세부 정보를 가져오는 경우 응용 프로그램은 **SQLGetData** 를 호출 하 여 **text**, **ntext** 또는 **image** 데이터를 검색할 수 있습니다. 이렇게 하면 사용자가 선택 하지 않은 행에 대해 **text**, **ntext** 또는 **image** 데이터가 전송 되지 않으므로 매우 많은 양의 데이터가 전송 되는 것을 방지할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [텍스트 및 이미지 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [커서 동작](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
