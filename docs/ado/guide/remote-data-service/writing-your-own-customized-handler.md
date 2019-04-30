---
title: 사용자 고유의 사용자 지정된 처리기를 작성 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daddb9057775e1f098754dd2a331c1dc77194d10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155916"
---
# <a name="writing-your-own-customized-handler"></a>고유한 사용자 지정된 처리기 작성
기본 RDS를 지원 하려는 IIS 서버 관리자 인 경우 사용자 고유의 처리기를 작성 하는 것이 좋습니다 하지만 사용자 요청을 보다 세부적으로 제어할 사용 권한과 액세스 합니다.  
  
 MSDFMAP 합니다. 처리기 구현 된 **예기치 않은** 인터페이스입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="idatafactoryhandler-interface"></a>예기치 않은 동작이  
 이 인터페이스에는 두 가지 메서드를 **GetRecordset** 하 고 **Reconnect**합니다. 두 메서드는 필요 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 설정할 수 **adUseClient**합니다.  
  
 두 메서드 모두에서 첫 번째 쉼표 뒤에 나오는 인수는 "**처리기 =**" 키워드입니다. 예를 들어 `"Handler=progid,arg1,arg2;"` 의 인수 문자열에 전달 됩니다 `"arg1,arg2"`, 및 `"Handler=progid"` null 인수를 전달 합니다.  
  
## <a name="getrecordset-method"></a>GetRecordset 메서드  
 이 메서드는 데이터 원본을 쿼리하고 만듭니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 제공 된 인수를 사용 하 여 개체입니다. 합니다 **레코드 집합** 사용 하 여 열어야 **adLockBatchOptimistic** 비동기적으로 열 수 있어야 합니다.  
  
### <a name="arguments"></a>인수  
 ***conn*** 연결 문자열입니다.  
  
 ***args*** 처리기에 대 한 인수입니다.  
  
 ***쿼리*** 명령 텍스트를 쿼리 합니다.  
  
 ***ppRS*** 포인터 위치를 **레코드 집합** 반환 되어야 합니다.  
  
## <a name="reconnect-method"></a>메서드를 다시 연결  
 이 메서드는 데이터 소스를 업데이트합니다. 새로 만듭니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체와 연결 된 지정 **레코드 집합**합니다.  
  
### <a name="arguments"></a>인수  
 ***conn*** 연결 문자열입니다.  
  
 ***args*** 처리기에 대 한 인수입니다.  
  
 ***Pr*** A **레코드 집합** 개체입니다.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 인터페이스 정의 대 한 **예기치 않은** 에 표시 되는 **msdfhdl.idl** 파일입니다.  
  
```cpp
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
 [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


