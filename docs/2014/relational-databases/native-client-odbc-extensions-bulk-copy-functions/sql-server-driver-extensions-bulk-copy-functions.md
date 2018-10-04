---
title: 대량 복사 함수와 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2888f34c1e4c4103845d07e569a0dbabeb2e4caa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133983"
---
# <a name="bulk-copy-functions"></a>Bulk Copy Functions
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 대량 복사 API 확장을 사용하면 클라이언트 응용 프로그램에서 신속하게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터 행을 추가하거나 추출할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용할 경우 SQLNCLI11.LIB 및 SQLNCLI.H에서 대량 복사 함수(BCP)를 참조할 수 있습니다.  
  
 BCP API 함수 호출을 사용하는 응용 프로그램은 응용 프로그램에서 사용하는 드라이버(.dll)와 함께 제공되는 라이브러리(.lib)와 연결해야 합니다. BCP 응용 프로그램을 두 개 이상의 드라이버 라이브러리와 연결해서는 안 됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [bcp_batch](bcp-batch.md)  
  
-   [bcp_bind](bcp-bind.md)  
  
-   [bcp_colfmt](bcp-colfmt.md)  
  
-   [bcp_collen](bcp-collen.md)  
  
-   [bcp_colptr](bcp-colptr.md)  
  
-   [bcp_columns](bcp-columns.md)  
  
-   [bcp_control](bcp-control.md)  
  
-   [bcp_done](bcp-done.md)  
  
-   [bcp_exec](bcp-exec.md)  
  
-   [bcp_getcolfmt](bcp-getcolfmt.md)  
  
-   [bcp_gettypename](bcp-gettypename.md)  
  
-   [bcp_init](bcp-init.md)  
  
-   [bcp_moretext](bcp-moretext.md)  
  
-   [bcp_readfmt](bcp-readfmt.md)  
  
-   [bcp_sendrow](bcp-sendrow.md)  
  
-   [bcp_setbulkmode](bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](bcp-setcolfmt.md)  
  
-   [bcp_writefmt](bcp-writefmt.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 드라이버 확장](../../database-engine/dev-guide/sql-server-driver-extensions.md)   
 [대량 복사 작업 수행 &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
