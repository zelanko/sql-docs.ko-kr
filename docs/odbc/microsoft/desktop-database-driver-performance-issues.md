---
title: 데스크톱 데이터베이스 드라이버 성능 문제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d92d2784649e4366113b3070b54598df585370
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240312"
---
# <a name="desktop-database-driver-performance-issues"></a>데스크톱 데이터베이스 드라이버 성능 문제
기존 ANSI 응용 프로그램과 호환성을 위해 Microsoft 액세스 4.0 또는 더 높은 데이터 원본에 대 한 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 데이터 형식 SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR로 노출 됩니다. 데이터 원본을 와이드 문자 데이터 형식을 반환 하지 않지만 데이터도 보내야 Jet 와이드 문자 형식에서입니다. 변환이 수행 됩니다 SQL_C_CHAR 매개 변수 또는 결과 열을 ANSI 응용 프로그램에서 SQL_CHAR 데이터 형식으로 바인딩된 경우를 이해 하는 것이 반드시 합니다.  
  
 이 변환은 SQL_C_CHAR 형식 LONGVARCHAR 형식의 매개 변수를 바인딩할 때 메모리 측면에서 특히 효율적 없습니다 수 있습니다. Jet 4.0 엔진을 스트리밍하려면 LONGTEXT 매개 변수 데이터 이므로 유니코드 변환 버퍼를 할당 해야 합니다 ANSI SQL_C_CHAR 버퍼의 크기 두 배입니다. 가장 효율적인 메커니즘을 SQL_C_WCHAR 형식으로 매개 변수를 바인딩하고 유니코드 변환을 수행 하도록 응용 프로그램입니다. 매개 변수가 실행 시 데이터 표시 되어 있고 데이터가 SQLPutData 여러 번 호출에 제공 됩니다, longtext 데이터 버퍼를 때 증가 합니다. 이 증가 하는 비용을 방지 하는 한 가지 방법은 "데이터 배치" 버퍼가 SQL_DATA_AT_EXEC_LEN(x) 통해 선택적 길이 제공 합니다. 여기서 *x* 예상 길이 (바이트)입니다. 이를 내부 PutData 버퍼의 크기를 초기화할 *x* 바이트입니다.  
  
> [!NOTE]  
>  긴 데이터 삽입 하거나 업데이트 하는 효율적인 방법을 사용 하 여 수행할 수 있습니다 **SQLBulkOperations()** 하거나 **SQLSetPos()** 긴 데이터 SQL_DATA_AT_EXEC로 설정 합니다. (EXEC_LEN 무시 됩니다 여기서.) 호출 하 여 데이터를 청크로 스트리밍할 수 있습니다 **SQLPutData** 여러 번은는 효과적으로 데이터 테이블에 추가 합니다.  
  
 Microsoft ODBC 데스크톱 데이터베이스 드라이버를 통해 Jet 3.5 데이터베이스를 사용 하 여 응용 프로그램 버전 4.0으로 업그레이드 되는 경우에 몇 가지 성능 저하 및 향상 된 작업 집합 크기를 발생할 수 있습니다. 왜냐하면 경우 버전 3입니다. *x* 데이터베이스를 새 버전 4.0 driver를 사용 하 여 열, Jet 4.0 로드 합니다. Jet 4.0 데이터베이스 연결을 열고 해당 데이터베이스가 3입니다. *x* 버전인 해당도 Jet 3.5 엔진을 로드 하는 설치 가능한 ISAM 드라이버를 로드 합니다. 성능 및 크기 페널티를 Jet 3을 제거 합니다. *x* Jet 4.0 형식으로 데이터베이스에 데이터베이스를 압축 해야 합니다. 두 개의 Jet 엔진을 로드 제거 되 고 데이터는 코드 경로 최소화 됩니다.  
  
 또한 Jet 4.0 엔진은 유니코드 엔진입니다. 모든 문자열이 저장 되 고 유니코드로 조작 합니다. 경우 ANSI 응용 프로그램 액세스 하는 Jet 3입니다. *x* 유니코드, ANSI 다시로 Jet 4.0 엔진은 데이터를 통해 데이터베이스에서 ANSI 변환 됩니다. 데이터베이스 버전 4.0 형식으로 업데이트 되 면 문자열을 하나의 Jet 엔진을 통해 이동 하 여 코드 경로 데이터를 최소화할 수 있을 뿐만 아니라 문자열 변환의 한 수준 제거 유니코드로 변환 됩니다.
