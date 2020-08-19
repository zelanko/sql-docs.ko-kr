---
description: Open 메서드(ADO 스트림)
title: Open 메서드 (ADO 스트림) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: baa3cb3eb5b2284a606362e31e0f185ab768c5f8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442955"
---
# <a name="open-method-ado-stream"></a>Open 메서드(ADO 스트림)
이진 또는 텍스트 데이터 스트림을 조작 하는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체를 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) **스트림에**대 한 데이터 원본을 지정 하는 **변형** 값입니다. *원본* 에는 전자 메일 또는 파일 시스템과 같이 잘 알려진 트리 구조의 기존 노드를 가리키는 절대 URL 문자열이 포함 될 수 있습니다. Url은 url 키워드 ("url =*체계*://*서버* / *폴더*")를 사용 하 여 지정 해야 합니다. 또는 *원본* 에 이미 열려 있는 [record](../../../ado/reference/ado-api/record-object-ado.md) 개체에 대 한 참조가 포함 되어 있을 수 있습니다. 그러면 **레코드**와 연결 된 기본 스트림이 열립니다. *Source* 가 지정 되지 않은 경우 기본적으로 기본 소스와 연결 된 **스트림이** 인스턴스화되고 열립니다. URL 스키마 및 연결 된 공급자에 대 한 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
 *모드*  
 (선택 사항) 결과 **스트림에** 대 한 액세스 모드를 지정 하는 [connectmodeenum](../../../ado/reference/ado-api/connectmodeenum.md) 값 (예: 읽기/쓰기 또는 읽기 전용)입니다. 기본값은 **Admodeunknown**입니다. 액세스 모드에 대 한 자세한 내용은 [Mode](../../../ado/reference/ado-api/mode-property-ado.md) 속성을 참조 하세요. *Mode* 를 지정 하지 않으면 소스 개체에 의해 상속 됩니다. 예를 들어 읽기 전용 모드에서 원본 **레코드가** 열리는 경우 **스트림은** 기본적으로 읽기 전용 모드에서 열립니다.  
  
 *OpenOptions*  
 (선택 사항) [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) 값입니다. 기본값은 **Adopenstreamunspecified 되지 않음**입니다.  
  
 *UserName*  
 (선택 사항) 필요한 경우 **스트림** 개체에 액세스 하는 사용자 id를 포함 하는 **문자열** 값입니다.  
  
 *암호*  
 (선택 사항) 필요한 경우 **스트림** 개체에 액세스 하는 암호를 포함 하는 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 **Record** 개체가 source 매개 변수로 전달 되는 경우 **record** 개체에 대 한 액세스를 이미 사용할 수 있으므로 *UserID* 및 *Password* 매개 변수는 사용 되지 않습니다. 마찬가지로 **Record** 개체의 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 는 **Stream** 개체에 전송 됩니다. *Source* 를 지정 하지 않으면 열린 **스트림에** 데이터가 없고 [크기가](../../../ado/reference/ado-api/size-property-ado-stream.md) 0입니다. **스트림이** 닫힐 때이 **스트림에** 작성 되는 데이터의 손실을 방지 하려면 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 또는 [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) 메서드를 사용 하 여 **스트림을** 저장 하거나 다른 메모리 위치에 저장 합니다.  
  
 **Adopenstreamfromrecord** 의 *Openoptions* 값은 *원본* 매개 변수의 내용을 이미 열려 있는 **Record** 개체가 되도록 식별 합니다. 기본 동작은 *소스* 를 파일 등의 트리 구조에서 노드를 직접 가리키는 URL로 처리 하는 것입니다. 해당 노드와 연결 된 기본 스트림이 열립니다.  
  
 **스트림이** 열려 있지 않은 동안에는 **스트림의**모든 읽기 전용 속성을 읽을 수 있습니다. **스트림이** 비동기적으로 열리면 **열기** 작업이 완료 될 때까지 모든 후속 작업 ( [상태](../../../ado/reference/ado-api/state-property-ado.md) 및 기타 읽기 전용 속성 확인 외)이 차단 됩니다.  
  
 *소스*를 지정 하지 않고 앞에서 설명한 옵션 외에도, 기본 소스와 연결 하지 않고 메모리에 **스트림** 개체의 인스턴스를 만들 수 있습니다. [쓰기](../../../ado/reference/ado-api/write-method.md) 또는 [WriteText](../../../ado/reference/ado-api/writetext-method.md)를 사용 하 여 **스트림에** 이진 또는 텍스트 데이터를 기록 하거나 [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)를 사용 하 여 파일에서 데이터를 로드 하 여 스트림에 데이터를 동적으로 추가할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)
