---
title: getEncrypt 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3764ff5b9308b4b370dda14e98787513c28458c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983370"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  encrypt 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>반환 값  
 encrypt가 사용되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>Remarks  
 encrypt 속성이 **true**로 설정되어 있으면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 서버에 인증서가 설치되어 있는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 클라이언트와 서버 간에 전송되는 모든 데이터에 대해 SSL 암호화를 사용하도록 지정합니다.  
  
 encrypt 속성이 지정되어 있지 않거나 **false**로 설정되어 있으면 드라이버에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 SSL 암호화를 지원하도록 지정하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 SSL 암호화를 사용하도록 구성되어 있지 않으면 암호화 없이 연결이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 SSL 암호화를 사용하도록 구성되어 있으면 올바르게 구성된 JVM(Java Virtual Machine)에서 실행될 때 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 자동으로 SSL 암호화를 사용하고, 그렇지 않으면 연결이 종료되어 드라이버에서 오류가 발생합니다. encryption 속성이 설정되어 있지 않으면 [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) 메서드는 기본값인 **false**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
