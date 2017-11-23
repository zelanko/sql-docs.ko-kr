---
title: "Open 메서드 (ADO 연결) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords: Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9133d8e959d1831fc1ff64ed1d8ecace96c3f882
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="open-method-ado-connection"></a>Open 메서드 (ADO 연결)
데이터 원본에 대 한 연결을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *연결 문자열*  
 (선택 사항) A **문자열** 연결 정보를 포함 하는 값입니다. 참조는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 유효한 설정에 대 한 자세한 내용은 속성입니다.  
  
 *사용자 Id*  
 (선택 사항) A **문자열** 연결을 설정할 때 사용할 사용자 이름을 포함 하는 값입니다.  
  
 *암호*  
 (선택 사항) A **문자열** 연결을 설정할 때 사용할 암호를 포함 하는 값입니다.  
  
 *옵션*  
 (선택 사항) A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) 후이 메서드를 반환할지 여부를 결정 하는 값 (동기) (비동기) 연결이 설정 되기 전에 합니다.  
  
## <a name="remarks"></a>주의  
 사용 하는 **열려** 메서드를 한 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 데이터 원본에 물리적 연결을 설정 하는 개체입니다. 이 메서드가 성공적으로 완료 된 후 연결이 라이브 및 것에 대해 명령을 실행 하 고 결과 처리할 수 있습니다.  
  
 선택적를 사용 하 여 *ConnectionString* 계열을 포함 하는 연결 문자열 중 하나를 지정 하려면 인수 *인수* *= value* 세미콜론으로 구분 하는 문 또는 URL로 식별 된 리소스 파일 또는 디렉터리입니다. **ConnectionString** 속성에 사용 되는 값을 자동으로 상속 된 *ConnectionString* 인수입니다. 설정 하거나 따라서 할 수 있습니다는 **ConnectionString** 속성은 **연결** 또는 사용을 열기 전에 개체는 *ConnectionString* 인수를 설정 하거나 재정의 하는 동안 현재 연결 매개 변수는 **열려** 메서드를 호출 합니다.  
  
 사용자 및 암호 정보 둘 다에 전달 하는 경우는 *ConnectionString* 인수와 선택 사항인 *UserID* 및 *암호* 인수는 *사용자 Id*  및 *암호* 인수에 지정 된 값을 재정의 *ConnectionString*합니다.  
  
 열려 있는 작업을 완료 한 경우 **연결**를 사용 하 여는 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 관련 시스템 리소스를 해제 하는 메서드. 개체를 닫아도 제거 되지 않고 메모리;에서 으로 설정 하 고 사용 하 여는 **열고** 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 설정 *Nothing*합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **연결** 개체는 **열려** 메서드 될 때까지 서버에 연결을 실제로 설정 되지는 않습니다는 [레코드 집합 ](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 열릴는 **연결** 개체입니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 (VBScript) 예제](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)
