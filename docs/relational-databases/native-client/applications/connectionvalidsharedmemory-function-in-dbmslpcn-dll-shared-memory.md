---
title: 연결유효한공유메모리 dbmslpcn.dll
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f3bb097965563afb458b4529676d1e9967e4899
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303893"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 공유 메모리의 ConnectionValidSharedMemory 함수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 함수는 SQL Server 공유 메모리가 설치되고 활성 상태인지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>매개 변수  
 *szServer이름*  
  
-   유형: **\* 문자**  
  
-   SQL 서버의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 유형: **BOOL**  
  
 유효하지 않은 경우 0을 반환합니다. else는 0이 아닌 것을 반환합니다.  
  
  
