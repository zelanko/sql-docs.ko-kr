---
description: 스트림 개체(ADO)
title: Stream 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 619d9d307e26829ffa74a24c6904fa84889f476f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988594"
---
# <a name="stream-object-ado"></a>스트림 개체(ADO)
이진 데이터 또는 텍스트의 스트림을 나타냅니다.  
  
 파일 시스템이 나 전자 메일 시스템과 같은 트리 구조 계층에서 [레코드](./record-object-ado.md) 에는 파일 또는 전자 메일의 내용이 포함 된 기본 이진 스트림의 비트가 연결 되어 있을 수 있습니다. **Stream** 개체는 이러한 데이터 스트림을 포함 하는 필드나 레코드를 조작 하는 데 사용할 수 있습니다. **Stream** 개체는 다음과 같은 방법으로 가져올 수 있습니다.  
  
-   이진 또는 텍스트 데이터를 포함 하는 개체 (일반적으로 파일)를 가리키는 URL입니다. 이 개체는 단순 문서, 구조화 된 문서를 나타내는 **Record** 개체 또는 폴더 일 수 있습니다.  
  
-   **Record** 개체와 연결 된 기본 **스트림** 개체를 엽니다. **레코드를** 열 때 **record** 개체와 연결 된 기본 스트림을 가져와 스트림을 열기 위한 왕복만 제거할 수 있습니다.  
  
-   **스트림** 개체를 인스턴스화합니다. 이러한 **Stream** 개체를 사용 하 여 응용 프로그램의 용도에 대 한 데이터를 저장할 수 있습니다. URL 또는 **레코드**의 기본 **스트림과** 연결 된 **스트림과** 달리 인스턴스화된 **스트림은** 기본적으로 기본 소스와 연결 되지 않습니다.  
  
 **Stream** 개체의 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Open](./open-method-ado-stream.md) 메서드를 사용 하 여 **레코드나** URL에서 **Stream** 개체를 엽니다.  
  
-   [Close](./close-method-ado.md) 메서드를 사용 하 여 **스트림을** 닫습니다.  
  
-   [Write](./write-method.md) 및 [WriteText](./writetext-method.md) 메서드를 사용 하 여 **스트림에** 바이트 또는 텍스트를 입력 합니다.  
  
-   [읽기](./read-method.md) 및 [ReadText](./readtext-method.md) 메서드를 사용 하 여 **스트림에서** 바이트를 읽습니다.  
  
-   [플러시](./flush-method-ado.md) 메서드를 사용 하 여 계속 해 서 ADO 버퍼에 있는 모든 **스트림** 데이터를 기본 개체에 씁니다.  
  
-   [CopyTo](./copyto-method-ado.md) 메서드를 사용 하 여 **스트림** 내용을 다른 **스트림으로** 복사 합니다.  
  
-   [SkipLine](./skipline-method.md)메서드 및 [LineSeparator](./lineseparator-property-ado.md) 속성을 사용 하 여 소스 파일에서 줄을 읽는 방법을 제어 합니다.  
  
-   [EOS](./eos-property.md)속성 및 [SetEOS](./seteos-method.md) 메서드를 사용 하 여 스트림 위치의 끝을 확인 합니다.  
  
-   [SaveToFile](./savetofile-method.md)및 [LoadFromFile](./loadfromfile-method-ado.md) 메서드를 사용 하 여 파일에 데이터를 저장 하 고 복원 합니다.  
  
-   [문자 집합 속성을](./charset-property-ado.md) 사용 하 여 **스트림을** 저장 하는 데 사용 되는 문자 집합을 지정 합니다.  
  
-   [Cancel](./cancel-method-ado.md) 메서드를 사용 하 여 비동기 **스트림** 작업을 중지 합니다.  
  
-   [Size](./size-property-ado-stream.md) 속성을 사용 하 여 **스트림의** 바이트 수를 확인 합니다.  
  
-   [위치](./position-property-ado.md) 속성을 사용 하 여 **스트림** 내의 현재 위치를 제어 합니다.  
  
-   [유형](./type-property-ado-stream.md) 속성을 사용 하 여 **스트림의** 데이터 유형을 결정 합니다.  
  
-   [상태](./state-property-ado.md) 속성을 사용 하 여 **스트림의** 현재 상태 (closed, open 또는 실행 중)를 확인 합니다.  
  
-   [Mode](./mode-property-ado.md) 속성을 사용 하 여 **스트림에** 대 한 액세스 모드를 지정 합니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
 **Stream** 개체는 스크립팅에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Stream 개체 속성, 메서드 및 이벤트](./stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [레코드 및 스트림](../../guide/data/records-and-streams.md)