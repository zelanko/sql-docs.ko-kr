---
title: 연결 이벤트
description: 데이터 원본에서 정보 메시지를 검색하고 상태가 변경되었는지 확인하기 위한 연결 이벤트입니다.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 5a29de74-acfc-4134-8616-829dd7ce0710
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 67b805e4ec95047b843e6b72ba10dc8fee4688d5
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419824"
---
# <a name="connection-events"></a>연결 이벤트

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server에는 데이터 원본에서 정보 메시지를 검색하거나 **연결** 상태가 변경되었는지 확인하는 데 사용할 수 있는 두 개의 이벤트가 있는 **Connection** 개체가 있습니다. 다음 표는 **Connection** 개체의 이벤트를 설명합니다.

|이벤트|Description|  
|-----------|-----------------|  
|**InfoMessage**|정보 메시지가 데이터 소스에서 반환될 때 발생합니다. 정보 메시지는 예외가 throw되지 않는 데이터 소스의 메시지입니다.|  
|**StateChange**|**연결** 상태가 변경되면 발생합니다.|  

## <a name="working-with-the-infomessage-event"></a>InfoMessage 이벤트 사용

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection> 이벤트를 사용하여 SQL Server 데이터 소스에서 경고 및 정보 메시지를 검색할 수 있습니다. 데이터 소스에서 반환된 오류의 심각도 수준이 11~16에 해당하면 예외가 throw됩니다. 그러나 <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트를 사용하여 오류와 무관한 데이터 소스의 메시지를 가져올 수 있습니다. Microsoft SQL Server의 경우 심각도 수준 10 이하의 모든 오류는 정보 메시지로 간주되고 <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트를 사용하여 캡처될 수 있습니다. 자세한 내용은 [데이터베이스 엔진 오류 심각도](/sql/relational-databases/errors-events/database-engine-error-severities) 문서를 참조하세요.

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트는 **오류** 속성에 데이터 원본의 메시지 모음을 포함하는 <xref:Microsoft.Data.SqlClient.SqlInfoMessageEventArgs> 개체를 받습니다. 이 컬렉션의 **오류** 개체에서 오류 번호와 메시지 텍스트 및 오류 소스를 쿼리 할 수 있습니다. Microsoft SqlClient Data Provider for SQL Server에는 데이터베이스, 저장 프로시저 및 메시지를 보낸 줄 번호에 대한 세부 정보도 포함되어 있습니다.

### <a name="example"></a>예제

다음 코드 예제에서는 <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트에 대한 이벤트 처리기를 추가하는 방법을 보여 줍니다.

[!code-csharp[SqlConnection_._InfoMessage#1](~/../sqlclient/doc/samples/SqlConnection_InfoMessage_StateChange.cs#1)]

## <a name="handling-errors-as-infomessages"></a>오류를 InfoMessages로 처리

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트는 일반적으로 서버에서 전송되는 정보 및 경고 메시지에 대해서만 발생합니다. 그러나 실제 오류가 발생하면 서버 작업을 시작한 **ExecuteNonQuery** 또는 **ExecuteReader** 메서드의 실행이 중지되고 예외가 발생합니다.

서버에서 발생한 오류와는 상관없이 명령에서 나머지 문을 계속 처리하려면 <xref:Microsoft.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A>의 <xref:Microsoft.Data.SqlClient.SqlConnection> 속성을 `true`로 설정합니다. 이렇게 하면 연결에서 예외를 throw하고 처리를 중단하는 대신 오류에 대해 <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트를 발생시킵니다. 그러면 클라이언트 애플리케이션에서 이 이벤트를 처리하고 오류 조건에 응답할 수 있습니다.

> [!NOTE]
> 심각도 수준이 17 이상인 오류는 서버에서 명령 처리를 중지하도록 하며 예외로 처리되어야 합니다. 이 경우 오류가 <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> 이벤트에서 처리되는 방법과 상관없이 예외가 throw됩니다.

## <a name="working-with-the-statechange-event"></a>StateChange 이벤트 사용

**StateChange** 이벤트는 **연결** 상태가 변경될 때 발생합니다. **StateChange** 이벤트는 **OriginalState** 및 **CurrentState** 속성을 사용하여 **연결** 의 상태 변경을 확인할 수 있는 <xref:System.Data.StateChangeEventArgs>를 받습니다. . **OriginalState** 속성은 변경되기 전의 **연결** 상태를 나타내는 <xref:System.Data.ConnectionState> 열거형입니다. **CurrentState** 는 **연결** 이 변경된 후의 상태를 나타내는 <xref:System.Data.ConnectionState> 열거형입니다.

다음 코드 예제는 **StateChange** 이벤트를 사용하여 **연결** 상태가 변경될 때 콘솔에 메시지를 씁니다.

[!code-csharp[SqlConnection_._StateChange#2](~/../sqlclient/doc/samples/SqlConnection_InfoMessage_StateChange.cs#2)]

## <a name="see-also"></a>참고 항목

- [데이터 원본에 연결](connecting-to-data-source.md)
