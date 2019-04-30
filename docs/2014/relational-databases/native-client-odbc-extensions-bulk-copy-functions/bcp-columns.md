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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcfbbdb1881662401e791ea197115120444cf855
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225535"
---
# <a name="bcpcolumns"></a>bcp_columns
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 대량 복사에 사용하기 위해 사용자 파일에서 찾는 총 열 수를 설정합니다. [bcp_setbulkmode](bcp-setbulkmode.md) bcp_columns 대신 사용할 수 있습니다 하 고 [bcp_colfmt](bcp-colfmt.md)합니다.  
  
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
 사용자 파일에 포함된 총 열 수입니다. 대량으로 사용자 파일에서 데이터 복사를 준비 하는 경우에 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 사용자 파일의 모든 열을 복사 하지도 설정 해야 합니다 *nColumns* 사용자 파일 열의 총 수입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 한 후에이 함수를 호출할 수 있습니다 [bcp_init](bcp-init.md) 가 올바른 파일 이름을 사용 하 여 호출 되었습니다.  
  
 기본값과는 다른 사용자 파일 형식을 사용하려는 경우에만 이 함수를 호출해야 합니다. 에 대 한 기본 사용자 파일 형식 설명 하는 방법에 대 한 자세한 내용은 참조 하세요. **bcp_init**합니다.  
  
 호출한 후 `bcp_columns`를 호출 해야 합니다 [bcp_colfmt](bcp-colfmt.md)완전히 사용자 지정 파일 형식을 정의 하는 사용자 파일의 각 열에 대 한 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
