---
description: SQL Server 드라이버 확장 - 대량 복사 함수
title: 대량 복사 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8de90d38e540b4c4964581ef434514bc734cbdf0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866946"
---
# <a name="sql-server-driver-extensions---bulk-copy-functions"></a>SQL Server 드라이버 확장 - 대량 복사 함수
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC(Open Database Connectivity)는 애플리케이션에서 ODBC 데이터 원본의 데이터에 액세스하는 데 사용하는 Microsoft Win32 응용 프로그래밍 인터페이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 참조에는 ODBC 함수 호출이 모두 문서화되어 있지는 않습니다. 드라이버 관련 매개 변수를 가지는 함수나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 사용될 때의 동작에 대해서만 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 ODBC 3.51 사양을 준수합니다. ODBC 3.51에 대 한 포괄적인 참조는 [데이터 액세스 및 저장소 개발자 센터](https://go.microsoft.com/fwlink?linkid=4173)에서 Microsoft Data ACCESS Components SDK를 다운로드 하거나 [odbc 프로그래머 참조](../../odbc/reference/odbc-programmer-s-reference.md) 를 온라인으로 확인 하세요.  
 
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 대량 복사 API 확장을 사용하면 클라이언트 애플리케이션에서 신속하게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터 행을 추가하거나 추출할 수 있습니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용할 경우 SQLNCLI11.LIB 및 SQLNCLI.H에서 대량 복사 함수(BCP)를 참조할 수 있습니다.  
  
 BCP API 함수 호출을 사용하는 애플리케이션은 애플리케이션에서 사용하는 드라이버(.dll)와 함께 제공되는 라이브러리(.lib)와 연결해야 합니다. BCP 애플리케이션을 두 개 이상의 드라이버 라이브러리와 연결해서는 안 됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)  
  
-   [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)  
  
-   [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)  
  
-   [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)  
  
-   [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)  
  
-   [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)  
  
-   [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)  
  
-   [bcp_getcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_gettypename](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-gettypename.md)  
  
-   [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)  
  
-   [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)  
  
-   [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)  
  
-   [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
-   [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 드라이버 확장]()   
 [ODBC&#41;&#40;대량 복사 작업 수행 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
