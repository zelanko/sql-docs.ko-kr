---
title: "스크립트 구성 요소에서 데이터 원본에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2accca553f1bd9c536076fd0bbcebbff0ff2c42
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-component"></a>스크립트 구성 요소에서 데이터 원본에 연결
  연결 관리자는 특정 유형의 데이터 원본에 연결하는 데 필요한 정보를 캡슐화하고 저장하는 편리한 단위입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
 사용할 수 있습니다 기존 연결 관리자 액세스를 위해 원본 또는 대상 구성 요소의 사용자 지정 스크립트를 클릭 하 여는 **추가** 및 **제거** 단추를 **연결 관리자** 의 페이지는 **스크립트 변환 편집기**합니다. 그러나 데이터를 로드하거나 저장하고 데이터 원본에 대한 연결을 열고 닫는 사용자 지정 코드는 개발자가 직접 작성해야 합니다. 에 대 한 자세한 내용은 **연결 관리자** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) 및 [스크립트 변환 편집기 &#40; 연결 관리자 페이지 &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 스크립트 구성 요소를 만듭니다는 **연결** 의 컬렉션 클래스는 **ComponentWrapper** 자체 연결 관리자와 동일한 이름을 가진 각 연결 관리자에 대 한 강력한 형식의 접근자를 포함 하는 프로젝트 항목입니다. 이 컬렉션을 통해 노출 되는 **연결** 의 속성은 **ScriptMain** 클래스입니다. 접근자 속성은 해당 연결 관리자에 대한 참조를 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>의 인스턴스로 반환합니다. 예를 들어 대화 상자의 연결 관리자 페이지에서 `MyADONETConnection`이라는 연결 관리자를 추가한 경우 스크립트에서 다음 코드를 추가하여 해당 연결 관리자에 대한 참조를 가져올 수 있습니다.  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  호출 하기 전에 연결 관리자에서 반환 되는 연결 유형을 알고 있어야 **AcquireConnection**합니다. 스크립트 태스크에 있기 때문에 **Option Strict** 활성화 형식으로 반환 되는 연결을 캐스팅 해야 **개체**, 적절 한 연결 유형에 사용할 수 있습니다.  
  
 그런 다음 호출에서 **AcquireConnection** 메서드를 기본 연결 또는 데이터 원본에 연결 하는 데 필요한 정보를 가져올 특정 연결 관리자의 합니다. 에 대 한 참조를 가져올 예를 들어는 **System.Data.SqlConnection** ADO.NET 연결 관리자는 다음 코드를 사용 하 여 래핑됩니다.  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 반면 플랫 파일 연결 관리자에 대해 동일한 메서드를 호출할 경우에는 파일 데이터 원본의 경로와 파일 이름만 반환됩니다.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 다음이 경로 파일 이름을 제공 해야 합니다는 **System.IO.StreamReader** 또는 **Streamwriter** 플랫 파일의 데이터를 쓰거나 읽을 수 있습니다.  
  
> [!IMPORTANT]  
>  스크립트 구성 요소에서 관리 되는 코드를 작성 하는 경우에 OLE DB 연결 관리자 및 Excel 연결 관리자와 같은 관리 되지 않는 개체를 반환 하는 관리자를 연결에 대 한 AcquireConnection 메서드를 호출할 수 없습니다. 그러나 이러한 연결 관리자의 ConnectionString 속성을 읽을 수 있으며 OLEDB의 연결 문자열을 사용 하 여 코드에서 직접 데이터 원본에 연결 **연결** 에서 **System.Data.OleDb** 네임 스페이스입니다.  
>   
>  관리 되지 않는 개체를 반환 하는 연결 관리자의 AcquireConnection 메서드를 호출 해야 할 경우 ADO.NET 연결 관리자를 사용 합니다. ADO.NET 연결 관리자에서 OLE DB 공급자를 사용하도록 구성할 경우 이 연결 관리자는 .NET Framework Data Provider for OLE DB를 사용하여 연결합니다. 이 경우에 대 한 AcquireConnection 메서드 반환는 **System.Data.OleDb.OleDbConnection** 관리 되지 않는 개체 대신 합니다. Excel 데이터 원본 사용에 대 한 ADO.NET 연결 관리자를 구성 하려면 Microsoft OLE DB Provider for Jet 선택, Excel 통합 문서를 지정 하 고 다음을 입력 `Excel 8.0` (Excel 97 이상)의 값으로 **Extended Properties** 에 **모든** 의 페이지는 **연결 관리자** 대화 상자.  
  
 스크립트 구성 요소와 연결 관리자를 사용 하는 방법에 대 한 자세한 내용은 참조 [스크립트 구성 요소를 사용 하 여 원본 만들기](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) 및 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services &#40; Ssis&#41; 연결](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [연결 관리자 만들기](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
