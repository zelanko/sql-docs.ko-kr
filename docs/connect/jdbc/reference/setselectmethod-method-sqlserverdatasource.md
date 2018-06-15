---
title: setSelectMethod 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a4de6cbf75816c584add43b3bfc1d9415f79f94
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843998"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>setSelectMethod 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 사용 하 여 만들어진 모든 결과 집합에 사용 되는 기본 커서 유형을 설정 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *selectMethod*  
  
 A **문자열** 기본 커서 유형을 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 selectMethod는 결과 집합에 사용되는 기본 커서 유형입니다. 이 속성은 큰 결과 집합을 처리하면서 클라이언트측 메모리에 전체 결과 집합을 저장하지 않으려는 경우에 유용합니다. 이 속성을 "cursor"로 설정하면 보다 작은 여러 개의 데이터 청크를 한 번에 인출할 수 있는 서버측 커서를 만들 수 있습니다. SelectMethod 속성이 설정 하지 않으면 [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) 기본값인 "direct"를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
