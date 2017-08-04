---
title: "데이터 흐름의 데이터 형식 작업 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
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
- custom data flow components [Integration Services], mapping data types
- data flow components [Integration Services], mapping data types
- data types [Integration Services], converting
ms.assetid: 941260d0-4ec3-4bf0-ab48-2b26733e6b24
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f020b16fd9609c64ed6a421c9c9f5e593d70276b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="working-with-data-types-in-the-data-flow"></a>데이터 흐름의 데이터 형식 작업
  Integration Services에서 사용자 지정 데이트 흐름 구성 요소를 개발할 때는 데이터를 데이터 흐름 버퍼에 복사하거나 데이터 흐름 버퍼에서 복사해 오고 값을 변환하는 방식으로 데이터 형식에 대한 작업을 지속적으로 수행하게 됩니다. 이 항목에서는 올바른 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 선택하고 데이터 형식에 대한 작업을 수행할 때 올바른 메서드를 사용할 수 있도록 유용한 정보를 제공합니다.  
  
## <a name="inserting-data-into-the-data-flow"></a>데이터 흐름에 데이터 삽입  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 클래스 제공 하는 일련의 **설정** 를 버퍼 열과 해당 일련의으로 데이터를 복사 하기 위한 메서드 **가져오기** 버퍼 열에서 데이터를 검색 하기 위한 방법입니다. 다음 표에서 각 사용 방법을 보여 줍니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식입니다.  
  
### <a name="set-methods-to-use-with-data-types"></a>데이터 형식에 사용할 수 있는 Set 메서드  
 다음 표에서 첫 번째 열의 데이터 형식을 나열 하 고 그런 다음 해당 나열 **설정** 및 **가져오기** 메서드.  
  
|데이터 형식|Set 메서드|Get 메서드|  
|---------------|----------------|----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BOOL>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetBoolean%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetBoolean%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BYTES>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetBytes%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetBytes%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_CY>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDecimal%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDecimal%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DATE>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTime%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDateTime%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBDATE>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDate%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDate%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetTime%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetTime%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME2>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetTime%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetTime%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTime%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDateTime%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP2>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTime%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDateTime%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMPOFFSET>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTimeOffset%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDateTimeOffset%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DECIMAL>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDecimal%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDecimal%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_FILETIME>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTime%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDateTime%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_GUID>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetGuid%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetGuid%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I1>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetSByte%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetSByte%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I2>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetInt16%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetInt16%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I4>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetInt32%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetInt32%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I8>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetInt64%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetInt64%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_IMAGE>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>또는<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetBlobData%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NTEXT>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>또는<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetBlobData%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NULL>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetNull%2A>|없는 **가져오기** 이 데이터 형식에 적용 되는 메서드.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NUMERIC>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDecimal%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDecimal%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_R4>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetSingle%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetSingle%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_R8>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDouble%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetDouble%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_STR>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetString%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetString%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_TEXT>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>또는<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetBlobData%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI1>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetByte%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetByte%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI2>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetUInt16%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetUInt16%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI4>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetUInt32%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetUInt32%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI8>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetUInt64%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetUInt64%2A>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_WSTR>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetString%2A>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.GetString%2A>|  
  
### <a name="data-types-to-use-with-the-set-methods"></a>Set 메서드와 함께 사용할 수 있는 데이터 형식  
  
|Set 메서드|데이터 형식|  
|----------------|---------------|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>또는<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddBlobData%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_IMAGE>, <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NTEXT> 또는 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_TEXT>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetBoolean%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BOOL>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetByte%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI1>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetBytes%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BYTES>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDate%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBDATE>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTime%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DATE>, <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>, <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP2> 또는 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_FILETIME>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDateTimeOffset%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMPOFFSET>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDecimal%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_CY>, <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DECIMAL> 또는 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NUMERIC>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetDouble%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_R8>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetGuid%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_GUID>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetInt16%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I2>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetInt32%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I4>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetInt64%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I8>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetNull%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NULL>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetSByte%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I1>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetSingle%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_R4>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetString%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_STR>또는<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_WSTR>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetTime%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME>또는<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME2>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetUInt16%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI2>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetUInt32%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI4>|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetUInt64%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI8>|  
  
## <a name="mapping-data-types-in-the-data-flow"></a>데이터 흐름에서 데이터 형식 매핑  
 데이터 원본에서 변환 거쳐 대상으로 이동 하는 동안 데이터 흐름 구성 요소 간에 데이터 형식을 변환 경우가 해야는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에 정의 된 형식을 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType> 의 관리 되는 데이터 형식과 열거형은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 에 정의 된는 **시스템** 네임 스페이스입니다. 또한 구성 요소에서는 하나의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 다른 형식으로 변환한 후에만 관리되는 형식으로 변환할 수 있는 경우가 종종 있습니다.  
  
> [!NOTE]  
>  기본적으로 C:\Program Files\Microsoft SQL Server\130\DTS\MappingFiles를 설치 하는 XML 형식의 매핑 파일은이 항목에서 설명 하는 데이터 형식 매핑과 관련이 없습니다. 이러한 파일은 예를 들어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 데이터 형식을 Oracle의 데이터 형식에 매핑하는 경우와 같이 한 데이터베이스 버전 또는 시스템의 데이터 형식을 다른 데이터 형식에 매핑하며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서만 사용됩니다. 이러한 매핑 파일에 대 한 자세한 내용은 참조 하십시오. [SQL Server 가져오기 및 내보내기 마법사](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)합니다.  
  
### <a name="mapping-between-integration-services-and-managed-data-types"></a>Integration Services와 관리되는 데이터 형식 간의 매핑  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A> 메서드는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 관리되는 데이터 형식에 매핑합니다.  
  
> [!CAUTION]  
>  개발자는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 클래스의 이러한 메서드를 신중히 사용해야 하며, 사용자 지정 구성 요소의 고유한 요구 사항에 보다 적합한 데이터 형식 매핑 메서드를 직접 코딩할 수도 있습니다. 기존 메서드는 전체 자릿수 또는 소수 자릿수나 데이터 형식 자체와 밀접하게 관련된 그 밖의 속성을 고려하지 않습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서는 이후 버전의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 이러한 메서드를 수정 또는 제거하거나 이러한 메서드가 수행하는 매핑을 수정할 수 있습니다.  
  
 다음 표에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A> 메서드가 다양한 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 관리되는 데이터 형식에 매핑하는 방식을 보여 줍니다.  
  
|Integration Services 데이터 형식|매핑 대상(관리되는 데이터 형식)|  
|------------------------------------|------------------------------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_WSTR>|System.String|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BYTES>|System.Byte의 배열|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>|System.DateTime|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP2>|System.DateTime|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMPOFFSET>|System.DateTimeOffset|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBDATE>|System.DateTime|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME>|System.TimeSpan|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME2>|System.TimeSpan|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DATE>|System.DateTime|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_FILETIME>|System.DateTime|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NUMERIC>|System.Decimal|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_GUID>|System.Guid|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I1>|System.SByte|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I2>|System.Int16|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I4>|System.Int32|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I8>|System.Int64|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BOOL>|System.Boolean|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_R4>|System.Single|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_R8>|System.Double|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI1>|System.Byte|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI2>|System.UInt16|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI4>|System.UInt32|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_UI8>|System.UInt64|  
  
### <a name="mapping-integration-services-data-types-to-fit-managed-data-types"></a>관리되는 데이터 형식에 맞게 Integration Services 데이터 형식 매핑  
 데이터 흐름 구성 요소에서는 한 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 다른 데이터 형식으로 변환한 후에만 해당 형식을 관리되는 형식으로 변환할 수 있는 경우도 종종 있습니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A> 메서드 클래스 지도 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 다른 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 를 사용 하 여 관리 되는 데이터 형식에 매핑할 수 있습니다는 데이터 형식에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 메서드.  
  
> [!CAUTION]  
>  개발자는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 클래스의 이러한 메서드를 신중히 사용해야 하며, 사용자 지정 구성 요소의 고유한 요구 사항에 보다 적합한 데이터 형식 매핑 메서드를 직접 코딩할 수도 있습니다. 기존 메서드는 전체 자릿수 또는 소수 자릿수나 데이터 형식 자체와 밀접하게 관련된 그 밖의 속성을 고려하지 않습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서는 이후 버전의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 이러한 메서드를 수정 또는 제거하거나 이러한 메서드가 수행하는 매핑을 수정할 수 있습니다.  
  
 다음 표에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A> 메서드가 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 다른 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방식을 보여 줍니다.  
  
|원본 Integration Services 데이터 형식|매핑 대상(Integration Services 데이터 형식)|  
|---------------------------------------------|-------------------------------------------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DECIMAL>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NUMERIC>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_CY>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NUMERIC>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DATE>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBDATE>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_FILETIME>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP2>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIMESTAMP>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_DBTIME2>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BOOL>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_I4>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_TEXT>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_WSTR>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_NTEXT>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_WSTR>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_STR>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_WSTR>|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_IMAGE>|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DataType.DT_BYTES>|  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A> 메서드는 DT_DBTIMESTAMPOFFSET 데이터 형식에 대한 값은 반환하지 않으며 이때 <xref:Microsoft.SqlServer.Dts.Pipeline.UnsupportedBufferDataTypeException>이 발생됩니다. 따라서 DT_DBTIMESTAMPOFFSET 데이터 형식은 관리되는 데이터 형식에 매핑할 수 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 날짜/시간 데이터 형식 중 하나로 변환해야 합니다. 관리되는 데이터 형식에 매핑할 수 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 날짜/시간 데이터 형식의 목록은 앞부분의 "Integration Services와 관리되는 데이터 형식 간의 매핑" 섹션에 나오는 표를 참조하십시오. 데이터 형식으로 변환 하는 방법에 대 한 정보를 참조 하십시오. [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A>   
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>   
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>   
 [Integration Services 데이터 형식](../../../integration-services/data-flow/integration-services-data-types.md)  
  
  

