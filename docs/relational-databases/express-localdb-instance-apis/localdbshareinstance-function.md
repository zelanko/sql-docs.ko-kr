---
title: LocalDBShareInstance 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBShareInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 21eb3b9a-7d32-455b-89bb-f624198cd202
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7b6ca5e83973c167ce2c39ffb0ac717a44c29b85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85640806"
---
# <a name="localdbshareinstance-function"></a>LocalDBShareInstance 함수
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  지정된 공유 이름을 사용하여 컴퓨터의 다른 사용자와 함께 지정된 SQL Server Express LocalDB 인스턴스를 공유합니다.  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBShareInstance(  
           PSID pOwnerSID,  
           PCWSTR pInstancePrivateName,  
           PCWSTR pInstanceSharedName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 *pOwnerSID*  
 [입력] 인스턴스 소유자의 SID입니다.  
  
 *pInstancePrivateName*  
 [입력] 공유할 LocalDB 인스턴스의 프라이빗 이름입니다.  
  
 *pInstanceSharedName*  
 [입력] 공유할 LocalDB 인스턴스의 공유 이름입니다.  
  
 *dwFlags*  
 [입력] 나중에 사용하도록 예약되어 있습니다. 현재 0으로 설정해야 합니다.  
  
## <a name="returns"></a>반환  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 지정한 인스턴스 이름이 잘못되었습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 지정한 인스턴스가 존재하지 않습니다.  
  
 [LOCALDB_ERROR_ADMIN_RIGHTS_REQUIRED](../../relational-databases/express-localdb-error-messages/localdb-error-admin-rights-required.md)  
 이 작업을 실행하려면 관리자 권한이 필요합니다.  
  
 [LOCALDB_ERROR_SHARED_NAME_TAKEN](../../relational-databases/express-localdb-error-messages/localdb-error-shared-name-taken.md)  
 지정한 공유 이름이 이미 사용되었습니다.  
  
 [LOCALDB_ERROR_INSTANCE_ALREADY_SHARED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-already-shared.md)  
 지정된 인스턴스가 이미 공유되고 있습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="remarks"></a>설명  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
