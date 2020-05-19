---
title: 텍스트 및 이미지 열 관리 | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e6f790a82b45f9a74318a8ec46ef1e4f2a283edb
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709282"
---
# <a name="managing-text-and-image-columns"></a>text 및 image 열 관리
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**text**, **ntext**및 **image** 데이터 (long 데이터 라고도 함)는 **char**, **varchar**, **binary**또는 **varbinary** 열에 맞지 않는 데이터 값을 저장할 수 있는 문자 또는 이진 문자열 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Text** 데이터 형식은 ODBC SQL_LONGVARCHAR 데이터 형식에 매핑됩니다. **ntext** 는 SQL_WLONGVARCHAR;에 매핑됩니다. 및 **이미지가** SQL_LONGVARBINARY에 매핑됩니다. 긴 문서나 큰 비트맵과 같은 일부 데이터 항목은 너무 커서 메모리에 저장하지 못할 수 있습니다. 순차 파트에서 긴 데이터를 검색 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버를 사용 하면 응용 프로그램에서 [SQLGetData](../native-client-odbc-api/sqlgetdata.md)를 호출할 수 있습니다. 긴 데이터를 순차적인 부분으로 전송 하기 위해 응용 프로그램은 [Sqlputdata](../native-client-odbc-api/sqlputdata.md)를 호출할 수 있습니다. 실행 단계에서 데이터가 전송되는 매개 변수를 실행 시 데이터 매개 변수라고 합니다.  
  
 응용 프로그램은 **Sqlputdata** 또는 **SQLGetData**를 사용 하 여 긴 데이터 뿐만 아니라 모든 유형의 데이터를 작성 하거나 검색할 수 있지만, **문자** 및 **이진** 데이터만 파트에서 전송 하거나 검색할 수 있습니다. 그러나 데이터가 단일 버퍼에 맞게 충분히 작은 경우 일반적으로 **Sqlputdata** 또는 **SQLGetData**를 사용할 이유가 없습니다. 단일 버퍼를 매개 변수 또는 열에 바인딩하는 것이 훨씬 쉽습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [바인딩된 Text 및 Image 열과 바인딩되지 않은 Text 및 Image 열](bound-vs-unbound-text-and-image-columns.md)  
  
-   [기록되는 수정 및 기록되지 않는 수정](logged-vs-unlogged-modifications.md)  
  
-   [실행 시 데이터 및 text, ntext 또는 image 열](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
