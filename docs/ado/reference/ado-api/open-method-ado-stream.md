---
title: Open 메서드 (ADO 스트림) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 12d39ecbeaf22785ab20e488787e2a5350160d18
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="open-method-ado-stream"></a>Open 메서드 (ADO 스트림)
열립니다는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 이진 또는 텍스트 데이터 스트림을 조작 하는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **Variant** 값에 대 한 데이터의 원본을 지정 하는 **스트림**합니다. *소스* 전자 메일 또는 파일 시스템 등의 잘 알려진 트리 구조에서 기존 노드를 가리키는 절대 URL 문자열을 포함할 수 있습니다. URL 키워드를 사용 하 여 URL을 지정 합니다 ("URL =*구성표*://*서버*/*폴더*"). 또는 *소스* 이미 열려 있는에 대 한 참조를 포함할 수 있습니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 와 연결 된 기본 스트림을 열 수 있는 개체는 **레코드**합니다. 경우 *소스* 를 지정 하지 않으면는 **스트림** 인스턴스화할 하며 열, 기본적으로 연결 된 기본 원본에 없습니다. URL 스키마 및 관련된 공급자에 대 한 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 *모드*  
 (선택 사항) A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) 결과 대 한 액세스 모드를 지정 하는 값 **스트림** (예를 들어 읽기/쓰기 또는 읽기 전용). 기본값은 **adModeUnknown**합니다. 참조는 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 액세스 모드에 대 한 자세한 내용은 속성입니다. 경우 *모드* 를 지정 하지 않으면 소스 개체에 의해 상속 됩니다. 예를 들어 경우 소스 **레코드** 읽기 전용 모드로 열리면는 **스트림** 는 또한 기본적으로 읽기 전용 모드에서 열 수입니다.  
  
 *OpenOptions*  
 (선택 사항) A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) 값입니다. 기본값은 **adOpenStreamUnspecified**합니다.  
  
 *UserName*  
 (선택 사항) A **문자열** , 필요한 경우 액세스 하는 사용자 id를 포함 하는 값은 **스트림** 개체입니다.  
  
 *암호*  
 (선택 사항) A **문자열** , 필요한 경우 액세스 하는 암호를 포함 하는 값은 **스트림** 개체입니다.  
  
## <a name="remarks"></a>주의  
 경우는 **레코드** 개체 source 매개 변수로 전달 됩니다는 *UserID* 및 *암호* 때문에 매개 변수가 사용 되지 않는에 대 한 액세스는 **레코드** 개체는 이미 사용할 수 있습니다. 마찬가지로,는 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 의 **레코드** 으로 전송 되는 개체는 **스트림** 개체입니다. 때 *소스* 를 지정 하지 않으면는 **스트림** 열려 있으며 데이터가 포함 되지 않은 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 영 (0). 이 작성 된 모든 데이터가 손실 되지 않도록 하려면 **스트림** 때는 **스트림** 가 닫힌 경우 저장는 **스트림** 와 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 또는 [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) 메서드 또는 다른 메모리 위치에 저장 합니다.  
  
 *OpenOptions* 값 **adOpenStreamFromRecord** 의 내용을 식별 하는 *소스* 매개 변수를 이미 열려 있는 **레코드**개체입니다. 기본 동작은 처리할 *소스* 파일 등의 트리 구조에서 노드로 직접 연결 되는 URL로 합니다. 해당 노드와 연결 된 기본 스트림이 열립니다.  
  
 반면는 **스트림** 가 열려 있지 않습니다. 수는의 모든 읽기 전용 속성을 읽을 **스트림**합니다. 경우는 **스트림** 모든 후속 작업과 비동기적으로 열린 (확인 외의 다른는 [상태](../../../ado/reference/ado-api/state-property-ado.md) 및 기타 읽기 전용 속성) 될 때까지 차단 되는 **열려** 작업이 완료 되었습니다.  
  
 지정 하 여 이전에 설명한 옵션 외에도 *소스*의 인스턴스를 만들 수는 **스트림** 원본에 연결 하지 않고 메모리에 개체입니다. 이진 또는 텍스트 데이터를 작성 하 여 스트림에 데이터를 동적으로 추가할 수 있습니다는 **스트림** 와 [쓰기](../../../ado/reference/ado-api/write-method.md) 또는 [WriteText](../../../ado/reference/ado-api/writetext-method.md), 사용 된 파일에서 데이터를 로드 하거나 [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)
