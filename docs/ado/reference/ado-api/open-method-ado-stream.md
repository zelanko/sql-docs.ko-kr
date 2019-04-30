---
title: Open 메서드 (ADO Stream) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0df165514a10bc667c8bd2cc6d2a8569faa79d11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239712"
---
# <a name="open-method-ado-stream"></a>Open 메서드(ADO 스트림)
열립니다는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 이진 또는 텍스트 데이터의 스트림을 조작 하는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **Variant** 에 대 한 데이터의 원본을 지정 하는 값을 **Stream**합니다. *원본* 전자 메일 또는 파일 시스템과 같은 잘 알려진 트리 구조에서 기존 노드를 가리키는 절대 URL 문자열을 포함 될 수 있습니다. URL 키워드를 사용 하 여 URL을 지정할 수 ("URL =*구성표*://*server*/*폴더*"). 또는 *소스* 는 이미 열려에 대 한 참조를 포함할 수 있습니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체와 연결 된 기본 스트림을 엽니다 합니다 **레코드**합니다. 경우 *소스* 지정 하지 않으면를 **Stream** 인스턴스화할 하며 열, 기본적으로 기본 소스를 사용 하 여 연결 합니다. URL 체계 및 연결된 공급자에 대 한 자세한 내용은 참조 하세요. [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 *모드*  
 (선택 사항) A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) 결과 대 한 액세스 모드를 지정 하는 값 **Stream** (예를 들어, 읽기/쓰기 또는 읽기 전용). 기본값은 **adModeUnknown**합니다. 참조 된 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 액세스 모드에 대 한 자세한 정보에 대 한 속성입니다. 하는 경우 *모드* 지정 하지 않으면 소스 개체에 의해 상속 됩니다. 예를 들어 경우 원본 **레코드** 읽기 전용 모드에서 열리는 합니다 **Stream** 는 또한 기본적으로 읽기 전용 모드로 열 수입니다.  
  
 *OpenOptions*  
 (선택 사항) A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) 값입니다. 기본값은 **adOpenStreamUnspecified**합니다.  
  
 *UserName*  
 (선택 사항) A **문자열** 코드는 필요한 경우에 액세스 하는 사용자 id를 포함 하는 값을 **Stream** 개체입니다.  
  
 *암호*  
 (선택 사항) A **문자열** 코드는 필요한 경우에 액세스 하는 암호를 포함 하는 값을 **Stream** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 경우는 **레코드** 개체가 원본 매개 변수로 전달 됩니다 합니다 *UserID* 및 *암호* 때문에 매개 변수가 사용 되지 않습니다에 대 한 액세스는 **레코드** 개체를 이미 사용할 수 있습니다. 마찬가지로 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 의 **레코드** 개체에 전송 되는 **Stream** 개체입니다. 때 *원본* 지정 하지 않으면는 **Stream** 열려 있고 데이터가 포함 되지 않은 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 영 (0). 이 작성 된 데이터를 손실 하지 않으려면 **Stream** 때를 **Stream** 는 닫힌 저장 합니다 **Stream** 사용 하 여는 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 또는 [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) 메서드 또는 다른 메모리 위치에 저장 합니다.  
  
 *OpenOptions* 의 값 **adOpenStreamFromRecord** 내용의 하 게 식별 하는 *원본* 매개 변수는 이미 열려 있어야 **레코드**개체입니다. 기본 동작을 처리 하는 것 *원본* 파일과 같은 트리 구조에서 노드로 직접 가리키는 url입니다. 해당 노드와 연결 된 기본 스트림이 열려 있습니다.  
  
 하는 동안 합니다 **Stream** 가 열려 있지 않은 것의 모든 읽기 전용 속성을 읽을 수는 **Stream**합니다. 경우는 **Stream** 모든 후속 작업이 비동기적으로 열린 (확인 외의 다른 합니다 [상태](../../../ado/reference/ado-api/state-property-ado.md) 및 기타 읽기 전용 속성) 때까지 차단 됩니다는 **열기** 작업이 완료 되었습니다.  
  
 지정 하지 않는 하 여 이전에 설명한 옵션 외에도 *원본*의 인스턴스를 만들 수 있습니다는 **Stream** 원본에 연결 하지 않고 메모리에서 개체. 이진 또는 텍스트 데이터를 작성 하 여 스트림으로 데이터를 동적으로 추가할 수 있습니다는 **Stream** 사용 하 여 [작성](../../../ado/reference/ado-api/write-method.md) 또는 [WriteText](../../../ado/reference/ado-api/writetext-method.md)를 사용 하 여 파일에서 데이터를 로드 하거나 [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)
