---
title: 컨텍스트 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context connections [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- context [CLR integration]
ms.assetid: 67dd1925-d672-4986-a85f-bce4fe832ef7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f6334964a58e643ad373aa8fb0599f39bd3ba01c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919226"
---
# <a name="context-connection"></a>Context Connection
  내부 데이터 액세스 문제는 상당히 일반적인 시나리오입니다. 즉, CLR(공용 언어 런타임) 저장 프로시저 또는 함수가 실행 중인 서버에 액세스하려는 경우입니다. 한 가지 방법은 `System.Data.SqlClient.SqlConnection`을 사용하여 연결을 만들고, 로컬 서버를 가리키는 연결 문자열을 지정하고, 연결을 여는 것입니다. 이렇게 하려면 로그인에 사용할 자격 증명을 지정해야 합니다. 연결은 저장 프로시저 또는 함수와 다른 데이터베이스 세션에 있거나, 다른 `SET` 옵션을 가지거나, 별도의 트랜잭션에 있거나, 사용자의 임시 테이블을 볼 수 없을 수 있습니다. 사용자의 관리 저장 프로시저 또는 함수 코드가 SQL Server 서버 프로세스에서 실행되는 경우 다른 사용자가 해당 서버에 연결하고 SQL 문을 실행하여 이를 호출했기 때문입니다. 저장 프로시저 또는 함수를 이 연결의 트랜잭션, `SET` 옵션 등과 함께 이 연결의 컨텍스트에서 실행하려는 경우가 있는데 이를 컨텍스트 연결이라고 합니다.  
  
 컨텍스트 연결을 사용하여 코드를 처음 호출한 컨텍스트에서 Transact-SQL 문을 실행할 수 있습니다. 컨텍스트 연결을 얻으려면 다음 예와 같이 "context connection" 연결 문자열 키워드를 사용해야 합니다.  
  
 [C#]  
  
```  
using(SqlConnection connection = new SqlConnection("context connection=true"))   
{  
    connection.Open();  
    // Use the connection  
}  
```  
  
 [Visual Basic]  
  
```  
Using connection as new SqlConnection("context connection=true")  
    connection.Open()  
    ' Use the connection  
End Using  
  
```  
  
## <a name="in-this-section"></a>섹션 내용  
 [일반 연결과 컨텍스트 연결 비교](context-connections-vs-regular-connections.md)  
 일반 연결과 컨텍스트 연결의 차이를 설명합니다.  
  
 [일반 연결 및 컨텍스트 연결에 대한 제한 사항](context-connections-and-regular-connections-restrictions.md)  
 일반 연결 및 컨텍스트 연결에 대한 제한 사항을 설명합니다.  
  
  
