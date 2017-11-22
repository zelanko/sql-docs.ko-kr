---
title: "ADO 이벤트 인스턴스화: ADO 및 WFC | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffe0911f2845e7ff7e41cf41fcc4f267f7c0ad66
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 이벤트 인스턴스화: ADO 및 WFC
ADO에 대 한 Windows Foundation Class (ADO/WFC) ADO 이벤트 모델을 바탕으로 하며 단순화 된 응용 프로그램 프로그래밍 인터페이스를 제공 합니다. 일반적으로 ADO/WFC 차단 ADO 이벤트, 이벤트 매개 변수는 단일 이벤트 클래스를 통합 하 고 이벤트 처리기를 호출 합니다.  
  
### <a name="to-use-ado-events-in-adowfc"></a>ADO/WFC ADO 이벤트를 사용 하려면  
  
1.  이벤트를 처리할 이벤트 처리기를 정의 합니다. 예를 들어 처리 하려는 경우는 **ConnectComplete** 이벤트에는 **ConnectionEvent** 패밀리를 사용할 수 있습니다이 코드:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  처리기 개체를 나타내는 이벤트 처리기를 정의 합니다. 처리기 개체 데이터 형식 이어야 합니다 **ConnectEventHandler** 형식의 이벤트에 대 한 **ConnectionEvent**, 또는 데이터 형식 **RecordsetEventHandler** 형식의이벤트에대한 **RecordsetEvent**합니다. 예를 들어 코드에 대 한 다음 프로그램 **ConnectComplete** 이벤트 처리기.  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     첫 번째 인수는 **ConnectionEventHandler** 생성자는 두 번째 인수에 명명 된 이벤트 처리기를 포함 하는 클래스에 대 한 참조입니다.  
  
3.  이벤트 처리기는 특정 형식의 이벤트를 처리 하도록 지정 된 처리기의 목록에 추가 합니다. 와 같은 이름을 가진 메서드를 사용 **addOn***EventName*(*처리기*).  
  
4.  ADO/WFC 모든 ADO 이벤트 처리기를 내부적으로 구현합니다. 이벤트에 의해 발생할 따라서는 **연결** 또는 **레코드 집합** 작업 ADO/WFC 이벤트 처리기에 의해 차단 됩니다.  
  
     ADO/WFC 이벤트 처리기 전달 ADO **ConnectionEvent** ADO/WFC 인스턴스의 매개 변수 **ConnectionEvent** 클래스 또는 ADO **RecordsetEvent** 의 매개 변수는 ADO/WFC 인스턴스의 **RecordsetEvent** 클래스입니다. 이러한 ADO/WFC 클래스에서는 ADO 이벤트 매개 변수를 통합합니다. 즉, 각 ADO/WFC 클래스는 모든 ado에서 고유한 각 매개 변수에 대해 하나의 데이터 멤버 **ConnectionEvent** 또는 **RecordsetEvent** 메서드.  
  
5.  ADO/WFC ADO/WFC 이벤트 개체와 이벤트 처리기를 호출합니다. 예를 들어 프로그램 **onConnectComplete** 처리기에는 다음과 같은 서명:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     첫 번째 인수는 이벤트를 보낸 개체의 형식 ([연결](../../../ado/reference/ado-api/connection-object-ado.md) 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)), 두 번째 인수는 ADO/WFC 이벤트 개체 (**ConnectionEvent** 또는 **RecordsetEvent**).  
  
     이벤트 처리기의 서명을 더 ADO 이벤트 보다 간단 합니다. 그러나 이벤트에 적용할 매개 변수를 응답 하는 방법에 알고 ADO 이벤트 모델은 여전히 이해 해야 합니다.  
  
6.  이벤트 처리기에서 ADO 이벤트에 대 한 ADO/WFC 처리기에 반환 합니다. ADO/WFC ADO 이벤트 매개 변수를 다시 관련 ADO/WFC 이벤트 데이터 멤버를 복사 하 고 ADO 이벤트 처리기의 반환 합니다.  
  
7.  완료 되 면 ADO/WFC 이벤트 처리기의 목록에서 처리기를 제거를 처리 합니다. 와 같은 이름을 가진 메서드를 사용 **removeOn***EventName*(*처리기*).  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 구문 인덱스](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 처리기 함께 작동 하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)
