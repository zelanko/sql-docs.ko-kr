---
title: 'IBCPSession:: BCPReadFmt (OLE DB) | Microsoft Docs'
description: '서식 파일에서 데이터를 읽는 데 IBCPSession:: BCPReadFmt 사용 (OLE DB)'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 97274315275f11e77c458827740f44906a524ed9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015503"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  서식 파일에서 각 열의 서식 정보를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPReadFmt** 메서드는 데이터 파일의 데이터 형식을 지정하는 서식 파일에서 데이터를 읽을 때 사용됩니다. 이 메서드는 서식 파일의 올바른 버전을 검색할 수 있으므로 서식 파일이 xml인지 이전 스타일의 텍스트 형식인지 자동으로 검색하여 그에 따라 동작합니다. SQL Server BCP에 대 한 OLE DB 드라이버에서 지 원하는 형식 파일 버전은 버전 6.0 이상입니다.  
  
 **BCPReadFmt** 메서드는 형식 값을 읽은 후 [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 및 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 메서드를 적절히 호출합니다. 따라서 사용자가 서식 파일의 구문을 분석하여 메서드를 호출할 필요가 없습니다.  
  
 서식 파일을 저장하려면 [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) 메서드를 호출합니다. **BCPReadFmt** 메서드를 호출할 때 저장된 형식을 참조할 수 있습니다. 또한 대량 복사 유틸리티(**bcp**)로 사용자 정의 데이터 형식을 **BCPReadFmt** 메서드가 참조할 수 있는 파일에 저장할 수 있습니다.  
  
 [IBCPSession:: BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) 의 *eoption* 매개 변수에 대 한 **BCP_OPTION_DELAYREADFMT** 값은 IBCPSession:: bcpreadfmt의 동작을 수정 합니다.  
  
## <a name="arguments"></a>인수  
 *pwszFormatFile*[in]  
 데이터 파일에 대한 형식 값이 포함된 파일의 경로 및 파일 이름입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스를 사용하세요.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 메서드를 호출하지 않았습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
