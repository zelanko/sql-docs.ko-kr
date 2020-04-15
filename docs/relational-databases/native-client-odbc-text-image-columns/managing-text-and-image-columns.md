---
title: 텍스트 및 이미지 열 관리 | 마이크로 소프트 문서
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
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3ac58e59f66dd107a9523a42f5647c90b4fb737
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297723"
---
# <a name="managing-text-and-image-columns"></a>text 및 image 열 관리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**텍스트**, **ntext**및 **이미지** 데이터(긴 데이터라고도 함)는 **char,** **varchar,** **이진**또는 varbinary 열에 맞지 않는 데이터 값을 너무 크게 보유할 수 있는 문자 또는 **이진** 문자열 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트** 데이터 형식은 ODBC SQL_LONGVARCHAR 데이터 형식에 매핑됩니다. **SQL_WLONGVARCHAR ntext** 지도; 이미지 **image** 맵을 SQL_LONGVARBINARY 수 있습니다. 긴 문서나 큰 비트맵과 같은 일부 데이터 항목은 너무 커서 메모리에 저장하지 못할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 순차적 부분에서 긴 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검색하려면 네이티브 클라이언트 ODBC 드라이버를 사용하여 응용 프로그램에서 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)를 호출할 수 있습니다. 순차적 부분으로 긴 데이터를 보내려면 응용 프로그램에서 [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)를 호출할 수 있습니다. 실행 단계에서 데이터가 전송되는 매개 변수를 실행 시 데이터 매개 변수라고 합니다.  
  
 응용 프로그램은 **실제로** 쓰기 또는 쓰기 또는 쓰기 또는 모든 유형의 데이터 (뿐만 아니라 긴 데이터) **SQLPutData** 또는 **SQLGetData,** 문자 및 **이진** 데이터 만 전송 하거나 부분적으로 검색할 수 있지만. 그러나 데이터가 단일 버퍼에 들어갈 만큼 작으면 일반적으로 **SQLPutData** 또는 **SQLGetData**를 사용할 이유가 없습니다. 단일 버퍼를 매개 변수 또는 열에 바인딩하는 것이 훨씬 쉽습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [기록되는 수정 및 기록되지 않는 수정](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [실행 시 데이터 및 text, ntext 또는 image 열](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
