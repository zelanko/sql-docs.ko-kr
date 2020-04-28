---
title: Open 메서드 (ADO 연결) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931938"
---
# <a name="open-method-ado-connection"></a>Open 메서드(ADO 연결)
데이터 원본에 대 한 연결을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 선택 사항입니다. 연결 정보를 포함 하는 **문자열** 값입니다. 유효한 설정에 대 한 자세한 내용은 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을 참조 하세요.  
  
 *Id*  
 선택 사항입니다. 연결을 설정할 때 사용할 사용자 이름을 포함 하는 **문자열** 값입니다.  
  
 *암호*  
 선택 사항입니다. 연결을 설정할 때 사용할 암호를 포함 하는 **문자열** 값입니다.  
  
 *옵션*  
 선택 사항입니다. 이 메서드가 연결을 설정한 후 (동기적으로) 또는 이전 (비동기적으로) 된 후에 반환 해야 하는지 여부를 결정 하는 [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) 값입니다.  
  
## <a name="remarks"></a>설명  
 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체에 대해 **Open** 메서드를 사용 하면 데이터 원본에 대 한 물리적 연결이 설정 됩니다. 이 메서드가 성공적으로 완료 되 면 연결이 라이브 되며이에 대 한 명령을 실행 하 고 결과를 처리할 수 있습니다.  
  
 선택적인 *ConnectionString* 인수를 사용 하 여 세미콜론으로 구분 된 일련의 *argument* *= value* 문을 포함 하는 연결 문자열 또는 URL로 식별 되는 파일 또는 디렉터리 리소스를 지정 합니다. **Connectionstring** 속성은 *connectionstring* 인수에 사용 되는 값을 자동으로 상속 합니다. 따라서 **연결** 개체의 **connectionstring** 속성을 열기 전에 설정 하거나 *connectionstring* 인수를 사용 하 여 **Open** 메서드 호출 중에 현재 연결 매개 변수를 설정 하거나 재정의할 수 있습니다.  
  
 *Connectionstring* 인수와 선택적 *userid* 및 *password* 인수 모두에 사용자 및 암호 정보를 전달 하면 *userid* 및 *password* 인수가 *connectionstring*에 지정 된 값을 재정의 합니다.  
  
 열린 **연결**에 대 한 작업을 완료 한 경우 [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드를 사용 하 여 연결 된 시스템 리소스를 해제 합니다. 개체를 닫으면 메모리가 제거 되지 않습니다. 속성 설정을 변경 하 고 **open** 메서드를 사용 하 여 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 *Nothing*으로 설정 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **연결** 개체에서 사용 하는 경우 **연결** 개체에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 열 때까지 **Open** 메서드는 실제로 서버에 대 한 연결을 설정 하지 않습니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 예제 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)
