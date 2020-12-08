---
title: 명령 실행
description: Microsoft SqlClient Data Provider for SQL Server `Command` 개체와 이를 사용하여 데이터 원본에 대한 쿼리 및 명령을 실행하는 방법을 설명합니다.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: b1427fa78e52c985478996bfb41cb7a20e1ee608
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428240"
---
# <a name="executing-a-command"></a>명령 실행

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server에는 <xref:System.Data.Common.DbCommand>에서 상속되는 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체가 있습니다. 이 개체는 다음 표에 설명된 것처럼 명령 형식 및 원하는 반환 값을 기반으로 명령을 실행하는 메서드를 노출합니다.

|명령|반환 값|  
|-------------|------------------|  
|`ExecuteReader`|`DataReader` 개체를 반환합니다.|  
|`ExecuteScalar`|단일 스칼라 값을 반환합니다.|  
|`ExecuteNonQuery`|어떠한 행도 반환하지 않는 명령을 실행합니다.|  
|`ExecuteXMLReader`|<xref:System.Xml.XmlReader>를 반환합니다. `SqlCommand` 개체에만 사용할 수 있습니다.|

 강력한 형식의 각 명령 개체는 명령 문자열의 해석 방법을 지정하는 <xref:System.Data.CommandType> 열거형도 지원합니다. 다음 표에는 CommandType의 각 열거형이 나와 있습니다.

|CommandType|설명|
|-----------------|-----------------|  
|`Text`|데이터 소스에 실행할 문을 정의하는 SQL 명령입니다.|  
|`StoredProcedure`|저장 프로시저의 이름입니다. 호출하는 `Parameters` 메서드에 관계없이 명령의 `Execute` 속성을 사용하면 입력 및 출력 매개 변수와 반환 값에 액세스할 수 있습니다.|  
|`TableDirect`|테이블의 이름입니다.|

> [!IMPORTANT]
> `ExecuteReader`를 사용하는 경우 `DataReader`가 닫히기 전에는 반환 값과 출력 매개 변수에 액세스할 수 없습니다.

## <a name="example"></a>예

다음 코드 예제에서는 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 만든 다음 해당 속성을 설정하여 저장 프로시저를 실행하는 방법을 보여 줍니다. 저장 프로시저에 대한 입력 매개 변수를 지정하는 데는 <xref:Microsoft.Data.SqlClient.SqlParameter> 개체를 사용합니다. <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReader%2A> 메서드를 사용하여 명령을 실행하고 <xref:Microsoft.Data.SqlClient.SqlDataReader>의 출력을 콘솔 창에 표시합니다.

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](~/../sqlclient/doc/samples/SqlCommand_StoredProcedure.cs#1)]

### <a name="troubleshooting-commands"></a>명령 문제 해결

[!INCLUDE[appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

Microsoft SqlClient Data Provider for SQL Server에서는 명령 실행 실패와 관련된 간헐적인 문제를 검색할 수 있도록 **성능 카운터** 가 추가되었습니다.

## <a name="see-also"></a>참조

- [명령 및 매개 변수](commands-parameters.md)
