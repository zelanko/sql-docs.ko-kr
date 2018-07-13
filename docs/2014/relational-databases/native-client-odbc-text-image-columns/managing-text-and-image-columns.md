---
title: Text 및 Image 열 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0989157eabe987ae8d1bdac22deb25ad2c6d028
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426992"
---
# <a name="managing-text-and-image-columns"></a>text 및 image 열 관리
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트**하십시오 **ntext**, 및 **이미지** (긴 데이터 라고도 함) 데이터는 문자 또는 이진 문자열 데이터 형식에 맞게 너무 큰 데이터 값을 보유할 수 있는 **char**하십시오 **varchar**, **이진**, 또는 **varbinary** 열입니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트** 데이터 형식은 ODBC SQL_LONGVARCHAR 데이터 형식으로 매핑됩니다 **ntext** sql_wlongvarchar 및 **이미지** sql_longvarbinary에 각각 매핑됩니다. 긴 문서나 큰 비트맵과 같은 일부 데이터 항목은 너무 커서 메모리에 저장하지 못할 수 있습니다. 긴 데이터를 검색할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 순차적 부분에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용 하면 호출 응용 프로그램 [SQLGetData](../native-client-odbc-api/sqlgetdata.md)합니다. 순차적 부분에 긴 데이터를 보내는 응용 프로그램이 호출할 수 있습니다 [SQLPutData](../native-client-odbc-api/sqlputdata.md)합니다. 실행 단계에서 데이터가 전송되는 매개 변수를 실행 시 데이터 매개 변수라고 합니다.  
  
 응용 프로그램이 실제로 쓰기 또는 모든 종류의 데이터 (시간 동안만 데이터)를 사용 하 여 검색 **SQLPutData** 또는 **SQLGetData**이지만 유일한 **문자** 고  **이진** 데이터를 전송 하거나 부분에서 검색할 수 있습니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 일반적으로 사용 하는 이유 **SQLPutData** 하거나 **SQLGetData**합니다. 단일 버퍼를 매개 변수 또는 열에 바인딩하는 것이 훨씬 쉽습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열](bound-vs-unbound-text-and-image-columns.md)  
  
-   [기록되는 수정 및 기록되지 않는 수정](logged-vs-unlogged-modifications.md)  
  
-   [실행 시 데이터 및 text, ntext 또는 image 열](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
