---
description: 준비된 문의 테이블 반환 매개 변수 메타데이터
title: 준비 된 문에 대 한 TVP 메타 데이터
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14ef8b8111ed40ca9d1286b2648d39656ca8b58b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478034"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>준비된 문의 테이블 반환 매개 변수 메타데이터
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  응용 프로그램은 SQLNumParams 및 SQLDescribeParam을 통해 준비 된 프로시저 호출에 대 한 메타 데이터를 가져올 수 있습니다. 테이블 반환 매개 변수의 경우 *DataTypePtr* 는 SQL_SS_TABLE로 설정 됩니다. SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME 및 SQL_CA_SS_SCHEMA_NAME에 대 한 SQLGetDescField를 통해 추가 메타 데이터를 사용할 수 있습니다.  
  
 SQLColumns에서 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME 및 SQL_CA_SS_SCHEMA_NAME를 사용 하 여 테이블 반환 매개 변수와 연결 된 테이블 형식에 대 한 열 메타 데이터를 가져올 수 있습니다. 이 경우 SQLColumns를 호출 하기 전에 SQL_SOPT_SS_NAME_SCOPE을 SQL_SS_NAME_SCOPE_TABLE_TYPE로 설정 해야 합니다. 그리고 애플리케이션이 테이블 반환 매개 변수 열 메타데이터 검색을 마치면 SQL_SOPT_SS_NAME_SCOPE를 기본값인 SQL_SS_NAME_SCOPE_TABLE로 다시 설정해야 합니다.  
  
 SQL_CA_SS_TYPE_NAME , SQL_CA_SS_CATALOG_NAME 및 SQL_CA_SS_SCHEMA_NAME을 CLR 사용자 정의 형식 매개 변수에 사용할 수도 있습니다.  
  
 저장 프로시저 호출이 아닌 준비된 문의 테이블 반환 매개 변수 메타데이터는 가져올 수 없습니다. 이렇게 하려고 하면 애플리케이션에서 SQLSTATE 42000이고 메시지가 &quot;구문 오류 또는 액세스 위반입니다.&quot;인 SQL_ERROR가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
