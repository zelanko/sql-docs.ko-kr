---
title: Stream 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 509f91b3e19b8e1215919ce89a98c6ac1c8fc74f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710759"
---
# <a name="stream-object-ado"></a>스트림 개체(ADO)
텍스트 또는 이진 데이터 스트림을 나타냅니다.  
  
 파일 시스템 또는 전자 메일 시스템 등의 계층이 트리 구조에 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 는 기본 이진 비트 스트림이 연결 된 파일 또는 전자 메일의 내용을 포함 하는 있을 수 있습니다. A **Stream** 이러한 스트림의 데이터를 포함 하는 레코드 또는 필드를 조작 하 개체를 사용할 수 있습니다. A **Stream** 다음과 같은이 방법으로 개체를 가져올 수 있습니다.  
  
-   이진 또는 텍스트 데이터를 포함 하는 개체 (일반적으로 파일)을 가리키는 URL입니다. 이 개체는 간단한 문서 수를 **레코드** 구조화 된 문서 또는 폴더를 나타내는 개체입니다.  
  
-   기본값을 열어 **Stream** 연관 된 개체를 **레코드** 개체입니다. 연결 된 기본 스트림을 가져올 수 있습니다를 **레코드** 개체 때를 **레코드** 스트림을 여는 데만 왕복을 제거 하기 위해 열려 있습니다.  
  
-   인스턴스화하여를 **Stream** 개체입니다. 이러한 **Stream** 응용 프로그램의 목적에 대 한 데이터를 저장 하는 개체를 사용할 수 있습니다. 와 달리를 **Stream** URL 또는 기본값을 사용 하 여 연결 **Stream** 의 **레코드**, 인스턴스화된 **Stream** 연관 시킬 의도가 없으며에 기본적으로 기본 소스입니다.  
  
 메서드 및 속성을 사용 하 여는 **Stream** 개체를 다음을 수행할 수 있습니다.  
  
-   열기를 **Stream** 에서 개체를 **레코드** 또는 사용 하 여 URL을 [열기](../../../ado/reference/ado-api/open-method-ado-stream.md) 메서드.  
  
-   닫기는 **Stream** 사용 하 여 합니다 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드.  
  
-   바이트 또는 텍스트를 입력 한 **Stream** 사용 하 여는 [작성](../../../ado/reference/ado-api/write-method.md) 및 [WriteText](../../../ado/reference/ado-api/writetext-method.md) 메서드.  
  
-   바이트를 읽을 합니다 **Stream** 사용 하 여를 [읽기](../../../ado/reference/ado-api/read-method.md) 하 고 [ReadText](../../../ado/reference/ado-api/readtext-method.md) 메서드.  
  
-   작성할 **Stream** ADO에 여전히 데이터가 사용 하 여 기본 개체를 버퍼링 합니다 [플러시](../../../ado/reference/ado-api/flush-method-ado.md) 메서드.  
  
-   내용을 복사 합니다는 **Stream** 간 **Stream** 사용 하 여 합니다 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 메서드.  
  
-   줄 인 소스 파일에서 읽는 방법을 제어 합니다 [SkipLine](../../../ado/reference/ado-api/skipline-method.md)메서드 및 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성입니다.  
  
-   사용 하 여 스트림 위치의 끝을 확인 합니다 [EOS](../../../ado/reference/ado-api/eos-property.md)속성 및 [SetEOS](../../../ado/reference/ado-api/seteos-method.md) 메서드.  
  
-   저장 하 고 사용 하 여 파일에서 데이터를 복원 합니다 [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)하 고 [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) 메서드.  
  
-   저장 하는 데 사용된 된 문자 집합을 지정 합니다 **Stream** 사용 하 여 합니다 [Charset](../../../ado/reference/ado-api/charset-property-ado.md) 속성입니다.  
  
-   비동기 중단 **Stream** 사용 하 여 작업을 [취소](../../../ado/reference/ado-api/cancel-method-ado.md) 메서드.  
  
-   바이트 수를 결정을 **Stream** 사용 하 여 합니다 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 속성입니다.  
  
-   내의 현재 위치를 제어를 **Stream** 사용 하 여 합니다 [위치](../../../ado/reference/ado-api/position-property-ado.md) 속성입니다.  
  
-   데이터의 형식을 결정을 **Stream** 사용 하 여 합니다 [형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 속성입니다.  
  
-   현재 상태를 확인 합니다 **Stream** (닫힌 열거나, 실행)와 [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성입니다.  
  
-   액세스 모드를 지정 합니다 **Stream** 사용 하 여 합니다 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 합니다 **Stream** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Stream 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)
