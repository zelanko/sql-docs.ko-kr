---
title: 데스크톱 데이터베이스 드라이버 성능 문제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a819d99a995fd7b287beb66b94f1df526e05f201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303504"
---
# <a name="desktop-database-driver-performance-issues"></a>데스크톱 데이터베이스 드라이버 성능 문제
기존 ANSI 응용 프로그램과의 호환성을 보장하기 위해 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 데이터 형식은 Microsoft Access 4.0 이상의 데이터 원본에 대한 SQL_CHAR, SQL_VARCHAR 및 SQL_LONGVARCHAR 노출됩니다. 데이터 원본은 WIDE CHAR 데이터 형식을 반환하지 않지만 데이터는 여전히 와이드 차 형식으로 Jet로 전송되어야 합니다. SQL_C_CHAR 매개 변수 또는 결과 열이 ANSI 응용 프로그램의 SQL_CHAR 데이터 형식에 바인딩된 경우 변환이 수행된다는 점을 이해하는 것이 중요합니다.  
  
 이 변환은 SQL_C_CHAR 형식이 LONGVARCHAR 형식의 매개 변수에 바인딩될 때 메모리 측면에서 특히 비효율적일 수 있습니다. Jet 4.0 엔진은 LONGTEXT 매개 변수 데이터를 스트리밍할 수 없으므로 SQL_C_CHAR ANSI 버퍼의 두 배 크기의 유니코드 변환 버퍼를 할당해야 합니다. 가장 효율적인 메커니즘은 응용 프로그램이 UNICODE 변환을 수행하고 매개 변수를 SQL_C_WCHAR 유형으로 바인딩하는 것입니다. 매개 변수가 실행 시 데이터로 표시되고 데이터가 SQLPutData에 대한 여러 호출에서 제공되면 긴 텍스트 데이터 버퍼가 증가합니다. 이 "데이터 넣기" 버퍼를 늘리는 비용을 방지하는 한 가지 방법은 *x가* 예상 바이트 길이인 SQL_DATA_AT_EXEC_LEN(x)를 통해 선택적 길이를 제공하는 것입니다. 이렇게 하면 내부 PutData 버퍼의 크기를 *x* 바이트로 초기화합니다.  
  
> [!NOTE]  
>  긴 데이터를 삽입하거나 업데이트하는 효율적인 방법은 **SQLBulkOperations()** 또는 **SQLSetPos()를** 사용하여 긴 데이터를 SQL_DATA_AT_EXEC 위해 설정할 수 있습니다. (이 경우 EXEC_LEN 무시됩니다.) **SQLPutData를** 여러 번 호출하여 데이터를 청크로 스트리밍할 수 있으며, 이 경우 데이터가 테이블에 효과적으로 부가될 수 있습니다.  
  
 Microsoft ODBC 데스크톱 데이터베이스 드라이버를 통해 Jet 3.5 데이터베이스를 사용하는 응용 프로그램이 버전 4.0으로 업그레이드되면 일부 성능 저하 및 작업 집합 크기가 증가할 수 있습니다. 이는 버전 3이 있을 때이기 때문입니다. *x* 데이터베이스는 새 버전 4.0 드라이버를 사용하여 열리고 Jet 4.0을 로드합니다. Jet 4.0이 데이터베이스를 열고 데이터베이스가 3임을 볼 때 *x* 버전에서는 Jet 3.5 엔진을 로드하는 것과 동일한 설치 가능한 ISAM 드라이버를 로드합니다. 성능 및 크기 페널티를 제거하려면 Jet 3. *x* 데이터베이스는 Jet 4.0 형식 데이터베이스로 압축되어야 합니다. 이렇게 하면 두 개의 Jet 엔진로드가 제거되고 데이터에 대한 코드 경로가 최소화됩니다.  
  
 또한 Jet 4.0 엔진은 유니코드 엔진입니다. 모든 문자열은 유니코드에 저장되고 조작됩니다. ANSI 응용 프로그램이 Jet 3에 액세스하는 경우 *x* Jet 4.0 엔진을 통해 데이터베이스는 데이터가 ANSI에서 유니코드로 변환되고 다시 ANSI로 변환됩니다. 데이터베이스가 버전 4.0 형식으로 업데이트되면 문자열이 유니코드로 변환되어 한 수준의 문자열 변환을 제거하고 하나의 Jet 엔진만 거치면 데이터에 대한 코드 경로를 최소화합니다.
