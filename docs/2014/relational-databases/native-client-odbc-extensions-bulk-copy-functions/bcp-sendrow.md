---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e8ef7aa7a4354f5a3fbc334504512b2ee8d131b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688836"
---
# <a name="bcpsendrow"></a>bcp_sendrow
  프로그램 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터 행을 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 합니다 **bcp_sendrow** 함수는 프로그램 변수에서 행을 작성 하 고로 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 호출 하기 전에 **bcp_sendrow**를 호출 해야 [bcp_bind](bcp-bind.md) 행 데이터를 포함 하는 프로그램 변수를 지정 합니다.  
  
 하는 경우 **bcp_bind** 예를 들어, 긴 가변 길이 데이터 형식 지정 이라고는 *eDataType* SQLTEXT 및 null이 아닌 매개 변수 *pData* 매개 변수를 **bcp_sendrow** 다른 데이터 형식에 대해서와 마찬가지로 변수와 값을 보냅니다. 그러나 If, **bcp_bind** NULL이 포함 되어 *pData* 매개 변수 **bcp_sendrow** 지정 된 데이터를 사용 하 여 모든 열을 보낸 후에 즉시 응용 프로그램에 제어를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 응용 프로그램을 호출할 수 있습니다 [bcp_moretext](bcp-moretext.md) 반복적으로 하는 긴 가변 길이 데이터를 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 한 번에 청크 합니다. 자세한 내용은 [bcp_moretext](bcp-moretext.md)합니다.  
  
 때 **bcp_sendrow** 행을 대량 복사할 프로그램 변수에서 하는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 행이 커밋됩니다 사용자를 호출 하는 경우에 [bcp_batch](bcp-batch.md) 하거나 [bcp_done](bcp-done.md) . 사용자 호출 하도록 선택할 수 있습니다 **bcp_batch** 되 면 모든 *n* 행 들어오는 데이터의 기간 사이의 소강 상태가 있는 경우 또는 합니다. 하는 경우 **bcp_batch** 가 호출 되지 행 시 커밋됩니다 **bcp_done** 라고 합니다.  
  
 대량 복사에서 시작 하 여 중단에 대 한 내용은 변경 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]를 참조 하십시오 [대량 복사 작업 수행 &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
