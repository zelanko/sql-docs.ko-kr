---
title: SQLServerXAResource 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bc12b2f49633b00addeec742104d5e525c578f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XAResource 나타냅니다 XA에 대 한 분산 트랜잭션 관리 합니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.lang.Object  
  
 **구현:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>주의  
 구현 되는 XA 트랜잭션 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 를 사용 하 여 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 분산 트랜잭션 관리자 (DTC). SQLServerXAResource 클래스를 호출 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] DTC와 상호 작용 sqljdbc_xa.dll 이라는 dll을 확장 합니다. SQLServerXAResource (XA_START, XA_END, XA_PREPARE 등)에서 수신 되는 XA 호출은 해당 DTC 함수 호출에 매핑됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
