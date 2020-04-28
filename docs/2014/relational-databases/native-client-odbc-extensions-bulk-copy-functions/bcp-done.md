---
title: bcp_done | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0326330e3d2052e8e997a293f666a8fc725391b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62689072"
---
# <a name="bcp_done"></a>bcp_done
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bcp_sendrow [로 수행된 프로그램 변수에서](bcp-sendrow.md)로의 대량 복사를 끝냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
## <a name="returns"></a>반환  
 [bcp_batch](bcp-batch.md) 를 마지막으로 호출한 후 영구적으로 저장된 행의 수입니다. 오류가 발생하는 경우에는 -1입니다.  
  
## <a name="remarks"></a>설명  
 **bcp_sendrow** 또는 [bcp_moretext](bcp-sendrow.md) 를 마지막으로 호출한 후 [bcp_done](bcp-moretext.md)을 호출합니다. 모든 데이터가 복사된 후 **bcp_done** 이 호출되지 않으면 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
