---
description: dbmslpcn.dll 공유 메모리의 ConnectionValidSharedMemory 함수
title: Connection유효한 Sharedmemory dbmslpcn.dll
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a487eb380ea4e7b0fe246efdb9281cbab63a1303
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475994"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 공유 메모리의 ConnectionValidSharedMemory 함수
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  함수는 SQL Server 공유 메모리가 설치 되어 있고 활성 상태 인지 여부를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>매개 변수  
 *szServerName*  
  
-   형식: **문자 \** _  
  
-   SQL server의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 형식: _ *BOOL**  
  
 유효 하지 않으면 0을 반환 합니다. else는 0이 아닌 값을 반환 합니다.  
  
  
