---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: rothja
ms.author: jroth
ms.openlocfilehash: 90170f586fb51794697308b09e46dbe5ff3a65f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019651"
---
# <a name="bcp_colptr"></a>bcp_colptr
  현재 복사본의 프로그램 변수 데이터 주소를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *pData*  
 복사할 데이터에 대한 포인터입니다. 바인딩된 데이터 형식이 대량 값 형식 (예: SQLTEXT 또는 SQLIMAGE) 인 경우 *.pdata* 는 NULL 일 수 있습니다. NULL *.pdata* 는 long 데이터 값이 [bcp_moretext](bcp-moretext.md)를 사용 하 여 SQL Server 청크로 전송 됨을 나타냅니다.  
  
 *.Pdata* 가 NULL로 설정 되어 있고 바인딩된 필드에 해당 하는 열이 크기가 크지 않은 경우 **bcp_colptr** 실패 합니다.  
  
 대량 값 형식에 대 한 자세한 내용은 [bcp_bind](bcp-bind.md)를 참조**하세요.**  
  
 *idxServerCol*  
 데이터 복사 대상인 데이터베이스 테이블 열의 서수 위치입니다. 테이블의 첫 번째 열은 열 1입니다. 열의 서수 위치는 [SQLColumns](../native-client-odbc-api/sqlcolumns.md)를 사용하여 확인할 수 있습니다.  
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 **Bcp_colptr** 함수를 사용 하면 [bcp_sendrow](bcp-sendrow.md)로 SQL Server 데이터를 복사할 때 특정 열의 원본 데이터 주소를 변경할 수 있습니다.  
  
 처음에는 사용자 데이터에 대 한 포인터가 **bcp_bind**를 호출 하 여 설정 됩니다. 프로그램 변수 데이터 주소가 **bcp_sendrow**호출 사이에서 변경 되는 경우 **bcp_colptr** 를 호출 하 여 포인터를 데이터에 다시 설정할 수 있습니다. **Bcp_sendrow** 에 대 한 다음 호출에서는 **bcp_colptr**호출로 주소가 지정 된 데이터를 보냅니다.  
  
 데이터 주소를 수정 하려는 테이블의 모든 열에 대해 별도의 **bcp_colptr** 호출이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
