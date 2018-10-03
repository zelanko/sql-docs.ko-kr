---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_colptr
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2bb66baa1cfefdeb857641daad0e454a1088d005
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648281"
---
# <a name="bcpcolptr"></a>bcp_colptr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  현재 복사본의 프로그램 변수 데이터 주소를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_colptr (  
        HDBC hdbc,  
        LPCBYTE pData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *pData*  
 복사할 데이터에 대한 포인터입니다. 바인딩된 데이터 형식을 큰 값 형식 (예: SQLTEXT 또는 SQLIMAGE) 이면 *pData* NULL 일 수 있습니다. NULL *pData* 긴 데이터 값 전송할 SQL Server를 사용 하 여 청크 단위로 나타냅니다 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)합니다.  
  
 하는 경우 *pData* NULL이 고 열으로 바인딩된 필드에 해당 하는 큰 값 형식인을 하지 **bcp_colptr** 실패 합니다.  
  
 큰 값 형식에 대 한 자세한 내용은 참조 하세요. [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)**합니다.**  
  
 *idxServerCol*  
 데이터 복사 대상인 데이터베이스 테이블 열의 서수 위치입니다. 테이블의 첫 번째 열은 열 1입니다. 열의 서 수 위치를 보고 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 합니다 **bcp_colptr** 함수를 사용 하면 SQL server로 데이터를 복사할 때 특정 열의 원본 데이터의 주소를 변경할 수 있습니다 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)합니다.  
  
 사용자 데이터에 대 한 포인터를 호출 하 여 처음에 설정할지 **bcp_bind**합니다. 프로그램 변수 데이터 주소가 변경 된 경우 호출 사이 **bcp_sendrow**를 호출할 수 있습니다 **bcp_colptr** 데이터에 대 한 포인터를 다시 설정 하려면. 다음에 호출할 **bcp_sendrow** 호출에 의해 주소가 지정 된 데이터를 보내는 **bcp_colptr**합니다.  
  
 별도 있어야 **bcp_colptr** 데이터 주소를 테이블의 모든 열에 대 한 호출을 수정 하려고 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
