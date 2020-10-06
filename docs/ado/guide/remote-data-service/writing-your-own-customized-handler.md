---
description: 고유한 사용자 지정된 처리기 작성
title: 사용자 지정 처리기 작성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d761b781e7de4225f51fb3600ac467015a0c274
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722724"
---
# <a name="writing-your-own-customized-handler"></a>고유한 사용자 지정된 처리기 작성
기본 RDS 지원을 원하는 IIS 서버 관리자 인 경우 사용자 요청 및 액세스 권한을 더 자세히 제어 하려면 고유한 처리기를 작성 하는 것이 좋습니다.  
  
 MSDFMAP입니다. 처리기는 **IDataFactoryHandler** 인터페이스를 구현 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler 인터페이스  
 이 인터페이스에는 두 가지 메서드인 **Getrecordset** 및 **Reconnect**가 있습니다. 두 방법 모두 [CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 해야 합니다.  
  
 두 메서드는 "**Handler =**" 키워드의 첫 번째 쉼표 뒤에 나오는 인수를 사용 합니다. 예를 들어 `"Handler=progid,arg1,arg2;"` 는의 인수 문자열을 전달 `"arg1,arg2"` 하 고는 `"Handler=progid"` null 인수를 전달 합니다.  
  
## <a name="getrecordset-method"></a>GetRecordset 메서드  
 이 메서드는 데이터 소스를 쿼리하고 제공 된 인수를 사용 하 여 새 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 만듭니다. **레코드 집합** 은 **Adlockbatchoptimistic** 으로 열어야 하며 비동기식으로 열지 않아야 합니다.  
  
### <a name="arguments"></a>인수  
 ***conn***  연결 문자열입니다.  
  
 ***args***  처리기에 대 한 인수입니다.  
  
 ***쿼리***  쿼리를 만들기 위한 명령 텍스트입니다.  
  
 ***ppRS***  **레코드 집합** 을 반환 해야 하는 포인터입니다.  
  
## <a name="reconnect-method"></a>Reconnect 메서드  
 이 메서드는 데이터 소스를 업데이트 합니다. 새 [연결](../../reference/ado-api/connection-object-ado.md) 개체를 만들고 지정 된 **레코드 집합**을 연결 합니다.  
  
### <a name="arguments"></a>인수  
 ***conn***  연결 문자열입니다.  
  
 ***args***  처리기에 대 한 인수입니다.  
  
 ***pr***  **레코드 집합** 개체입니다.  
  
## <a name="msdfhdlidl"></a>msdfhdl .idl  
 **Msdfhdl .idl** 파일에 표시 되는 **IDataFactoryHandler** 에 대 한 인터페이스 정의입니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 파일 연결 섹션](./customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](./customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](./customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](./customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정](./required-client-settings.md)   
 [사용자 지정 파일 이해](./understanding-the-customization-file.md)