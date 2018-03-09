---
title: "데스크톱 데이터베이스 드라이버 성능 문제 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67379ee540aecb691122d91b42776b0c9d990b1d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="desktop-database-driver-performance-issues"></a>데스크톱 데이터베이스 드라이버 성능 문제
기존 ANSI 응용 프로그램 호환성을 위해, Microsoft 액세스 4.0 또는 더 높은 데이터 원본에 대 한 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 데이터 형식은 SQL_CHAR, SQL_VARCHAR, 및 SQL_LONGVARCHAR로 노출 됩니다. 데이터 소스를 넓은 CHAR 데이터 형식을 반환 하지 않지만 데이터 여전히로 보내야 합니다 Jet 와이드 문자 형식으로 합니다. 변환을 수행 됩니다 SQL_C_CHAR 매개 변수 또는 결과 열 ANSI 응용 프로그램에서 SQL_CHAR 데이터 형식에 바인딩된 경우를 이해 하는 것이 유용 합니다.  
  
 이 변환은 SQL_C_CHAR 형식 LONGVARCHAR 형식의 매개 변수를 바인딩할 때 메모리 측면에서 특히 효율적 하지 수 있습니다. Jet 4.0 엔진을 스트리밍하려면 LONGTEXT 매개 변수 데이터 이므로 유니코드 변환 버퍼 할당 되어야 합니다 ANSI SQL_C_CHAR 버퍼의 크기를 두 배입니다. 가장 효율적인 방법 유니코드 변환을 수행 하거나 SQL_C_WCHAR 형식으로 매개 변수를 바인딩하여 응용 프로그램입니다. 실행 시 데이터 매개 변수 표시 되어 있고 데이터가 SQLPutData 여러 번 호출에서 제공 되 때 longtext 데이터 버퍼 증가 하는 합니다. 이 증가 하 고 관련 비용을 방지 하기 위해 한 가지 방법은 "Put 데이터" 버퍼를 제공 하는 데 SQL_DATA_AT_EXEC_LEN(x) 통해 사용자는 선택적 길이가 여기서 *x* 예상 시간은 바이트입니다. 이 내부 PutData 버퍼의 크기를 초기화할 *x* 바이트입니다.  
  
> [!NOTE]  
>  긴 데이터 삽입 하거나 업데이트 하는 효율적인 방법을 사용 하 여 수행할 수 있습니다 **SQLBulkOperations()** 또는 **SQLSetPos()** 긴 데이터 SQL_DATA_AT_EXEC로 설정 합니다. (EXEC_LEN은에 경우 무시 됩니다.) 호출 하 여 데이터를 청크로 스트리밍할 수 있습니다 **SQLPutData** 여러 번은는 효과적으로 데이터 테이블에 추가 합니다.  
  
 Microsoft ODBC 데스크톱 데이터베이스 드라이버를 통해 Jet 3.5 데이터베이스를 사용 하 여 응용 프로그램 버전 4.0으로 업그레이드 되는 경우 일부 성능 저하 및 증가 작업 집합 크기 발생할 수 있습니다. 때문에 이것이 경우 버전 3입니다. *x* 데이터베이스를 새 버전 4.0 드라이버를 사용 하 여 열, Jet 4.0을 로드 합니다. Jet 4.0 데이터베이스 연결을 열고 해당 데이터베이스가 3입니다. *x* 버전을 해당 하는 Jet 3.5 엔진을 로드 하는 설치 가능한 ISAM 드라이버 로드 합니다. 성능 및 크기 페널티를 Jet 3 제거 하려면 *x* Jet 4.0 형식 데이터베이스에 데이터베이스를 압축 해야 합니다. 두 개의 Jet 엔진을 로드 제거 되 고 코드 경로 데이터를 최소화 합니다.  
  
 또한 Jet 4.0 엔진은 유니코드 엔진입니다. 모든 문자열이 저장 되 고 유니코드에서 조작 합니다. 경우 ANSI 응용 프로그램에서는 Jet 3에 액세스 합니다. *x* 유니코드, ANSI 다시로 데이터 Jet 4.0 엔진을 통해 데이터베이스에서 ANSI 변환 됩니다. 데이터베이스 버전 4.0 형식으로 업데이트 되 면 문자열 하나만 Jet 엔진을 통해 이동 하 여 코드 경로 데이터를 최소화할 수 있을 뿐만 아니라 한 수준의 문자열 변환 제거 유니코드로 변환 됩니다.
