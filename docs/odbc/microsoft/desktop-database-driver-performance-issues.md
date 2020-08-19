---
description: 데스크톱 데이터베이스 드라이버 성능 문제
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20c21c493d81df6afb4a338675f86ad96ccfab68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449555"
---
# <a name="desktop-database-driver-performance-issues"></a>데스크톱 데이터베이스 드라이버 성능 문제
기존 ANSI 응용 프로그램과의 호환성을 보장 하기 위해 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 데이터 형식은 Microsoft Access 4.0 이상의 데이터 원본에 대 한 SQL_CHAR, SQL_VARCHAR 및 SQL_LONGVARCHAR으로 노출 됩니다. 데이터 원본은 와이드 문자 데이터 형식을 반환 하지 않지만 데이터는 여전히 와이드 문자 형식으로 Jet에 전송 되어야 합니다. SQL_C_CHAR 매개 변수 또는 결과 열이 ANSI 응용 프로그램의 SQL_CHAR 데이터 형식에 바인딩된 경우에는 변환이 수행 됩니다.  
  
 이 변환은 SQL_C_CHAR 형식이 비 형식 매개 변수에 바인딩된 경우 메모리 측면에서 특히 비효율적입니다. Jet 4.0 엔진은 LONGTEXT 매개 변수 데이터를 스트리밍할 수 없기 때문에 SQL_C_CHAR ANSI 버퍼 크기의 두 배에 해당 하는 유니코드 변환 버퍼를 할당 해야 합니다. 가장 효율적인 메커니즘은 응용 프로그램에서 유니코드 변환을 수행 하 고 매개 변수를 SQL_C_WCHAR 형식으로 바인딩하는 것입니다. 매개 변수가 실행 시 데이터로 표시 되 고 데이터가 SQLPutData에 대 한 여러 호출에서 제공 되는 경우 longtext 데이터 버퍼가 증가 합니다. 이러한 "데이터 배치" 버퍼의 증가를 방지 하는 한 가지 방법은 SQL_DATA_AT_EXEC_LEN (x)를 통해 선택적 길이를 제공 하는 것입니다. 여기서 *x* 는 예상 되는 바이트 길이입니다. 그러면 내부 PutData 버퍼의 크기가 *x* 바이트로 초기화 됩니다.  
  
> [!NOTE]  
>  **SQLBulkOperations ()** 또는 **SQLSetPos ()** 를 사용 하 고 긴 데이터를 SQL_DATA_AT_EXEC으로 설정 하 여 긴 데이터를 삽입 하거나 업데이트 하는 효율적인 방법을 수행할 수 있습니다. 이 경우 EXEC_LEN은 무시 됩니다. **Sqlputdata** 를 여러 번 호출 하 여 데이터를 청크로 스트리밍할 수 있습니다. 그러면 데이터를 효과적으로 테이블에 추가 합니다.  
  
 Microsoft ODBC 데스크톱 데이터베이스 드라이버를 통해 Jet 3.5 데이터베이스를 사용 하는 응용 프로그램을 버전 4.0로 업그레이드 하는 경우 성능이 저하 되 고 작업 집합 크기가 증가 하는 경우가 발생할 수 있습니다. 이는 버전 3 인 경우입니다. *x* 데이터베이스는 새 버전 4.0 드라이버를 사용 하 여 열리므로 Jet 4.0를 로드 합니다. Jet 4.0에서 데이터베이스가 열리고 데이터베이스가 3 인 것을 볼 수 있습니다. *x* 버전은 Jet 3.5 엔진을 로드 하는 것과 동일한 설치 가능한 ISAM 드라이버를 로드 합니다. 성능 및 크기 저하 (Jet 3)를 제거 합니다. *x* 데이터베이스는 Jet 4.0 형식 데이터베이스에 압축 되어야 합니다. 이렇게 하면 두 개의 Jet 엔진이 로드 되 고 데이터에 대 한 코드 경로가 최소화 됩니다.  
  
 또한 Jet 4.0 엔진은 유니코드 엔진입니다. 모든 문자열은 유니코드로 저장 되 고 조작 됩니다. ANSI 응용 프로그램이 Jet 3에 액세스 하는 경우 *x* 데이터베이스 Jet 4.0 엔진을 통해 데이터는 Ansi에서 유니코드로 변환 되 고 다시 ansi로 변환 됩니다. 데이터베이스가 버전 4.0 형식으로 업데이트 되는 경우 문자열 변환의 한 수준을 제거 하 고 하나의 Jet 엔진을 통해 데이터에 대 한 코드 경로를 최소화 하는 방식으로 문자열을 유니코드로 변환 합니다.
