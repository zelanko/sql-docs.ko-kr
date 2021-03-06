---
description: setSelectMethod 메서드(SQLServerDataSource)
title: setSelectMethod 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c2b9c0fb4fb5f2a410abc790bf2f40d2bd2a64e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458368"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>setSelectMethod 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체를 사용하여 만들어진 모든 결과 집합에 사용되는 기본 커서 유형을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *selectMethod*  
  
 기본 커서 형식이 포함된 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 selectMethod는 결과 집합에 사용되는 기본 커서 유형입니다. 이 속성은 큰 결과 집합을 처리하면서 클라이언트측 메모리에 전체 결과 집합을 저장하지 않으려는 경우에 유용합니다. 이 속성을 "cursor"로 설정하면 보다 작은 여러 개의 데이터 청크를 한 번에 인출할 수 있는 서버측 커서를 만들 수 있습니다. selectMethod 속성이 설정되어 있지 않으면 [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)는 기본값인 “direct”를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
