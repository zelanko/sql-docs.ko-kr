---
title: bcp_columns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: rothja
ms.author: jroth
ms.openlocfilehash: d634f393b18124e6ae0db753def2c31860f91a74
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019643"
---
# <a name="bcp_columns"></a>bcp_columns
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 대량 복사에 사용하기 위해 사용자 파일에서 찾는 총 열 수를 설정합니다. bcp_columns 및 [bcp_colfmt](bcp-colfmt.md)대신 [bcp_setbulkmode](bcp-setbulkmode.md) 를 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *nColumns*  
 사용자 파일에 포함된 총 열 수입니다. 사용자 파일에서 테이블로 데이터를 대량 복사 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 사용자 파일의 모든 열을 복사 하지 않으려는 경우에도 *ncolumns* 를 총 사용자 파일 열 수로 설정 해야 합니다.  
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 이 함수는 올바른 파일 이름을 사용 하 여 [bcp_init](bcp-init.md) 를 호출한 후에만 호출할 수 있습니다.  
  
 기본값과는 다른 사용자 파일 형식을 사용하려는 경우에만 이 함수를 호출해야 합니다. 기본 사용자 파일 형식에 대 한 자세한 내용은 **bcp_init**를 참조 하십시오.  
  
 를 호출한 후 `bcp_columns` 사용자 파일의 각 열에 대해 [bcp_colfmt](bcp-colfmt.md)를 호출 하 여 사용자 지정 파일 형식을 완전히 정의 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
