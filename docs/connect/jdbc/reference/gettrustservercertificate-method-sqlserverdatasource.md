---
title: getTrustServerCertificate 메서드 (SQLServerDataSource) | Microsoft Docs
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
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0d22963fc8e916bb554ba5bb385efe1abfcd84c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  반환 된 **부울** trustServerCertificate 속성이 사용 되는지 여부를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** trustServerCertificate 사용 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 TrustServerCertificate 속성이로 설정 되어 있으면 **true**, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 통신 계층이 SSL을 사용 하 여 암호화 된 경우 (SECURE Sockets Layer) 인증서가 자동으로 트러스트 합니다. 즉,는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 유효성을 검사 하지 것입니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 인증서입니다. 기본값은 **false**입니다.  
  
 TrustServerCertificate 속성이로 설정 되어 있으면 **false**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 서버 SSL 인증서의 유효성을 검사 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
