---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db8b433652829b16890552a70bd1e0d08d1c1bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689085"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
  열 형식 속성 값을 찾는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_getcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbvalue,  
INT*   
pcbLen  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *field*  
 속성을 검색할 열 번호입니다.  
  
 *속성*  
 속성 상수 중 하나입니다.  
  
 *pValue*  
 검색할 속성 값이 있는 버퍼에 대한 포인터입니다.  
  
 *cbValue*  
 속성 버퍼의 길이(바이트)입니다.  
  
 *pcbLen*  
 속성 버퍼에서 반환되는 데이터의 길이에 대한 포인터입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 열 형식 속성 값은 [bcp_setcolfmt](bcp-setcolfmt.md) 항목에 나와 있습니다. 열 형식 속성 값은 **bcp_setcolfmt** 함수를 호출하여 설정되고 **bcp_getcolfmt** 함수는 열 형식 속성 값을 찾는 데 사용됩니다.  
  
 이전 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전과 비교해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이상 버전의 서버 컴퓨터에 연결할 때 동작 변경 내용이 관찰될 수 있습니다. 자세한 내용은 [Metadata Discovery](../native-client/features/metadata-discovery.md)를 참조하십시오.  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_getcolfmt 지원  
 형식을 사용 합니다 `BCP_FMT_TYPE` 날짜/시간 형식에 대 한 속성에 지정 된 대로 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
