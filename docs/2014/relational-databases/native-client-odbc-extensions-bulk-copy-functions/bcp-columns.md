---
title: bcp_columns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f2f7cb508f9b7715abbc2505f38b30795df2d142
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081087"
---
# <a name="bcpcolumns"></a>bcp_columns
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 대량 복사에 사용하기 위해 사용자 파일에서 찾는 총 열 수를 설정합니다. [bcp_setbulkmode](bcp-setbulkmode.md) bcp_columns 대신 사용할 수 있습니다 및 [bcp_colfmt](bcp-colfmt.md)합니다.  
  
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
 사용자 파일에 포함된 총 열 수입니다. 데이터 대량 복사 하려면에서 사용자 파일을 준비 하는 경우에 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 사용자 파일의 모든 열을 복사 하지 않으려는 설정 해야 *nColumns* 사용자 파일 열의 총 수입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 후에이 함수를 호출할 수 있습니다 [bcp_init](bcp-init.md) 유효한 파일 이름으로 호출 합니다.  
  
 기본값과는 다른 사용자 파일 형식을 사용하려는 경우에만 이 함수를 호출해야 합니다. 기본 사용자 파일 형식에 대 한 설명에 대 한 자세한 내용은 참조 **bcp_init**합니다.  
  
 호출한 후 `bcp_columns`를 호출 해야 [bcp_colfmt](bcp-colfmt.md)완전히 사용자 지정 파일 형식 정의를 사용자 파일의 각 열에 대 한 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  