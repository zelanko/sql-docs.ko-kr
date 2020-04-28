---
title: LocalDBStopTracing 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBStopTracing
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 1d50e040-8602-4ffa-be8f-b8633fdfa7ff
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e35b0c9b806b435a4a98a319180801094068caf1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68022043"
---
# <a name="localdbstoptracing-function"></a>LocalDBStopTracing 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  현재 Windows 사용자가 소유한 모든 SQL Server Express LocalDB 인스턴스에 대해 API 호출 추적을 비활성화합니다.  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBStopTracing();  
```  
  
## <a name="returns"></a>반환  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="remarks"></a>설명  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
