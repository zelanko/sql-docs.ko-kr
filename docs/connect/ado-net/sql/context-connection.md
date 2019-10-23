---
title: 컨텍스트 연결
description: 컨텍스트 연결에 대해 설명 합니다.
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: b5ebd0b1b7357a385507d1ab528adde4023092da
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452259"
---
# <a name="the-context-connection"></a>컨텍스트 연결

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

내부 데이터 액세스 문제는 상당히 일반적인 시나리오입니다. 즉, CLR(공용 언어 런타임) 저장 프로시저 또는 함수가 실행 중인 서버에 액세스하려는 경우입니다. 한 가지 방법은 <xref:Microsoft.Data.SqlClient.SqlConnection>을 사용하여 연결을 만들고, 로컬 서버를 가리키는 연결 문자열을 지정하고, 연결을 여는 것입니다. 이렇게 하려면 로그인에 사용할 자격 증명을 지정해야 합니다. 연결은 저장 프로시저 또는 함수와 다른 데이터베이스 세션에 있거나, 다른 `SET` 옵션을 가지거나, 별도의 트랜잭션에 있거나, 사용자의 임시 테이블을 볼 수 없을 수 있습니다. 사용자의 관리 저장 프로시저 또는 함수 코드가 SQL Server 서버 프로세스에서 실행되는 경우 다른 사용자가 해당 서버에 연결하고 SQL 문을 실행하여 이를 호출했기 때문입니다. 저장 프로시저 또는 함수를 이 연결의 트랜잭션, `SET` 옵션 등과 함께 이 연결의 컨텍스트에서 실행하려는 경우가 있는데 이를 컨텍스트 연결이라고 합니다.  
  
컨텍스트 연결을 사용하여 코드를 처음 호출한 컨텍스트에서 Transact-SQL 문을 실행할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서에서 [컨텍스트 연결](https://go.microsoft.com/fwlink/?LinkId=115395) 을 참조 하세요.
