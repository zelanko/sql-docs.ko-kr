---
title: 데이터 파일과 서식 파일을 사용 하 여 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4c377bbfbe4170b5631ba1ac9c017af1176b279
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831401"
---
# <a name="using-data-files-and-format-files"></a>데이터 파일 및 서식 파일 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  가장 간단한 대량 복사 프로그램은 다음을 수행합니다.  
  
1.  호출 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 지정 하려면 데이터 파일을 보거나 테이블에서 대량 복사 (BCP_OUT 설정).  
  
2.  호출 [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 대량 복사 작업을 실행 합니다.  
  
 데이터 파일은 기본 모드에서 만들어지기 때문에 테이블 또는 뷰에서 가져온 모든 열의 데이터는 데이터베이스에서와 동일한 형식으로 데이터 파일에 저장됩니다. 그런 후 다음과 같은 단계를 수행하고 DB_OUT 대신 DB_IN을 설정하여 파일을 서버에 대량 복사할 수 있습니다. 이 작업은 원본 테이블과 대상 테이블의 구조가 정확히 일치하는 경우에만 수행할 수 있습니다. 결과 데이터 파일을 입력할 수도 있습니다는 **bcp** 사용 하 여 유틸리티를 **/n** (기본 모드) 스위치.  
  
 테이블이나 뷰에서 직접 복사하는 대신 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 결과 집합을 대량 복사하려면  
  
1.  호출 **bcp_init** 대량 복사를 지정 하려면 테이블 이름에 NULL을 지정 합니다.  
  
2.  호출 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 사용 하 여 *eOption* BCPHINTS로 설정 하 고 *iValue* TRANSACT-SQL 문이 포함 된 SQLTCHAR 문자열에 대 한 포인터를 설정 합니다.  
  
3.  호출 **bcp_exec** 대량 복사 작업을 실행 합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 결과 집합을 생성하는 모든 문이 될 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 첫 번째 결과 집합이 포함된 데이터 파일이 생성됩니다. 대량 복사 시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 결과 집합이 여러 개 생성될 경우 첫 번째 결과 집합 다음의 결과 집합은 모두 무시됩니다.  
  
 열에서 데이터는 테이블의 다른 형식으로 보다 저장 된 데이터 파일을 만들려면 호출 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 개수 열은 변경 되도록 호출 [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) 각 열에 대 한 형식의 변경 하려고 합니다. 호출 후 이렇게 **bcp_init** 호출 하기 전에 **bcp_exec**합니다. **bcp_colfmt** 데이터 파일에 저장 되는 열의 데이터 형식을 지정 합니다. 대량 복사하거나 대량 복사해 올 때 사용될 수 있습니다. 사용할 수도 있습니다 **bcp_colfmt** 행 및 열 종결자를 설정 합니다. 예를 들어 데이터에 탭 문자가 없는 경우 만들어야 탭으로 구분 된 파일을 사용 하 여 **bcp_colfmt** 각 열의 종결자로 탭 문자를 설정 합니다.  
  
 때 대량 복사할를 사용 하 여 **bcp_colfmt**를 호출 하 여 만든 데이터 파일을 설명 하는 서식 파일을 쉽게 만들 수 있습니다 [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) 에 대 한 마지막 호출 후 **bcp_colfmt**.  
  
 대량 복사 서식 파일에 설명 된 데이터 파일에서 호출 하 여 서식 파일을 읽는 [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) 한 후 **bcp_init** 하기 전에 **bcp_exec**합니다.  
  
 합니다 **bcp_control** 로 대량 복사해올 경우에 몇 가지 옵션을 제어 하는 함수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일에서 합니다. **bcp_control** 종료 하기 전에 오류, 대량 복사, 행 및 일괄 처리 크기를 시작 하는 파일에서 행의 최대 수와 같은 옵션을 설정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
