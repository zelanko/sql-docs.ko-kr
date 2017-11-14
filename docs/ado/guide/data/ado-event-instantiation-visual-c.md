---
title: "ADO 이벤트 인스턴스화: Visual c + + | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
ms.assetid: 385ad90a-37d0-497c-94aa-935d21fed78f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7b72af426b28b0c9c7a1581df303589b2b2831d0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ado-event-instantiation-visual-c"></a>ADO 이벤트 인스턴스화: Visual c + +
Microsoft® C++®에서 ADO 이벤트를 인스턴스화하는 방법에 도식 설명입니다. 참조 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md) 설명과 합니다.  
  
 파생 된 클래스를 만들기는 **ConnectionEventsVt** 및 **RecordsetEventsVt** 인터페이스 파일 adoint.h에서 찾을 수 있습니다.  
  
```  
// BeginEventExampleVC01  
class CConnEvent : public ConnectionEventsVt  
{  
    public:  
    STDMETHODIMP InfoMessage(   
            ADOError *pError,  
            EventStatusEnum *adStatus,  
            _ADOConnection *pConnection);  
...  
}  
  
class CRstEvent : public RecordsetEventsVt   
{  
    public:  
        STDMETHODIMP WillChangeField(   
                LONG cFields,  
                VARIANT Fields,  
                EventStatusEnum *adStatus,  
                _ADORecordset *pRecordset);  
...  
}  
// EndEventExampleVC01  
```  
  
 두 클래스 모두에서 각 이벤트 처리기 메서드를 구현 합니다. 각 메서드에 단순히 HRESULT의 S_OK를 반환 만으로는 합니다. 그러나 수행할 때 그 알려진 이벤트 처리기를 사용할 수 있는, 기본적으로 지속적으로 호출 합니다. 대신, 하려는 경우도 처음 추가 알림이 설정 하 여 요청 **adStatus** 를 **adStatusUnwantedEvent**합니다.  
  
```  
// BeginEventExampleVC02  
STDMETHODIMP CConnEvent::ConnectComplete(  
            ADOError *pError,  
            EventStatusEnum *adStatus,  
            _ADOConnection *pConnection)   
        {  
        *adStatus = adStatusUnwantedEvent;  
        return S_OK;  
        }  
  
// EndEventExampleVC02  
```  
  
 이벤트 클래스에서 상속 **IUnknown**구현 해야 하므로 **QueryInterface**, **AddRef**, 및 **릴리스** 메서드. 클래스 생성자 및 소멸자를 구현할 수도 있습니다. 이 부분에서는 작업을 간소화 하기 위해 가장 능숙 하는 Visual c + + 도구를 선택 합니다.  
  
 알 수 있는 이벤트 처리기 되어 사용할 수 있는 실행 하 여 확인 **QueryInterface** 에 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 및 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 에 대 한 개체는  **IConnectionPointContainer** 및 **IConnectionPoint** 인터페이스입니다. 그런 다음 실행할 **IConnectionPoint::Advise** 각 클래스에 대 한 합니다.  
  
 예를 들어 사용자가 반환 하는 부울 함수 사용을 가정 **True** 성공적으로 알리는 경우는 **레코드 집합** 이벤트 처리기를 사용할 수 있는 개체입니다.  
  
```  
// BeginEventExampleVC03  
HRESULT    hr;  
DWORD      dwEvtClass;  
IConnectionPointContainer    *pCPC = NULL;  
IConnectionPoint             *pCP = NULL;  
CRstEvent                    *pRStEvent = NULL;  
...  
_RecordsetPtr                pRs;  
pRs.CreateInstance(__uuidof(Recordset));  
pRStEvent = new CRstEvent;  
if (pRStEvent == NULL) return FALSE;  
...  
hr = pRs->QueryInterface(IID_IConnectionPointContainer, (LPVOID *)&pCPC);  
if (FAILED(hr)) return FALSE;  
hr = pCPC->FindConnectionPoint(RecordsetEvents, &pCP);  
pCPC->Release();    // Always Release now, even before checking.  
if (FAILED(hr)) return FALSE;  
hr = pCP->Advise(pRstEvent, &dwEvtClass);   //Turn on event support.  
pCP->Release();  
if (FAILED(hr)) return FALSE;  
...  
return TRUE;  
...  
// EndEventExampleVC03  
```  
  
 이 시점에 대 한 이벤트는 **RecordsetEvent** 제품군을 사용할 수 있고으로 메서드를 호출할지 **레코드 집합** 이벤트가 발생 합니다.  
  
 나중에 이벤트 처리기를 사용할 수 없도록 설정 하려는 경우 연결 지점을 다시 가져오고 발급는 **IConnectionPoint::Unadvise** 메서드.  
  
```  
// BeginEventExampleVC04  
...  
hr = pCP->Unadvise(dwEvtClass);    //Turn off event support.  
pCP->Release();  
if (FAILED(hr)) return FALSE;  
...  
// EndEventExampleVC04  
```  
  
 인터페이스를 해제 하 고 적절 하 게 클래스 개체를 삭제 해야 합니다.  
  
 다음 코드와의 완전 한 예제는 **레코드 집합** 이벤트 싱크 클래스입니다.  
  
```  
// BeginEventExampleVC05.cpp  
// compile with: /LD  
#include <adoint.h>  
  
class CADORecordsetEvents : public RecordsetEventsVt {  
  
public:  
   ULONG m_ulRefCount;  
   CADORecordsetEvents():m_ulRefCount(1){}  
  
   STDMETHOD(QueryInterface)(REFIID iid, LPVOID * ppvObject) {  
      if (IsEqualIID(__uuidof(IUnknown), iid) || IsEqualIID(__uuidof(RecordsetEventsVt), iid)) {  
         *ppvObject = this;  
         return S_OK;  
      }  
      else   
         return E_NOINTERFACE;  
   }  
  
   STDMETHOD_(ULONG, AddRef)() {  
      return m_ulRefCount++;  
   }  
  
   STDMETHOD_(ULONG, Release)() {  
      if (--m_ulRefCount == 0) {  
         delete this;  
         return 0;  
      }  
      else   
         return m_ulRefCount;  
   }  
  
   STDMETHOD(WillChangeField)( LONG cFields,   
                               VARIANT Fields,   
                               EventStatusEnum *adStatus,  
                               _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(FieldChangeComplete)( LONG cFields,  
                                   VARIANT Fields,  
                                   ADOError *pError,  
                                   EventStatusEnum *adStatus,  
                                   _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(WillChangeRecord)( EventReasonEnum adReason,  
                                LONG cRecords,  
                                EventStatusEnum *adStatus,  
                                _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(RecordChangeComplete)( EventReasonEnum adReason,  
                                    LONG cRecords,  
                                    ADOError  *pError,  
                                    EventStatusEnum  *adStatus,  
                                    _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(WillChangeRecordset)( EventReasonEnum adReason,  
                                   EventStatusEnum *adStatus,  
                                   _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(RecordsetChangeComplete)( EventReasonEnum adReason,  
                                       ADOError *pError,  
                                       EventStatusEnum  *adStatus,  
                                       _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(WillMove)( EventReasonEnum adReason,  
                        EventStatusEnum  *adStatus,  
                        _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(MoveComplete)( EventReasonEnum adReason,  
                            ADOError *pError,  
                            EventStatusEnum *adStatus,  
                            _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(EndOfRecordset)( VARIANT_BOOL *fMoreData,  
                              EventStatusEnum *adStatus,  
                              _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(FetchProgress)( long Progress,  
                             long MaxProgress,  
                             EventStatusEnum *adStatus,  
                             _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(FetchComplete)( ADOError *pError,  
                             EventStatusEnum *adStatus,  
                             _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
};  
```

