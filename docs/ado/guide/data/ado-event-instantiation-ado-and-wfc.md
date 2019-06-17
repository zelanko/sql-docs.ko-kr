---
title: 'ADO 이벤트 인스턴스: ADO 및 WFC | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1a4bb76e9172458c26e59dc366e8a321a548f34e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702610"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 이벤트 인스턴스: ADO 및 WFC
ADO에 대 한 Windows Foundation Class (ADO/WFC) ADO 이벤트 모델 기반 및 간소화 된 응용 프로그램 프로그래밍 인터페이스를 제공 합니다. 일반적으로 ADO/WFC ADO 이벤트를 가로채는 단일 이벤트 클래스에 이벤트 매개 변수를 통합 및 다음 이벤트 처리기를 호출 합니다.  
  
### <a name="to-use-ado-events-in-adowfc"></a>이벤트 사용 하 여 ADO에서 ADO/WFC  
  
1.  이벤트를 처리할 이벤트 처리기를 정의 합니다. 예를 들어 처리 하려는 경우는 **ConnectComplete** 이벤트에는 **ConnectionEvent** 제품군에 사용할 수 있습니다이 코드:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  이벤트 처리기를 나타내는 처리기 개체를 정의 합니다. 처리기 개체 데이터 형식 이어야 **ConnectEventHandler** 형식의 이벤트에 대 한 **ConnectionEvent**, 또는 데이터 형식 **RecordsetEventHandler** 형식의이벤트에대한 **RecordsetEvent**합니다. 예를 들어 다음 코드에 **ConnectComplete** 이벤트 처리기:  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     첫 번째 인수는 **ConnectionEventHandler** 생성자는 두 번째 인수에서 명명 된 이벤트 처리기를 포함 하는 클래스에 대 한 참조입니다.  
  
3.  특정 유형의 이벤트를 처리 하도록 지정 된 처리기의 목록에 이벤트 처리기를 추가 합니다. 와 같은 이름을 가진 메서드를 사용 **addOn** *EventName*(*처리기*).  
  
4.  ADO/WFC 내부적으로 모든 ADO 이벤트 처리기를 구현합니다. 이벤트에 의해 발생할 따라서를 **연결** 또는 **레코드 집합** 작업 ADO/WFC 이벤트 처리기에 의해 차단 됩니다.  
  
     ADO/WFC 이벤트 처리기를 전달 ADO **ConnectionEvent** ADO/WFC 인스턴스의 매개 변수 **ConnectionEvent** 클래스나 ADO **RecordsetEvent** 에서 매개 변수는 인스턴스의 ADO/WFC **RecordsetEvent** 클래스입니다. 이러한 ADO/WFC 클래스 통합 ADO 이벤트 매개 변수입니다. 각 ADO/WFC 클래스 모든 ADO 각 고유 매개 변수에 대해 하나의 데이터 멤버를 포함 하는, 즉 **ConnectionEvent** 하거나 **RecordsetEvent** 메서드.  
  
5.  ADO/WFC ADO/WFC 이벤트 개체를 사용 하 여 이벤트 처리기를 호출합니다. 예를 들어 프로그램 **onConnectComplete** 처리기를 사용 하면 다음과 같은 시그니처가:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     첫 번째 인수는 이벤트를 전송 하는 개체의 형식 ([연결](../../../ado/reference/ado-api/connection-object-ado.md) 하거나 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)), 두 번째 인수는 ADO/WFC 이벤트 개체 (**ConnectionEvent** 또는 **RecordsetEvent**).  
  
     이벤트 처리기의 서명을 ADO 이벤트 보다 더 쉽습니다. 그러나 이벤트 적용할 매개 변수 및 응답 하는 방법을 알아야 ADO 이벤트 모델도 이해 해야 합니다.  
  
6.  ADO 이벤트에 대 한 ADO/WFC 처리기에 이벤트 처리기에서 반환 합니다. ADO/WFC ADO 이벤트 매개 변수를 다시 관련 ADO/WFC 이벤트 데이터 멤버를 복사 하 고 ADO 이벤트 처리기를 반환 하는 합니다.  
  
7.  완료 되 면 처리기 ADO/WFC 이벤트 처리기의 목록에서 제거를 처리 합니다. 와 같은 이름을 가진 메서드를 사용 **removeOn** *EventName*(*처리기*).  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 구문 인덱스](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 처리기를 함께 작동](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)
