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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931938"
---
# <a name="open-method-ado-connection"></a>Open 메서드(ADO 연결)
데이터 원본에 연결을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 (선택 사항) A **문자열** 연결 정보를 포함 하는 값입니다. 참조 된 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 유효한 설정에 대 한 세부 정보에 대 한 속성입니다.  
  
 *UserID*  
 (선택 사항) A **문자열** 연결을 설정할 때 사용할 사용자 이름을 포함 하는 값입니다.  
  
 *암호*  
 (선택 사항) A **문자열** 연결을 설정할 때 사용할 암호를 포함 하는 값입니다.  
  
 *옵션*  
 (선택 사항) A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) 후이 메서드를 반환할지 여부를 결정 하는 값 (동기적으로) 비동기적으로 연결이 설정 되기 전에 합니다.  
  
## <a name="remarks"></a>설명  
 사용 하 여는 **열려** 메서드를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 데이터 원본에 물리적 연결을 설정 합니다. 이 메서드가 성공적으로 완료 된 후 연결이 라이브 및에 대해 명령을 실행 하 고 결과 처리할 수 있습니다.  
  
 사용 하 여 선택적 *ConnectionString* 계열이 포함 된 연결 문자열을 지정 하는 인수 *인수* *= value* 세미콜론으로 구분 된 문 또는 파일 또는 디렉터리 리소스를 식별 하는 url입니다. 합니다 **ConnectionString** 속성에 사용 된 값을 자동으로 상속 합니다 *ConnectionString* 인수입니다. 설정 하거나 있습니다 따라서 합니다 **ConnectionString** 의 속성을 **연결** 사용할지를 열기 전에 개체를 *ConnectionString* 설정 하거나 재정의 하는 인수 중 현재 연결 매개 변수를 **열려** 메서드를 호출 합니다.  
  
 사용자 이름 및 암호 둘 다에서 정보를 전달 하는 경우는 *ConnectionString* 인수 및 선택적 *UserID* 및 *암호* 인수를 *UserID*  하 고 *암호* 인수에 지정 된 값을 재정의 *ConnectionString*합니다.  
  
 열려 있는 작업을 완료 있을 때 **연결**를 사용 합니다 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 관련 시스템 리소스를 해제 하는 방법입니다. 개체 닫기지 않습니다 하지 메모리에서 제거 합니다. 해당 속성 설정을 변경 하 고 사용할 수 있습니다 합니다 **엽니다** 나중에 다시 열면 하는 방법입니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 설정 합니다 *Nothing*합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **연결** 개체를 **열기** 메서드 하지 실제로 연결 될 때까지 서버에는 [레코드 집합 ](../../../ado/reference/ado-api/recordset-object-ado.md) 열려 합니다 **연결** 개체입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 예제 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)
