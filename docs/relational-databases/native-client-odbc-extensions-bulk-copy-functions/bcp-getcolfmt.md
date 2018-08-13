---
title: bcp_getcolfmt | Microsoft Docs
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
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 202713a323e5f257740a2457fccd4e69b7ee8e51
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562967"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  열 형식 속성 값을 찾는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *field*  
 속성을 검색할 열 번호입니다.  
  
 *property*  
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
 에 나열 된 열 형식 속성 값을 [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) 항목입니다. 열 형식 속성 값은 **bcp_setcolfmt** 함수를 호출하여 설정되고 **bcp_getcolfmt** 함수는 열 형식 속성 값을 찾는 데 사용됩니다.  
  
 에 연결할 때 동작 변경 내용이 관찰 될 수 있습니다는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (또는 이상) 서버 컴퓨터에서 이전에 비해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전입니다. 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_getcolfmt 지원  
 형식을 사용 합니다 **BCP_FMT_TYPE** 날짜/시간 형식에 대 한 속성에 지정 된 대로 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
