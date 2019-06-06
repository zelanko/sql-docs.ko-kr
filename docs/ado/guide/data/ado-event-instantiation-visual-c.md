---
title: 'ADO 이벤트 인스턴스: Visual C++ | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 385ad90a-37d0-497c-94aa-935d21fed78f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 500beed65583eea1e1e01b34a3bb585198b219e1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700990"
---
# <a name="ado-event-instantiation-visual-c"></a>ADO 이벤트 인스턴스: Visual C++
Microsoft® C++®에서 ADO 이벤트를 인스턴스화하는 방법에 도식 설명입니다. 참조 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md) 설명은 합니다.  
  
 파생 된 클래스를 만들기는 **ConnectionEventsVt** 하 고 **RecordsetEventsVt** 인터페이스 파일 adoint.h 있는 합니다.  
  
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
  
 두 클래스 모두에서 각 이벤트 처리기 메서드를 구현 합니다. 각 메서드는 S_OK HRESULT는 단순히 반환 부족 합니다. 그러나 하는 경우이 알려진 이벤트 처리기는 사용 가능한에 기본적으로 지속적으로 호출 합니다. 설정 하 여 처음으로 후 추가 알림이 요청 하려는 하는 대신 **adStatus** 하 **adStatusUnwantedEvent**합니다.  
  
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
  
 이벤트 클래스에서 상속 **IUnknown**이므로 구현 해야 합니다 **QueryInterface**를 **AddRef**, 및 **릴리스** 메서드. 또한 클래스 생성자와 소멸자를 구현 합니다. 시각적 개체 선택 C++ 도구는 가장 편리한 작업의이 부분을 간소화 합니다.  
  
 확인 하는 알려진 해당 이벤트 처리기를 사용할 수 있습니다 실행 **QueryInterface** 에 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 하 고 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 에 대 한 개체는  **IConnectionPointContainer** 하 고 **IConnectionPoint** 인터페이스입니다. 그런 다음 실행할 **IConnectionPoint::Advise** 각 클래스에 대 한 합니다.  
  
 예를 들어, 반환 하는 부울 함수를 사용 하는 것으로 가정 **True** 성공적으로 알리는 경우를 **Recordset** 이벤트 처리기를 사용할 수 있는 개체입니다.  
  
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
  
 이 시점에 대 한 이벤트를 **RecordsetEvent** 제품군 설정 되 고 메서드를 호출할 **레코드 집합** 이벤트가 발생 합니다.  
  
 나중에 이벤트 처리기를 사용할 수 없게 하려는 경우 연결 지점을 다시 가져오고 실행 합니다 **iconnectionpoint:: Unadvise** 메서드.  
  
```  
// BeginEventExampleVC04  
...  
hr = pCP->Unadvise(dwEvtClass);    //Turn off event support.  
pCP->Release();  
if (FAILED(hr)) return FALSE;  
...  
// EndEventExampleVC04  
```  
  
 인터페이스를 해제 하 고 적절 하 게 클래스 개체를 제거 해야 합니다.  
  
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
