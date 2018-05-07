---
title: setTrustServerCertificate 메서드 (SQLServerDataSource) | Microsoft Docs
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
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb5923c3078944a446abfc763c76122f44af2396
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **부울** trustServerCertificate 속성이 사용 되는지 여부를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *TrustServerCertificate*  
  
 **true 이면** 경우 서버 (SECURE Sockets Layer) 인증서 자동으로 트러스트 해야 하면 통신 계층이 SSL을 사용 하 여 암호화 됩니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 TrustServerCertificate 속성이로 설정 되어 있으면 **true**, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 통신 계층이 SSL을 사용 하 여 암호화 된 경우 SSL 인증서가 자동으로 트러스트 합니다. 즉,는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 유효성을 검사 하지 것입니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 인증서입니다. 기본값은 **false**입니다.  
  
 TrustServerCertificate 속성이로 설정 되어 있으면 **false**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 서버 SSL 인증서의 유효성을 검사 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
