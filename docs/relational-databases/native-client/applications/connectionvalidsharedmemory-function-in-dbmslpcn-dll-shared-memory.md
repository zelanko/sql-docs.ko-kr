---
title: ConnectionValidSharedMemory dbmslpcn .dll
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c64fe0020ca6c406cadd5b5b71ade1641919a81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244195"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 공유 메모리의 ConnectionValidSharedMemory 함수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  함수는 SQL Server 공유 메모리가 설치 되어 있고 활성 상태 인지 여부를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>매개 변수  
 *szServerName*  
  
-   형식: **char\* **  
  
-   SQL server의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 형식: **BOOL**  
  
 유효 하지 않으면 0을 반환 합니다. else는 0이 아닌 값을 반환 합니다.  
  
  
