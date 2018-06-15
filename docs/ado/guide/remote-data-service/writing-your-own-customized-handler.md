---
title: 사용자 고유의 사용자 지정된 처리기 작성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b9cb903d276357e46489dbdcd316d4f3974087a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274702"
---
# <a name="writing-your-own-customized-handler"></a>사용자 고유의 사용자 지정된 처리기 작성
RDS 지원, 기본 IIS 서버 관리자 모르는 경우 자신만 처리기를 작성 하려는 수 있지만 사용자 요청 더 자세하게 제어 및 액세스 권한을 합니다.  
  
 MSDFMAP 합니다. 처리기 구현 하는 **예기치 않은** 인터페이스입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="idatafactoryhandler-interface"></a>예기치 않은 동작이  
 이 인터페이스에는 두 가지 방법 **GetRecordset** 및 **Reconnect**합니다. 두 방법 모두 해야 하는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성으로 설정할 수 **adUseClient**합니다.  
  
 두 방법 모두 표시 되는 인수에서 첫 번째 쉼표 뒤의 "**처리기 =**" 키워드입니다. 예를 들어 `"Handler=progid,arg1,arg2;"` 의 인수 문자열을 전달 하는 `"arg1,arg2"`, 및 `"Handler=progid"` null 인수를 전달 합니다.  
  
## <a name="getrecordset-method"></a>GetRecordset 메서드  
 이 메서드는 데이터 소스를 쿼리 하 고 새 만듭니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 제공 된 인수를 사용 하 여 개체입니다. **레코드 집합** 으로 열어야 **adLockBatchOptimistic** 비동기적으로 열 수 있어야 합니다.  
  
### <a name="arguments"></a>인수  
 ***conn*** 연결 문자열입니다.  
  
 ***args*** 처리기에 대 한 인수입니다.  
  
 ***쿼리*** 명령 텍스트를 쿼리 합니다.  
  
 ***ppRS*** 포인터 위치는 **레코드 집합** 반환 되어야 합니다.  
  
## <a name="reconnect-method"></a>메서드를 다시 연결  
 이 메서드는 데이터 소스를 업데이트 합니다. 만드는 새 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체와 연결 합니다.는 주어진 **레코드 집합**합니다.  
  
### <a name="arguments"></a>인수  
 ***conn*** 연결 문자열입니다.  
  
 ***args*** 처리기에 대 한 인수입니다.  
  
 ***Pr*** A **레코드 집합** 개체입니다.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 이 인터페이스 정의 대 한 **예기치 않은** 에 표시 되는 **msdfhdl.idl** 파일입니다.  
  
```  
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필요한 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


