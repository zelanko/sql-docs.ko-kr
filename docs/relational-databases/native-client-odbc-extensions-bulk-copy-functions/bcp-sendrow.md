---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5898c55baa1cb3447c97fd42e8435217c3a11325
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666281"
---
# <a name="bcpsendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  프로그램 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터 행을 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 합니다 **bcp_sendrow** 함수는 프로그램 변수에서 행을 작성 하 고로 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 호출 하기 전에 **bcp_sendrow**를 호출 해야 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 행 데이터를 포함 하는 프로그램 변수를 지정 합니다.  
  
 하는 경우 **bcp_bind** 예를 들어, 긴 가변 길이 데이터 형식 지정 이라고는 *eDataType* SQLTEXT 및 NULL이 아닌 매개 변수 *pData* 매개 변수를 **bcp_sendrow** 다른 데이터 형식에 대해서와 마찬가지로 전체 데이터 값을 보냅니다. 그러나 If, **bcp_bind** NULL이 포함 되어 *pData* 매개 변수 **bcp_sendrow** 지정 된 데이터를 사용 하 여 모든 열을 보낸 후에 즉시 응용 프로그램에 제어를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 응용 프로그램을 호출할 수 있습니다 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) 반복적으로 하는 긴 가변 길이 데이터를 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 한 번에 청크 합니다. 자세한 내용은 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)합니다.  
  
 때 **bcp_sendrow** 행을 대량 복사할 프로그램 변수에서 하는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 행이 커밋됩니다 사용자를 호출 하는 경우에 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) 하거나 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) . 사용자 호출 하도록 선택할 수 있습니다 **bcp_batch** 되 면 모든 *n* 행 들어오는 데이터의 기간 사이의 소강 상태가 있는 경우 또는 합니다. 하는 경우 **bcp_batch** 가 호출 되지 행 시 커밋됩니다 **bcp_done** 라고 합니다.  
  
 대량 복사에서 시작 하 여 중단에 대 한 내용은 변경 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]를 참조 하십시오 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
