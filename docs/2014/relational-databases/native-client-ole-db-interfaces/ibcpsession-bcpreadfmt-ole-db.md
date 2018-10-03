---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPReadFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a82cd2b9261b8f8c26e4e37636423cc27603fcc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141147"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt(OLE DB)
  서식 파일에서 각 열의 서식 정보를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPReadFmt** 메서드는 데이터 파일의 데이터 형식을 지정하는 서식 파일에서 데이터를 읽을 때 사용됩니다. 이 메서드는 서식 파일의 올바른 버전을 검색할 수 있으므로 서식 파일이 xml인지 이전 스타일의 텍스트 형식인지 자동으로 검색하여 그에 따라 동작합니다. 지 원하는 서식 파일 버전을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 BCP는 6.0 이상 버전.  
  
 **BCPReadFmt** 메서드는 형식 값을 읽은 후 [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) 및 [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) 메서드를 적절히 호출합니다. 따라서 사용자가 서식 파일의 구문을 분석하여 메서드를 호출할 필요가 없습니다.  
  
 서식 파일을 저장하려면 [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md) 메서드를 호출합니다. **BCPReadFmt** 메서드를 호출할 때 저장된 형식을 참조할 수 있습니다. 또한 대량 복사 유틸리티(**bcp**)로 사용자 정의 데이터 형식을 **BCPReadFmt** 메서드가 참조할 수 있는 파일에 저장할 수 있습니다.  
  
 `BCP_OPTION_DELAYREADFMT` 의 값을 *eOption* 의 매개 변수 [ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md) ibcpsession:: Bcpreadfmt의 동작을 수정 합니다.  
  
## <a name="arguments"></a>인수  
 *pwszFormatFile*[in]  
 데이터 파일에 대한 형식 값이 포함된 파일의 경로 및 파일 이름입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 인터페이스를 사용하세요.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) 메서드를 호출하지 않았습니다.  
  
## <a name="see-also"></a>관련 항목  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../native-client/features/performing-bulk-copy-operations.md)  
  
  
