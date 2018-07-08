---
title: 테이블 반환 매개 변수 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: aace2d320b23110b286ee4f3d06124f830d3bede
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430772"
---
# <a name="table-valued-parameters-odbc"></a>테이블 반환 매개 변수(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC의 테이블 반환 매개 변수 지원을 통해 한 번의 호출로 여러 행을 서버로 보냄으로써 클라이언트 응용 프로그램에서 서버로 매개 변수가 있는 데이터를 보다 효율적으로 전송할 수 있습니다.  
  
 서버에서 테이블 반환 매개 변수에 관한 정보를 참조 하세요 [테이블 반환 매개 변수 &#40;데이터베이스 엔진&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)합니다.  
  
 ODBC에서 다음 두 가지 방법으로 테이블 반환 매개 변수를 서버로 보낼 수 있습니다.  
  
-   모든 테이블 반환 매개 변수 데이터가 메모리에 SQLExecDirect 또는 SQLExecute 라고 시 수 있습니다. 테이블 반환에 행이 여러 개 있으면 이 데이터가 배열로 저장됩니다.  
  
-   SQLExecDirect 또는 SQLExecute 호출 될 때 응용 프로그램에서 테이블 반환 매개 변수에 대해 실행 시 데이터를 지정할 수 있습니다. 이 경우 테이블 반환의 데이터 행을 일괄 처리로 제공하거나, 한 번에 하나씩 제공해 메모리 사용량을 줄일 수 있습니다.  
  
 첫 번째 옵션을 사용하면 저장 프로시저가 비즈니스 논리를 더 많이 캡슐화할 수 있습니다. 예를 들어 주문 항목이 테이블 반환 매개 변수로 전달된 경우 단일 저장 프로시저가 전체 주문 입력 트랜잭션을 캡슐화할 수 있습니다. 이 옵션은 서버로의 왕복이 한 번만 필요하기 때문에 매우 효율적입니다. 또는 다른 프로시저를 사용하여 주문 헤더와 주문 항목을 각각 별도로 처리할 수도 있습니다. 이 경우 코드가 더 많이 필요하고 클라이언트와 서버 간의 계약이 복잡해집니다.  
  
 두 번째 방법은 매우 많은 양의 데이터로 대량 작업을 수행할 때 효율적인 메커니즘을 제공합니다. 이 방법을 사용하면 응용 프로그램에서 먼저 메모리에 데이터를 모두 버퍼링하지 않고도 서버로 데이터 행을 스트리밍할 수 있습니다.  
  
 테이블 변수를 만들 때 제약 조건과 기본 키를 만들 수 있습니다. 제약 조건은 테이블의 데이터가 특정 요구 사항을 충족하는지 확인하는 데 유용합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ODBC 테이블 반환 매개 변수 사용](../../relational-databases/native-client-odbc-table-valued-parameters/uses-of-odbc-table-valued-parameters.md)  
 테이블 반환 매개 변수 및 ODBC의 기본 사용자 시나리오를 설명합니다.  
  
 [테이블 반환 매개 변수의 ODBC SQL 유형](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-sql-type-for-table-valued-parameters.md)  
 SQL_SS_TABLE 형식에 대해 설명합니다. 테이블 반환 매개 변수를 지원하는 새로운 ODBC SQL 형식입니다.  
  
 [테이블 반환 매개 변수 설명자 필드](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)  
 테이블 반환 매개 변수를 지원하는 설명자 필드에 대해 설명합니다.  
  
 [테이블 반환 매개 변수 구성 열의 설명자 필드](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 테이블 반환 매개 변수에 대한 의미를 갖는 설명자 필드에 대해 설명합니다.  
  
 [테이블 반환 매개 변수 진단 레코드 필드](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-diagnostic-record-fields.md)  
 테이블 반환 매개 변수를 지원하기 위해 진단 레코드에 추가된 두 진단 필드에 대해 설명합니다.  
  
 [테이블 반환 매개 변수에 영향을 주는 문 특성](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)  
 테이블 반환 매개 변수 열에 번호를 지정할 수 있도록 하는 새로운 설명자 헤더 필드에 대해 설명합니다.  
  
 [테이블 반환 매개 변수 및 열 값에 대한 바인딩 및 데이터 전송](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 테이블 반환 매개 변수를 서버로 전달하는 방법과 매개 변수 바인딩에 대해 설명합니다.  
  
 [준비된 문의 테이블 반환 매개 변수 메타데이터](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)  
 응용 프로그램에서 준비된 프로시저 호출의 메타데이터를 가져오는 방법을 설명합니다.  
  
 [추가 테이블 반환 매개 변수 메타데이터](../../relational-databases/native-client-odbc-table-valued-parameters/additional-table-valued-parameter-metadata.md)  
 SQLProcedureColumns, SQLTables, 및 SQLColumns를 사용 하 여 테이블 반환 매개 변수에 대 한 메타 데이터를 검색 하는 방법에 설명 합니다.  
  
 [테이블 반환 매개 변수 데이터 변환과 기타 오류 및 경고](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 테이블 반환 매개 변수 열 값에서 발생한 오류를 처리하는 방법을 설명합니다.  
  
 [버전 간 호환성](../../relational-databases/native-client-odbc-table-valued-parameters/cross-version-compatibility.md)  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]보다 이전 버전의 클라이언트나 서버에서 테이블 반환 매개 변수를 사용할 때 발생할 수 있는 충돌에 대해 설명합니다.  
  
 [ODBC 테이블 반환 매개 변수 API 요약](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-table-valued-parameter-api-summary.md)  
 테이블 반환 매개 변수를 지원하는 ODBC 함수 목록을 보여 줍니다.  
  
 [ODBC 테이블 반환 매개 변수 프로그래밍 예제](http://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
 일반적인 태스크를 수행하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [테이블 반환 매개 변수 &#40;SQL Server Native Client&#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
