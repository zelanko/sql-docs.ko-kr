---
title: Dbmslpcn.dll 공유 메모리의에서 ConnectionValidSharedMemory 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cb8f36b1e9ab57711a2c24c026130e5b9a6fc382
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718121"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 공유 메모리의 ConnectionValidSharedMemory 함수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  함수는 SQL Server 공유 메모리 설치 및 활성화 되어 있는지 여부를 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>매개 변수  
 *szServerName*  
  
-   형식: **char\***  
  
-   SQL server의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 형식: **BOOL**  
  
 유효 하지 않으면 0 반환 합니다 그렇지 않으면 0이 아닌 값을 반환합니다.  
  
  
