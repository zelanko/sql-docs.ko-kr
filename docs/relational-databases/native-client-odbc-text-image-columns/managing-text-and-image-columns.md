---
title: Text 및 Image 열 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 300caa16e74ee36e740c901a295c1c30c1723d33
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707241"
---
# <a name="managing-text-and-image-columns"></a>text 및 image 열 관리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트**, **ntext**, 및 **이미지** (긴 데이터 라고도 함) 데이터는 문자 또는 이진 문자열 데이터 형식에 맞게 너무 커서 데이터 값을 보유할 수 있는 **char**, **varchar**, **이진**, 또는 **varbinary** 열입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트** 데이터 형식은 ODBC SQL_LONGVARCHAR 데이터 형식입니다. **ntext** SQL_WLONGVARCHAR에 및 **이미지** sql_longvarbinary에 각각 매핑됩니다. 긴 문서나 큰 비트맵과 같은 일부 데이터 항목은 너무 커서 메모리에 저장하지 못할 수 있습니다. Long 데이터를 검색할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 순차적 부분에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 응용 프로그램을 호출할 수 있도록 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)합니다. 순차적 부분에 대 한 long 데이터를 보내려고 하면 응용 프로그램이 호출할 수 [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)합니다. 실행 단계에서 데이터가 전송되는 매개 변수를 실행 시 데이터 매개 변수라고 합니다.  
  
 응용 프로그램이 실제로 쓰기 또는 모든 종류의 데이터 (긴 데이터)와 함께 검색할 **SQLPutData** 또는 **SQLGetData**유일한 하지만, **문자** 및  **이진** 데이터를 전송 하거나 부분에서 검색할 수 있습니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 없기 일반적으로 사용할 이유가 없습니다 **SQLPutData** 또는 **SQLGetData**합니다. 단일 버퍼를 매개 변수 또는 열에 바인딩하는 것이 훨씬 쉽습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [기록되는 수정 및 기록되지 않는 수정](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [실행 시 데이터 및 text, ntext 또는 image 열](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
