---
title: SQLServerXAResource 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7a40dc7a3f55a9c331f15783a4349e3ffbed269
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784068"
---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XA 분산 트랜잭션 관리를 위한 XAResource를 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.lang.Object  
  
 **구현:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Remarks  
 XA 트랜잭션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] DTC(분산 트랜잭션 관리자)를 사용하여 구현됩니다. SQLServerXAResource 클래스는 DTC와 상호 작용하는 sqljdbc_xa.dll이라는 이름의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 확장 dll을 호출합니다. SQLServerXAResource에서 받은 XA_START, XA_END, XA_PREPARE 등의 XA 호출은 해당하는 DTC 함수 호출에 매핑됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
