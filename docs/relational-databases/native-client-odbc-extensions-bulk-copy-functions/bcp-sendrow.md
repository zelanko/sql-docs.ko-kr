---
title: bcp_sendrow | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 937ea3a4086e65712f77b569976902fbd2038007
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39561913"
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
 **bcp_sendrow** 함수 프로그램 변수에서 행을 빌드하고을 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 호출 하기 전에 **bcp_sendrow**, 호출을 수행 해야 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 행 데이터를 포함 하 여 프로그램 변수를 지정할 수 있습니다.  
  
 경우 **bcp_bind** 라고 예를 들어, 긴 가변 길이 데이터 형식을 지정 하는 *eDataType* SQLTEXT 및 NULL이 아닌 매개 변수 *pData* 매개 변수, **bcp_sendrow** 는 다른 데이터 형식에 적용 되는 것 처럼 전체 데이터 값을 보냅니다. 그러나 If, **bcp_bind** 에 NULL *pData* 매개 변수를 **bcp_sendrow** 지정 된 데이터를 사용 하 여 모든 열을 보낸 후에 즉시 응용 프로그램에 제어를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 응용 프로그램이 호출할 수 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) 긴, 가변 길이 데이터를 보내려고 반복적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 한 번에 한 청크. 자세한 내용은 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 때 **bcp_sendrow** 대량 복사 행으로 프로그램 변수에서 사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 사용자가 요청할 때만 행 확정은 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) 또는 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) . 호출 하도록 선택할 수 있습니다 **bcp_batch** 일단 모든 *n* 행 또는 들어오는 데이터의 기간별 lull 한 경우. 경우 **bcp_batch** 가 호출 되지 행은 커밋된 경우 **bcp_done** 라고 합니다.  
  
 대량 복사에서 시작 하 여 중단에 대 한 내용은 변경 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]를 참조 하십시오 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
