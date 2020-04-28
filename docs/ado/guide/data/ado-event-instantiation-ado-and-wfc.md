---
title: 'ADO 이벤트 인스턴스화: ADO 및 WFC | Microsoft Docs'
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
ms.openlocfilehash: 7dbbbf92c751093d2a7333b7ac1f76888d41d345
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70212335"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 이벤트 인스턴스: ADO 및 WFC
Windows Foundation 클래스 (ADO/WFC) 용 ADO는 ADO 이벤트 모델을 기반으로 하며 간소화 된 응용 프로그램 프로그래밍 인터페이스를 제공 합니다. 일반적으로 ADO/WFC는 ADO 이벤트를 가로채 고 이벤트 매개 변수를 단일 이벤트 클래스로 통합 한 다음 이벤트 처리기를 호출 합니다.  
  
### <a name="to-use-ado-events-in-adowfc"></a>ADO/WFC에서 ADO 이벤트를 사용 하려면  
  
1.  이벤트를 처리 하는 고유한 이벤트 처리기를 정의 합니다. 예를 들어 **connectionevent** Family에서 **connectcomplete** 이벤트를 처리 하려는 경우 다음 코드를 사용할 수 있습니다.  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  이벤트 처리기를 나타내는 처리기 개체를 정의 합니다. Handler 개체는 **Connectionevent**형식의 이벤트에 대 한 데이터 형식 **Connecteventhandler** 이거나 **RecordsetEvent**형식의 이벤트에 대 한 데이터 형식 **RecordsetEventHandler** 여야 합니다. 예를 들어 **Connectcomplete** 이벤트 처리기에 대해 다음 코드를 코딩 합니다.  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     **Connectioneventhandler** 생성자의 첫 번째 인수는 두 번째 인수에 명명 된 이벤트 처리기를 포함 하는 클래스에 대 한 참조입니다.  
  
3.  특정 유형의 이벤트를 처리 하도록 지정 된 처리기 목록에 이벤트 처리기를 추가 합니다. **AddOn**_EventName_(*handler*)과 같은 이름을 사용 하 여 메서드를 사용 합니다.  
  
4.  ADO/WFC는 내부적으로 모든 ADO 이벤트 처리기를 구현 합니다. 따라서 **연결** 또는 **레코드 집합** 작업에 의해 발생 한 이벤트는 ADO/WFC 이벤트 처리기에 의해 차단 됩니다.  
  
     Ado/wfc 이벤트 처리기는 ado/wfc **connectionevent** 클래스의 인스턴스 또는 ADO/wfc **RECORDSETEVENT** 클래스 인스턴스의 ado **RecordsetEvent** 매개 변수에서 ado **connectionevent** 매개 변수를 전달 합니다. 이러한 ADO/WFC 클래스는 ADO 이벤트 매개 변수를 통합 합니다. 즉, 각 ADO/WFC 클래스에는 모든 ADO **Connectionevent** 또는 **RecordsetEvent** 메서드의 고유한 매개 변수에 대 한 하나의 데이터 멤버가 포함 되어 있습니다.  
  
5.  ADO/WFC는 ADO/WFC 이벤트 개체를 사용 하 여 이벤트 처리기를 호출 합니다. 예를 들어 **Onconnectcomplete** 처리기에는 다음과 같은 시그니처가 있습니다.  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     첫 번째 인수는 이벤트를 보낸 개체의 유형 ([연결](../../../ado/reference/ado-api/connection-object-ado.md) 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md))이 고 두 번째 인수는 ADO/WFC 이벤트 개체 (**connectionevent** 또는 **RecordsetEvent**)입니다.  
  
     이벤트 처리기의 서명은 ADO 이벤트 보다 간단 합니다. 그러나 ADO 이벤트 모델을 이해 하 여 이벤트에 적용 되는 매개 변수와 응답 하는 방법을 알고 있어야 합니다.  
  
6.  이벤트 처리기에서 ADO 이벤트에 대 한 ADO/WFC 처리기로 돌아갑니다. ADO/WFC는 관련 ADO/WFC 이벤트 데이터 멤버를 다시 ADO 이벤트 매개 변수에 복사 하 고 ADO 이벤트 처리기는를 반환 합니다.  
  
7.  처리가 완료 되 면 ADO/WFC 이벤트 처리기 목록에서 처리기를 제거 합니다. **RemoveOn**_EventName_(*handler*)과 같은 이름을 사용 하 여 메서드를 사용 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 구문 인덱스](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 처리기가 함께 작동 하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [이벤트 형식](../../../ado/guide/data/types-of-events.md)
