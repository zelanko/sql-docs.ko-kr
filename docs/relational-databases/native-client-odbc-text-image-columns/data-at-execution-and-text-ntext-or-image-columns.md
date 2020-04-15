---
title: 데이터 실행 및 텍스트, ntext, 이미지
ms.custom: ''
ms.date: 03/06/2017
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
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d95478cd558239030ccfb4091641258548705ba9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297720"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>실행 시 데이터 및 text, ntext 또는 image 열
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 실행 시 데이터는 애플리케이션에서 바인딩된 열 또는 매개 변수에 있는 대량의 데이터를 사용할 수 있도록 하는 기능입니다. 매우 큰 **텍스트,** **ntext**또는 **이미지** 열을 검색할 때 응용 프로그램이 단순히 거대한 버퍼를 할당하고, 열을 버퍼에 바인딩하고, 행을 가져오지 못할 수 있습니다. 매우 큰 **텍스트,** **ntext**또는 **이미지** 열을 업데이트할 때 응용 프로그램은 단순히 거대한 버퍼를 할당하고 SQL 문의 매개 변수 마커에 바인딩한 다음 문을 실행하지 못할 수 있습니다. 이러한 경우 응용 프로그램은 실행 시 데이터 옵션을 사용하여 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 또는 [SQLPutData를](../../relational-databases/native-client-odbc-api/sqlputdata.md) 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [text 및 image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
