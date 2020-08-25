---
description: 'ADO 이벤트 인스턴스: Visual C++'
title: 'ADO 이벤트 인스턴스화: Visual C++ | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 25271ea1cf080f8f2bb599681a54af967a2d4ad2
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806440"
---
# <a name="ado-event-instantiation-visual-c"></a>ADO 이벤트 인스턴스: Visual C++
Microsoft® Visual C++®에서 ADO 이벤트를 인스턴스화하는 방법에 대 한 구조 설명입니다. 전체 설명은 [ADO Events 모델 예제 (VC + +)](../../reference/ado-api/ado-events-model-example-vc.md) 를 참조 하세요.  
  
 Adoint 파일에 있는 **ConnectionEventsVt** 및 **RecordsetEventsVt** 인터페이스에서 파생 된 클래스를 만듭니다.  
  
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
  
 두 클래스 모두에서 각 이벤트 처리기 메서드를 구현 합니다. 각 메서드는 S_OK의 HRESULT만 반환 하면 됩니다. 그러나 이벤트 처리기를 사용할 수 있다는 것을 알고 있는 경우에는 기본적으로 계속 호출 됩니다. 대신 **Adstatus** 를 **adStatusUnwantedEvent**로 설정 하 여 추가 알림을 처음으로 요청 하는 것이 좋습니다.  
  
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
  
 이벤트 클래스는 **IUnknown**에서 상속 하므로 **QueryInterface**, **AddRef**및 **Release** 메서드도 구현 해야 합니다. 클래스 생성자 및 소멸자도 구현 합니다. 작업의이 부분을 간소화 하는 데 가장 친숙 한 Visual C++ 도구를 선택 합니다.  
  
 **IConnectionPointContainer** 및 **IConnectionPoint** 인터페이스에 대 한 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 및 [연결](../../reference/ado-api/connection-object-ado.md) 개체에 대해 **QueryInterface** 를 실행 하 여 이벤트 처리기를 사용할 수 있다는 것을 알고 있어야 합니다. 그런 다음 각 클래스에 대해 **IConnectionPoint:: Advise** 를 실행 합니다.  
  
 예를 들어, 사용할 수 있는 이벤트 처리기가 있는 **레코드 집합** 개체에 성공적으로 알리는 경우 **True** 를 반환 하는 부울 함수를 사용 한다고 가정 합니다.  
  
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
  
 이 시점에서 **RecordsetEvent** 제품군에 대 한 이벤트가 활성화 되 고 **레코드 집합** 이벤트가 발생 하는 경우 메서드가 호출 됩니다.  
  
 나중에 이벤트 처리기를 사용할 수 없게 하려면 연결 지점을 다시 가져오고 **IConnectionPoint:: Unadvise** 메서드를 실행 합니다.  
  
```  
// BeginEventExampleVC04  
...  
hr = pCP->Unadvise(dwEvtClass);    //Turn off event support.  
pCP->Release();  
if (FAILED(hr)) return FALSE;  
...  
// EndEventExampleVC04  
```  
  
 인터페이스를 해제 하 고 클래스 개체를 적절 하 게 삭제 해야 합니다.  
  
 다음 코드에서는 **레코드 집합** 이벤트 싱크 클래스의 전체 예를 보여 줍니다.  
  
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