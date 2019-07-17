---
title: 외부 메타데이터 구현 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 925db41997def8591c9304e3116f23271ed77581
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724675"
---
# <a name="implementing-external-metadata"></a>외부 메타데이터 구현

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  구성 요소와 해당 데이터 원본의 연결이 끊어진 경우 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100> 인터페이스를 사용하여 외부 데이터 원본의 열을 기준으로 입력 및 출력 열 컬렉션의 열에 대한 유효성을 검사할 수 있습니다. 이 인터페이스를 사용하면 외부 데이터 원본에 있는 열의 스냅샷을 유지 관리하고 이러한 열을 구성 요소의 입력 및 출력 열 컬렉션에 있는 열에 매핑할 수 있습니다.  
  
 외부 메타데이터 열을 구현하면 추가 열 컬렉션에 대한 유지 관리 및 유효성 검사를 수행해야 하므로 구성 요소 개발의 오버헤드와 복잡성이 늘어나지만 유효성 검사를 위한 고비용의 서버 왕복을 피할 수 있으면 이 개발 작업을 성공적으로 수행할 수 있습니다.  
  
## <a name="populating-external-metadata-columns"></a>외부 메타데이터 열 채우기  
 외부 메타데이터 열은 일반적으로 해당하는 입력 또는 출력 열이 만들어질 때 컬렉션에 추가됩니다. 새 열은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A> 메서드 호출을 통해 만들어집니다. 그런 다음 열의 속성이 외부 데이터 원본과 일치하도록 설정됩니다.  
  
 외부 메타데이터 열을 해당하는 입력 또는 출력 열에 매핑하려면 해당 입력 또는 출력 열의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> 속성에 외부 메타데이터 열의 ID를 할당합니다. 이렇게 하면 컬렉션의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> 메서드를 사용하여 특정 입력 또는 출력 열에 대한 외부 메타데이터 열을 쉽게 찾을 수 있습니다.  
  
 다음 예에서는 외부 메타데이터 열을 만든 다음 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> 속성을 설정하여 이 열을 외부 열에 매핑하는 방법을 보여 줍니다.  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>외부 메타데이터 열을 사용하여 유효성 검사  
 유효성 검사를 수행할 때는 추가 열 컬렉션을 기준으로 해야 하므로 외부 메타데이터 열 컬렉션을 유지 관리하는 구성 요소에 대한 추가 단계가 필요합니다. 유효성 검사는 연결 시 유효성 검사와 연결 해제 시 유효성 검사로 나눌 수 있습니다.  
  
### <a name="connected-validation"></a>연결 시 유효성 검사  
 구성 요소가 외부 데이터 원본에 연결되어 있는 경우 입력 또는 출력 컬렉션의 열은 외부 데이터 원본을 기준으로 직접 유효성이 검사됩니다. 외부 메타데이터 컬렉션의 열에 대한 유효성 검사도 수행해야 합니다. [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 **고급 편집기**에서는 외부 메타데이터 컬렉션을 수정할 수 있으며 이 때 컬렉션의 변경 내용은 검색할 수 없으므로 이 작업이 필요합니다. 따라서 연결된 상태일 때 구성 요소에서는 외부 메타데이터 열 컬렉션의 열이 계속해서 외부 데이터 원본의 열을 반영하는지 확인해야 합니다.  
  
 **고급 편집기**에서 외부 메타데이터 컬렉션의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A> 속성을 **false**로 설정하여 해당 컬렉션을 숨길 수 있습니다. 그러나 이렇게 하면 사용자가 입력 또는 출력 컬렉션의 열을 외부 메타데이터 열 컬렉션의 열에 매핑하는 데 사용할 수 있는 편집기의 **열 매핑** 탭도 숨겨집니다. 이 속성을 **false**로 설정해도 개발자는 컬렉션을 프로그래밍 방식으로 수정할 수 있지만 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서만 사용되는 구성 요소의 외부 메타데이터 열 컬렉션은 어느 정도 보호됩니다.  
  
### <a name="disconnected-validation"></a>연결 해제 시 유효성 검사  
 구성 요소가 외부 데이터 원본에 연결되어 있지 않은 경우 입력 또는 출력 컬렉션의 열은 외부 원본이 아니라 외부 메타데이터 컬렉션의 열을 기준으로 유효성이 검사되므로 유효성 검사 과정이 간단해집니다. 외부 데이터 원본에 대한 연결이 설정되어 있지 않거나 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 속성이 **false**인 경우 구성 요소에서는 연결 해제 시 유효성 검사를 수행해야 합니다.  
  
 다음 코드 예에서는 외부 메타데이터 열 컬렉션을 기준으로 유효성 검사를 수행하는 구성 요소의 구현을 보여 줍니다.  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  

## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)  
  
  
