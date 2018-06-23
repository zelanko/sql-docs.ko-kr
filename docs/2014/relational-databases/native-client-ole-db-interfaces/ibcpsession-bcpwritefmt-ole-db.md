---
title: 'Ibcpsession:: Bcpwritefmt (OLE DB) | Microsoft Docs'
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
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f7b2437a8a1a46b84f011eb631887d39f7c96eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082463"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt(OLE DB)
  각 열에 대한 서식 정보를 서식 파일에 기록합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 서식 파일은 대량 복사를 통해 만들어진 데이터 파일의 데이터 형식을 지정합니다. 에 대 한 호출이 [ibcpsession:: Bcpcolumns](ibcpsession-bcpcolumns-ole-db.md) 및 [ibcpsession:: Bcpcolfmt](ibcpsession-bcpcolfmt-ole-db.md) 메서드는 데이터 파일의 형식을 정의 합니다. **BCPWriteFmt** 메서드는 이 정의를 pwszFormatFile 인수에서 참조하는 파일에 저장합니다.  
  
 **BCPWriteFmt** 메서드는 서식 파일을 xml 또는 text 형식으로 저장할 수 있습니다. 사용 하 여 BCP_OPTION_XML 제어 옵션을 사용 하 여이 값이 표시 되어야 합니다는 [ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md) 메서드.  
  
 저장된 된 서식 파일을 로드 하려면 사용 하 여는 [ibcpsession:: Bcpreadfmt](ibcpsession-bcpreadfmt-ole-db.md) 메서드.  
  
## <a name="arguments"></a>인수  
 *pwszFormatFile*[in]  
 데이터 파일에 대한 형식 값이 포함된 파일의 경로 및 파일 이름입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 사용 하 여는 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 인터페이스입니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어는 [ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md) 이 메서드를 호출 하기 전에 메서드를 호출 하지 않았습니다.  
  
## <a name="see-also"></a>관련 항목  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../native-client/features/performing-bulk-copy-operations.md)  
  
  