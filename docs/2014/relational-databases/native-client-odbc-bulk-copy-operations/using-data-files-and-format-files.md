---
title: 데이터 파일 및 서식 파일 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a70eed8c362411a3b1b87c66b9277da8aeac1ed4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021276"
---
# <a name="using-data-files-and-format-files"></a>데이터 파일 및 서식 파일 사용
  가장 간단한 대량 복사 프로그램은 다음을 수행합니다.  
  
1.  [Bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 를 호출 하 여 테이블 또는 뷰에서 데이터 파일로의 대량 복사 (BCP_OUT 설정)를 지정 합니다.  
  
2.  [Bcp_exec](../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 를 호출 하 여 대량 복사 작업을 실행 합니다.  
  
 데이터 파일은 기본 모드에서 만들어지기 때문에 테이블 또는 뷰에서 가져온 모든 열의 데이터는 데이터베이스에서와 동일한 형식으로 데이터 파일에 저장됩니다. 그런 후 다음과 같은 단계를 수행하고 DB_OUT 대신 DB_IN을 설정하여 파일을 서버에 대량 복사할 수 있습니다. 이 작업은 원본 테이블과 대상 테이블의 구조가 정확히 일치하는 경우에만 수행할 수 있습니다. 결과 데이터 파일은 **/n** (기본 모드) 스위치를 사용 하 여 **bcp** 유틸리티에 입력할 수도 있습니다.  
  
 테이블이나 뷰에서 직접 복사하는 대신 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 결과 집합을 대량 복사하려면  
  
1.  **Bcp_init** 를 호출 하 여 대량 복사를 지정 하지만 테이블 이름에 NULL을 지정 합니다.  
  
2.  *Eoption* 을 BCPHINTS로 설정 하 고 *ivalue* 를 transact-sql 문을 포함 하는 sqltchar 문자열에 대 한 포인터로 설정 하 여 [bcp_control](../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 를 호출 합니다.  
  
3.  **bcp_exec** 를 호출하여 대량 복사 작업을 실행합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 결과 집합을 생성하는 모든 문이 될 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 첫 번째 결과 집합이 포함된 데이터 파일이 생성됩니다. 대량 복사 시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 결과 집합이 여러 개 생성될 경우 첫 번째 결과 집합 다음의 결과 집합은 모두 무시됩니다.  
  
 열 데이터가 테이블과 다른 형식으로 저장 되는 데이터 파일을 만들려면 [bcp_columns](../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 를 호출 하 여 변경할 열 수를 지정한 다음 해당 형식을 변경할 각 열에 대해 [bcp_colfmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) 를 호출 합니다. 이 작업은 **bcp_init** 를 호출한 후 **bcp_exec**를 호출 하기 전에 수행 됩니다. **bcp_colfmt** 데이터 파일에 열 데이터가 저장 되는 형식을 지정 합니다. 대량 복사를 수행할 때 사용할 수 있습니다. **Bcp_colfmt** 를 사용 하 여 행 및 열 종결자를 설정할 수도 있습니다. 예를 들어 데이터에 탭 문자가 없는 경우 **bcp_colfmt** 를 사용 하 여 탭으로 구분 된 파일을 만들어 탭 문자를 각 열의 종결자로 설정할 수 있습니다.  
  
 **Bcp_colfmt**를 대량으로 복사 하 고 사용 하는 경우 **bcp_colfmt**를 마지막으로 호출한 후 [bcp_writefmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) 를 호출 하 여 만든 데이터 파일을 설명 하는 서식 파일을 쉽게 만들 수 있습니다.  
  
 서식 파일에서 설명 하는 데이터 파일에서 대량 복사를 수행 하는 경우 **bcp_init** 후 **bcp_exec**전에 [bcp_readfmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) 을 호출 하 여 서식 파일을 읽습니다.  
  
 **Bcp_control** 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일에서로의 대량 복사에 대 한 몇 가지 옵션을 제어 합니다. **bcp_control** 는 종료 전 최대 오류 수, 대량 복사를 시작할 파일의 행, 중지할 행 및 일괄 처리 크기와 같은 옵션을 설정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;대량 복사 작업 수행](performing-bulk-copy-operations-odbc.md)  
  
  
