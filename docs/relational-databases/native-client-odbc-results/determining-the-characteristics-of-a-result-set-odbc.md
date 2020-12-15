---
description: 결과 집합의 특징 확인(ODBC)
title: 결과 집합의 특징 (ODBC)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 643daf45e784e8ec3622939186ec1942d7960fac
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473534"
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>결과 집합의 특징 확인(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  메타데이터는 다른 데이터를 설명하는 데이터입니다. 예를 들어 결과 집합 메타데이터는 결과 집합에 있는 열 수, 이러한 열의 데이터 형식, 이름, 전체 자릿수, Null 허용 여부 등과 같은 결과 집합의 특징을 설명합니다.  
  
 ODBC는 카탈로그 API 함수를 통해 애플리케이션에 메타데이터를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT odbc 드라이버는 해당 카탈로그 프로시저에 대 한 호출로 많은 ODBC API 카탈로그 함수를 구현 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 애플리케이션에서는 대부분의 결과 집합 작업에 대해 메타데이터를 요구합니다. 예를 들어 애플리케이션에서는 열의 데이터 형식을 사용하여 해당 열에 바인딩할 변수의 종류를 확인하고 문자 열의 바이트 길이를 사용하여 열 데이터를 표시하는 데 필요한 공간을 확인합니다. 애플리케이션에서 열의 메타데이터를 확인하는 방법은 애플리케이션 종류에 따라 다릅니다.  
  
 일반적으로 수직 시장 애플리케이션에서는 미리 정의된 테이블을 사용하여 미리 정의된 작업을 수행합니다. 이러한 애플리케이션의 결과 집합 메타데이터는 개발자가 애플리케이션을 작성하고 제어하기 전에 정의되므로 용용 프로그램에 하드 코딩됩니다. 예를 들어 주문 ID 열이 데이터 원본에 4바이트 정수로 정의된 경우 애플리케이션에서는 항상 해당 열에 4바이트 정수를 바인딩할 수 있습니다. 메타데이터가 애플리케이션에 하드 코딩되면 애플리케이션에서 사용하는 테이블의 변경은 일반적으로 애플리케이션 코드의 변경을 암시합니다.  
  
 임시 쿼리를 지원하는 애플리케이션과 같은 일반 애플리케이션에서는 일반적으로 애플리케이션에서 만든 결과 집합의 메타데이터를 런타임 이전에 알 수 없습니다.  
  
 결과 집합의 특징을 확인하기 위해 애플리케이션에서는 다음과 같이 할 수 있습니다.  
  
-   요청에서 반환 된 열 수를 확인 하기 위한 [Sqlnumresultcols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)  
  
-   결과 집합의 열을 설명 하는 [Sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 또는 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)  
  
 잘 디자인된 애플리케이션은 결과 집합을 알 수 없고 결과 집합이 이러한 함수에서 반환하는 정보를 사용하여 해당 결과 집합의 열을 바인딩한다는 가정 하에 작성됩니다. 애플리케이션에서는 문이 준비되거나 실행된 후 언제든지 이러한 함수를 호출할 수 있습니다. 그러나 최적의 성능을 위해 응용 프로그램은 문이 실행 된 후 **Sqlcolattribute**, **SQLDescribeCol** 및 **sqlnumresultcols** 를 호출 해야 합니다.  
  
 메타데이터는 동시에 여러 번 호출할 수 있습니다. ODBC 카탈로그 API 구현을 기반으로 하는 시스템 카탈로그 프로시저는 ODBC 드라이버가 정적 서버 커서를 사용하는 동안 호출할 수 있습니다. 이렇게 하면 애플리케이션에서 ODBC 카탈로그 함수에 대한 여러 호출을 동시에 처리할 수 있습니다.  
  
 애플리케이션에서 특정 메타데이터 세트을 두 번 이상 사용하는 경우 이러한 메타데이터 세트을 처음으로 가져올 때 프라이빗 변수에 해당 정보가 캐시되는 이점을 얻을 수 있습니다. 이는 나중에 드라이버를 강제로 서버에 왕복하게 하는 ODBC 카탈로그 함수가 동일한 정보에 대해 호출되지 않도록 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;결과 처리 ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
