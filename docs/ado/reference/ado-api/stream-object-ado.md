---
title: "스트림 개체 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b074a26bdd82bd4356620dbd0b12dc0b7f1c75c7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="stream-object-ado"></a>스트림 개체 (ADO)
텍스트 또는 이진 데이터 스트림을 나타냅니다.  
  
 파일 시스템 또는 전자 메일 시스템 같은 계층 구조 트리 구조에서 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 스트림이 있을 수 있습니다는 기본 이진 비트 연결 된 파일 또는 전자 메일의 내용을 포함 합니다. A **스트림** 파일이 나 이러한 스트림에 데이터를 포함 하는 레코드 개체를 사용할 수 있습니다. A **스트림** 개체는 다음과 같은이 방법으로 얻을 수 있습니다.  
  
-   이진 또는 텍스트 데이터를 포함 하는 개체 (일반적으로 파일)를 가리키는 URL입니다. 이 개체는 간단한 문서 수는 **레코드** 구조화 된 문서 또는 폴더를 나타내는 개체입니다.  
  
-   기본값을 열어 **스트림** 연관 된 개체는 **레코드** 개체입니다. 연결 된 기본 스트림을 가져올 수 있습니다는 **레코드** 개체 때는 **레코드** 라운드트립의 스트림을 열을 제거 하기 위해 열릴 합니다.  
  
-   인스턴스화하여는 **스트림** 개체입니다. 이러한 **스트림** 응용 프로그램의 목적에 대 한 데이터를 저장 하는 개체를 사용할 수 있습니다. 와 달리는 **스트림** URL 또는 기본와 관련 된 **스트림** 의 **레코드**, 인스턴스화된 **스트림** 아무런 관계가 기본적으로 기본 소스입니다.  
  
 메서드 및 속성을 사용 하 여 한 **스트림** 개체를 다음을 수행할 수 있습니다.  
  
-   열기는 **스트림** 에서 개체는 **레코드** 또는 URL로의 [열려](../../../ado/reference/ado-api/open-method-ado-stream.md) 메서드.  
  
-   닫기는 **스트림** 와 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드.  
  
-   바이트 또는 텍스트를 입력 한 **스트림** 와 [쓰기](../../../ado/reference/ado-api/write-method.md) 및 [WriteText](../../../ado/reference/ado-api/writetext-method.md) 메서드.  
  
-   바이트 읽기는 **스트림** 와 [읽기](../../../ado/reference/ado-api/read-method.md) 및 [ReadText](../../../ado/reference/ado-api/readtext-method.md) 메서드.  
  
-   모든 쓰기 **스트림** ADO에 여전히 데이터 버퍼가 너무 사용 하 여 기본 개체는 [플러시](../../../ado/reference/ado-api/flush-method-ado.md) 메서드.  
  
-   내용을 복사 하는 **스트림** 다른 **스트림** 와 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 메서드.  
  
-   인 소스 파일에서 줄을 읽는 방법 제어는 [SkipLine](../../../ado/reference/ado-api/skipline-method.md)메서드 및 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성입니다.  
  
-   스트림 위치와 끝을 확인할는 [EOS](../../../ado/reference/ado-api/eos-property.md)속성 및 [SetEOS](../../../ado/reference/ado-api/seteos-method.md) 메서드.  
  
-   저장 하 고 사용 하 여 파일에서 데이터를 복원 하는 [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)및 [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) 메서드.  
  
-   문자 집합 저장 하는 데 사용 되는 지정는 **스트림** 와 [Charset](../../../ado/reference/ado-api/charset-property-ado.md) 속성입니다.  
  
-   비동기 중단 **스트림** 사용 하 여 작업의 [취소](../../../ado/reference/ado-api/cancel-method-ado.md) 메서드.  
  
-   바이트 수를 확인 한 **스트림** 와 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 속성입니다.  
  
-   내의 현재 위치를 제어는 **스트림** 와 [위치](../../../ado/reference/ado-api/position-property-ado.md) 속성입니다.  
  
-   데이터의 형식을 결정 한 **스트림** 와 [형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 속성.  
  
-   현재 상태를 확인는 **스트림** (닫힘, 열기, 또는 실행)으로 [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성입니다.  
  
-   에 대 한 액세스 모드를 지정 된 **스트림** 와 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성입니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 **스트림** 개체는 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스트림 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)
