---
title: 텍스트 및 이미지 열 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a161b009239db3c17acb64f8d8eeaaa61321cd9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63195320"
---
# <a name="managing-text-and-image-columns"></a>text 및 image 열 관리
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트**, **ntext**, 및 **이미지** (long 데이터 라고도 함) 데이터는 문자 또는 이진 문자열 데이터 형식에 맞게 너무 큰 데이터 값을 보유할 수 있는 **문자**, **varchar**, **이진**, 또는 **varbinary** 열. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트** 데이터 형식은 ODBC SQL_LONGVARCHAR 데이터 형식으로 매핑됩니다 **ntext** sql_wlongvarchar 및 **이미지** sql_longvarbinary에 각각 매핑됩니다. 긴 문서나 큰 비트맵과 같은 일부 데이터 항목은 너무 커서 메모리에 저장하지 못할 수 있습니다. 긴 데이터를 검색할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 일련의 부분에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버를 호출 하는 응용 프로그램을 사용 하면 [SQLGetData](../native-client-odbc-api/sqlgetdata.md). 응용 프로그램에서 순차적인 부분이 긴 데이터를 보내려고 호출할 수 [위해 SQLPutData](../native-client-odbc-api/sqlputdata.md). 실행 단계에서 데이터가 전송되는 매개 변수를 실행 시 데이터 매개 변수라고 합니다.  
  
 실제로 응용 프로그램 쓰거나와 함께 모든 종류의 데이터 (시간 동안만 데이터)을 검색할 수 **위해 SQLPutData** 또는 **SQLGetData**만 있지만, **문자** 및  **이진** 데이터 전송 하거나 부분에서 검색할 수 있습니다. 그러나 데이터를 단일 버퍼에 맞게 충분히 작은 경우는 일반적으로 사용 하는 이유 **위해 SQLPutData** 또는 **SQLGetData**. 단일 버퍼를 매개 변수 또는 열에 바인딩하는 것이 훨씬 쉽습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열](bound-vs-unbound-text-and-image-columns.md)  
  
-   [기록되는 수정 및 기록되지 않는 수정](logged-vs-unlogged-modifications.md)  
  
-   [실행 시 데이터 및 text, ntext 또는 image 열](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
