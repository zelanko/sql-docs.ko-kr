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
author: rothja
ms.author: jroth
ms.openlocfilehash: c45e87fdd8e00e9456718c4c9c8160c22bac03a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019378"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
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
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 **Bcp_sendrow** 함수는 프로그램 변수에서 행을 빌드하고로 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Bcp_sendrow**를 호출 하기 전에 [bcp_bind](bcp-bind.md) 를 호출 하 여 행 데이터가 포함 된 프로그램 변수를 지정 해야 합니다.  
  
 Long, 가변 길이 데이터 형식 (예: SQLTEXT의 *Edatatype* 매개 변수 및 Null이 아닌 *.pdata* 매개 변수)을 지정 하 여 **bcp_bind** 를 호출 하는 경우 **bcp_sendrow** 는 다른 데이터 형식에 대해 수행 되는 것과 같은 방법으로 데이터 값을 보냅니다. 그러나 **bcp_bind** 에 NULL *.pdata* 매개 변수가 있는 경우에는 지정 된 데이터가 있는 모든 열이로 전송 되는 즉시 응용 프로그램에 제어를 반환 **bcp_sendrow** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 그런 다음 응용 프로그램은 [bcp_moretext](bcp-moretext.md) 를 반복적으로 호출 하 여 긴 가변 길이 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 번에 청크로 보낼 수 있습니다. 자세한 내용은 [bcp_moretext](bcp-moretext.md)를 참조 하세요.  
  
 **Bcp_sendrow** 를 사용 하 여 프로그램 변수에서 테이블로 행을 대량 복사 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 [bcp_batch](bcp-batch.md) 또는 [bcp_done](bcp-done.md)를 호출 하는 경우에만 행이 커밋됩니다. 사용자는 *n 개* 행 마다 또는 들어오는 데이터 기간 사이에 소강 상태가이 있는 경우 **bcp_batch** 를 호출 하도록 선택할 수 있습니다. **Bcp_batch** 를 호출 하지 않으면 **bcp_done** 를 호출할 때 행이 커밋됩니다.  
  
 에서 시작 하는 대량 복사의 주요 변경 내용에 대 한 자세한 내용은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [ODBC&#41;&#40;대량 복사 작업 수행 ](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
