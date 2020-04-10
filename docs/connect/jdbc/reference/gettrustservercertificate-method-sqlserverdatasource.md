---
title: getTrustServerCertificate 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b84a323e3dd8bac95309f0462b48e322ba422c9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911407"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustServerCertificate 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Return Value  
 trustServerCertificate가 사용되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 trustServerCertificate 속성이 **true**로 설정되어 있으면 통신 계층이 SSL을 사용하여 암호화된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL(Secure Sockets Layer) 인증서가 자동으로 트러스트됩니다. 즉, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 인증서의 유효성을 검사하지 않습니다. 기본 값은 **false**입니다.  
  
 trustServerCertificate 속성이 **false**로 설정되어 있으면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 서버 SSL 인증서의 유효성을 검사합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
