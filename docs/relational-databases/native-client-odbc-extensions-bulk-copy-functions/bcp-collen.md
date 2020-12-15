---
description: bcp_collen
title: bcp_collen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_collen
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_collen function
ms.assetid: faaf1f7a-81f2-4852-a178-56602c33673a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba02f03b831f2bdae6c6f4e86c59647598a741ce
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473644"
---
# <a name="bcp_collen"></a>bcp_collen
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 대량 복사에 대한 프로그램 변수의 데이터 길이를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_collen (  
        HDBC hdbc,  
        DBINT cbData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *cbData*  
 길이 표시기나 종결자의 길이를 제외한 프로그램 변수의 데이터 길이입니다. *Cbdata* 를 SQL_NULL_DATA로 설정 하면 서버에 복사 된 모든 행에는 열에 대 한 NULL 값이 포함 됩니다. SQL_VARLEN_DATA로 설정하면 복사되는 데이터의 길이를 확인하는 데 문자열 종결자 또는 다른 메서드가 사용됩니다. 길이 표시기와 종결자가 모두 있으면 시스템에서는 복사되는 데이터 크기가 더 작은 것이 사용됩니다.  
  
 *idxServerCol*  
 데이터가 복사되는 대상 테이블 열의 서수 위치입니다. 첫 번째 열은 1입니다. 열의 서수 위치는 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)를 사용하여 확인할 수 있습니다.  
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 **Bcp_collen** 함수를 사용 하면 bcp_sendrow를 사용 하 여 데이터를에 복사할 때 특정 열에 대해 프로그램 변수의 데이터 길이를 변경할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)  
  
 처음에는 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 를 호출할 때 데이터 길이가 결정 됩니다. **Bcp_sendrow** 호출 사이에 데이터 길이가 변경 되 고 길이 접두사나 종결자가 사용 되지 않는 경우 **bcp_collen** 를 호출 하 여 길이를 다시 설정할 수 있습니다. **Bcp_sendrow** 에 대 한 다음 호출에서는 **bcp_collen** 에 대 한 호출로 설정 된 길이를 사용 합니다.  
  
 데이터 길이가 수정 하려는 테이블의 각 열에 대해 **bcp_collen** 를 한 번씩 호출 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
