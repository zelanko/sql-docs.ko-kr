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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7edee23f7111b55a6d34ac6ae10bf3720879fc01
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219307"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  encrypt 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Return Value  
 encrypt가 사용되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 encrypt 속성이 **true**로 설정되어 있으면, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 서버에 인증서가 설치되어 있는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 클라이언트와 서버 간에 전송되는 모든 데이터에 대해 TLS 암호화를 사용하도록 지정합니다.  
  
 encrypt 속성이 지정되어 있지 않거나 **false**로 설정되어 있으면, 드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 TLS 암호화를 지원하도록 적용하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 강제로 TLS 암호화를 사용하도록 구성되어 있지 않으면 암호화 없이 연결이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 강제로 TLS 암호화를 사용하도록 구성되어 있으면, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 올바르게 구성된 JVM(Java Virtual Machine)에서 실행되는 경우 자동으로 TLS 암호화를 사용하도록 설정합니다. 그렇지 않으면 연결이 종료되고 드라이버에서 오류가 발생합니다. encryption 속성이 설정되어 있지 않으면 [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) 메서드는 기본값인 **false**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
