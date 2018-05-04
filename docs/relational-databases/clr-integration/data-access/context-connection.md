---
title: 컨텍스트 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a608c42da2c7a6a0c1294718b1be52d247062961
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="context-connection"></a>컨텍스트 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  내부 데이터 액세스 문제는 상당히 일반적인 시나리오입니다. 즉, CLR(공용 언어 런타임) 저장 프로시저 또는 함수가 실행 중인 서버에 액세스하려는 경우입니다. 사용 하 여 연결을 만드는 한 가지 방법은 **System.Data.SqlClient.SqlConnection**로컬 서버를 가리키는 연결 문자열을 지정 하 고 연결을 엽니다. 이렇게 하려면 로그인에 사용할 자격 증명을 지정해야 합니다. 연결이 저장 프로시저나 함수가 아닌 다른 데이터베이스 세션, 다른 있을 수 있습니다 **설정** 옵션을 개별 트랜잭션에서 이루어지거나, 임시 테이블에 나타나지 않는 등입니다. 사용자의 관리 저장 프로시저 또는 함수 코드가 SQL Server 서버 프로세스에서 실행되는 경우 다른 사용자가 해당 서버에 연결하고 SQL 문을 실행하여 이를 호출했기 때문입니다. 싶이 저장된 프로시저 또는 함수를 함께 해당 트랜잭션, 해당 연결의 컨텍스트 내에서 실행 **설정** 옵션 및 기타 등등. 이를 컨텍스트 연결이라고 합니다.  
  
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
 [일반 vs입니다. 컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 일반 연결과 컨텍스트 연결의 차이를 설명합니다.  
  
 [일반 연결 및 컨텍스트 연결에 대 한 제한](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 일반 연결 및 컨텍스트 연결에 대한 제한 사항을 설명합니다.  
  
  
