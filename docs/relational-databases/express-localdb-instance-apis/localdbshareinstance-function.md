---
title: LocalDBShareInstance 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LocalDBShareInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 21eb3b9a-7d32-455b-89bb-f624198cd202
caps.latest.revision: 9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e57ff8210a9676920805b655c7c2fa44c27f3c28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="localdbshareinstance-function"></a>LocalDBShareInstance 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 [입력] 공유할 LocalDB 인스턴스의 전용 이름입니다.  
  
 *pInstanceSharedName*  
 [입력] 공유할 LocalDB 인스턴스의 공유 이름입니다.  
  
 *dwFlags*  
 [입력] 나중에 사용하도록 예약되어 있습니다. 현재 0으로 설정해야 합니다.  
  
## <a name="returns"></a>반환 값  
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
  
## <a name="remarks"></a>주의  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
