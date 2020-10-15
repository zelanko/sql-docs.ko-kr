---
title: IBCPSession::BCPWriteFmt(OLE DB 드라이버) | Microsoft Docs
description: IBCPSession::BCPWriteFmt를 사용하여 xml 또는 text 형식으로 형식 파일 저장(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c088997b86fa8f0a5bd87d6497f9945c3ca2da8d
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081392"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  각 열에 대한 서식 정보를 서식 파일에 기록합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>설명  
 서식 파일은 대량 복사를 통해 만들어진 데이터 파일의 데이터 형식을 지정합니다. [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 및 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 메서드를 호출하여 데이터 파일의 형식을 정의합니다. **BCPWriteFmt** 메서드는 이 정의를 pwszFormatFile 인수에서 참조하는 파일에 저장합니다.  
  
 **BCPWriteFmt** 메서드는 서식 파일을 xml 또는 text 형식으로 저장할 수 있습니다. [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) 메서드에 BCP_OPTION_XML 제어 옵션을 사용하여 서식 파일의 형식을 나타내야 합니다.  
  
 저장된 서식 파일을 로드하려면 [IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) 메서드를 사용합니다.  
  
## <a name="arguments"></a>인수  
 *pwszFormatFile*[in]  
 데이터 파일에 대한 형식 값이 포함된 파일의 경로 및 파일 이름입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](./isqlservererrorinfo-geterrorinfo-ole-db.md) 인터페이스를 사용하세요.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 메서드를 호출하지 않았습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md) 
  
