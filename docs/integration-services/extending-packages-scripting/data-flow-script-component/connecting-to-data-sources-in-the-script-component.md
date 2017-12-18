---
title: "스크립트 구성 요소에서 데이터 원본에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ff502af31334a22e6459aa281ccc846e8d34f47d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>스크립트 구성 요소에서 데이터 원본에 연결
  연결 관리자는 특정 유형의 데이터 원본에 연결하는 데 필요한 정보를 캡슐화하고 저장하는 편리한 단위입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **연결 관리자** 페이지에서 **추가** 및 **제거** 단추를 클릭하여 원본 또는 대상 구성 요소의 사용자 지정 스크립트에서 기존 연결 관리자에 액세스할 수 있게 할 수 있습니다. 그러나 데이터를 로드하거나 저장하고 데이터 원본에 대한 연결을 열고 닫는 사용자 지정 코드는 개발자가 직접 작성해야 합니다. **스크립트 변환 편집기**의 **연결 관리자** 페이지에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) 및 [스크립트 변환 편집기&#40;연결 관리자 페이지&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)를 참조하세요.  
  
 스크립트 구성 요소는 각 연결 관리자에 대해 해당 연결 관리자와 동일한 이름을 갖는 강력한 형식의 접근자가 있는 **Connections** 컬렉션 클래스를 **ComponentWrapper** 프로젝트 항목에 만듭니다. 이 컬렉션은 **ScriptMain** 클래스의 **Connections** 속성을 통해 제공됩니다. 접근자 속성은 해당 연결 관리자에 대한 참조를 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>의 인스턴스로 반환합니다. 예를 들어 대화 상자의 연결 관리자 페이지에서 `MyADONETConnection`이라는 연결 관리자를 추가한 경우 스크립트에서 다음 코드를 추가하여 해당 연결 관리자에 대한 참조를 가져올 수 있습니다.  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  **AcquireConnection**을 호출하려면 먼저 연결 관리자에서 반환하는 연결 유형을 알고 있어야 합니다. 스크립트 태스크에는 **Option Strict**가 설정되어 있으므로 **개체** 형식으로 반환된 연결을 사용하려면 먼저 이 연결을 적절한 연결 형식으로 캐스팅해야 합니다.  
  
 그런 다음 특정 연결 관리자의 **AcquireConnection** 메서드를 호출하여 기본 연결이나 데이터 원본에 연결하는 데 필요한 정보를 가져옵니다. 예를 들어 다음 코드를 사용하여 ADO.NET 연결 관리자에 의해 래핑된 **System.Data.SqlConnection**에 대한 참조를 가져올 수 있습니다.  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 반면 플랫 파일 연결 관리자에 대해 동일한 메서드를 호출할 경우에는 파일 데이터 원본의 경로와 파일 이름만 반환됩니다.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 플랫 파일의 데이터를 읽거나 쓰려면 **System.IO.StreamReader** 또는 **Streamwriter**에 이 경로와 파일 이름을 제공해야 합니다.  
  
> [!IMPORTANT]  
>  스크립트 구성 요소에서 관리 코드를 작성하는 경우 OLE DB 연결 관리자 및 Excel 연결 관리자와 같이 관리되지 않는 개체를 반환하는 연결 관리자의 AcquireConnection 메서드는 호출할 수 없습니다. 그러나 이러한 연결 관리자의 ConnectionString 속성을 읽고 **System.Data.OleDb** 네임스페이스에서 OLEDB **connection**의 연결 문자열을 사용하여 코드에서 직접 데이터 원본에 연결할 수 있습니다.  
>   
>  관리되지 않는 개체를 반환하는 연결 관리자의 AcquireConnection 메서드를 호출해야 하는 경우에는 ADO.NET 연결 관리자를 사용합니다. ADO.NET 연결 관리자에서 OLE DB 공급자를 사용하도록 구성할 경우 이 연결 관리자는 .NET Framework Data Provider for OLE DB를 사용하여 연결합니다. 이 경우 AcquireConnection 메서드는 관리되지 않는 개체 대신 **System.Data.OleDb.OleDbConnection**을 반환합니다. ADO.NET 연결 관리자를 Excel 데이터 원본에 사용할 수 있도록 구성하려면 **연결 관리자** 대화 상자의 **모두** 페이지에서 Microsoft OLE DB Provider for Jet를 선택하고 Excel 통합 문서를 지정한 다음 **확장 속성** 값으로 `Excel 8.0`(Excel 97 이상의 경우)을 입력합니다.  
  
 스크립트 구성 요소에 연결 관리자를 사용하는 방법에 대한 자세한 내용은 [스크립트 구성 요소를 사용하여 원본 만들기](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) 및 [스크립트 구성 요소를 사용하여 대상 만들기](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services&#40;SSIS&#41; 연결](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [연결 관리자 만들기](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
