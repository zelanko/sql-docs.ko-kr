---
title: 컨텍스트 연결 | Microsoft Docs
description: Microsoft SQL Server에서 컨텍스트 연결을 사용 하면 코드가 호출 된 동일한 컨텍스트에서 Transact-sql 문을 실행할 수 있습니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
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
ms.openlocfilehash: 3f29914557e3a1c1e7a929bec22a2b55d0db2a50
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81485585"
---
# <a name="context-connection"></a>컨텍스트 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  내부 데이터 액세스 문제는 상당히 일반적인 시나리오입니다. 즉, CLR(공용 언어 런타임) 저장 프로시저 또는 함수가 실행 중인 서버에 액세스하려는 경우입니다. 한 가지 옵션은 **SqlConnection**를 사용 하 여 연결을 만들고, 로컬 서버를 가리키는 연결 문자열을 지정 하 고, 연결을 여는 것입니다. 이렇게 하려면 로그인에 사용할 자격 증명을 지정해야 합니다. 연결이 저장 프로시저 또는 함수와 다른 데이터베이스 세션에 있거나, 다른 **SET** 옵션이 있을 수 있으며, 별도의 트랜잭션에 있거나, 임시 테이블을 볼 수 없습니다. 사용자의 관리 저장 프로시저 또는 함수 코드가 SQL Server 서버 프로세스에서 실행되는 경우 다른 사용자가 해당 서버에 연결하고 SQL 문을 실행하여 이를 호출했기 때문입니다. 저장 프로시저 또는 함수를 해당 연결의 컨텍스트에서 실행 하는 것이 좋습니다. 트랜잭션, **SET** options 등이 있습니다. 이를 컨텍스트 연결이라고 합니다.  
  
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
 [일반 연결 및 컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 일반 연결과 컨텍스트 연결의 차이를 설명합니다.  
  
 [일반 연결 및 컨텍스트 연결에 대한 제한 사항](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 일반 연결 및 컨텍스트 연결에 대한 제한 사항을 설명합니다.  
  
  
